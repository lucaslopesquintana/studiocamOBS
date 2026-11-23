# Arquitetura — StudioCam

**Estado:** arquitetura proposta; interfaces internas ainda podem mudar após as provas de conceito.

## 1. Diagrama lógico

```text
┌──────────────────────── ANDROID ────────────────────────┐
│ Jetpack Compose (UI)                                    │
│        │                                                │
│ ViewModel / Use Cases                                   │
│        │                                                │
│ Camera Controller ── Camera2 ── Surface / ImageReader   │
│        │                                                │
│ Capability Registry                                     │
│        │                                                │
│ Encoder Adapter ── MediaCodec (H.264 inicial)           │
│        │                                                │
│ WebRTC PeerConnection + DataChannel                     │
└──────────────────────────┬──────────────────────────────┘
                           │ Wi-Fi / LAN
                           │ ICE + DTLS-SRTP / SCTP
┌──────────────────────────┴──────────────────────────────┐
│ WINDOWS DESKTOP                                         │
│ .NET UI                                                 │
│        │                                                │
│ Session / Device Manager                                │
│        │                                                │
│ Native C++ media bridge                                 │
│        ├── WebRTC receiver                               │
│        ├── Decoder / frame conversion                    │
│        └── Virtual camera source                         │
│                    │                                    │
│          Media Foundation Virtual Camera                │
└────────────────────┬────────────────────────────────────┘
                     │
              OBS / Meet / Zoom etc.
```

## 2. Android

### Módulos sugeridos

- `app`: composição da aplicação e navegação.
- `core-camera`: Camera2, seleção de câmera, capabilities e requests.
- `core-stream`: encoder, WebRTC e gestão da sessão.
- `core-domain`: casos de uso e modelos independentes de framework.
- `core-data`: DataStore e configurações.
- `core-telemetry`: métricas locais de desempenho.
- `feature-camera`: preview e controles.
- `feature-connection`: QR, estado de conexão e diagnóstico.

A estrutura pode começar como um único módulo Gradle para reduzir complexidade; a separação lógica deve existir desde o início. Só extrair módulos físicos quando houver benefício concreto.

### Captura

- Consultar `CameraManager.cameraIdList`.
- Consultar `CameraCharacteristics` para cada câmera.
- Consultar capacidades, tamanhos de saída, FPS ranges, foco e exposição.
- Criar sessão de captura e surfaces compatíveis com o encoder.
- Preferir fluxo direto para `MediaCodec` quando tecnicamente viável.
- Não assumir que a lente lógica permite selecionar todas as lentes físicas de forma independente.

### Controles

O domínio deve representar capacidades opcionais. Exemplo: `ManualExposureCapability`, `ManualFocusCapability`, `WhiteBalanceCapability`. A UI só oferece o controle se a câmera selecionada o suportar.

Focus peaking, zebra e histograma são ferramentas de análise/processamento; não são controles Camera2 nativos.

### Execução em segundo plano

A captura deve ser iniciada com o app visível e consentimento explícito. Em Android 14/API 34, serviços em primeiro plano que usam câmera precisam declarar o tipo `camera` e as permissões específicas correspondentes. Restrições de permissões while-in-use devem ser respeitadas. Ver documentação oficial.

## 3. Transporte e sinalização

### Mídia

- WebRTC para vídeo e, futuramente, áudio.
- H.264 como codec inicial por ampla interoperabilidade.
- Negociação de codec e perfil conforme capacidades do encoder/decoder.
- Bitrate adaptativo e resolução configurável.
- Medir perda, jitter, RTT, bitrate e FPS.

### Sinalização local

A sinalização WebRTC não é fornecida automaticamente pelo protocolo. O MVP deve incluir um mecanismo local para trocar SDP e ICE candidates.

Proposta inicial:
- Desktop cria uma sessão e um token aleatório de uso único.
- Desktop apresenta QR Code com endereço local, porta, identificador de sessão e token.
- Android escaneia e abre conexão local autenticada.
- Canal WebSocket/HTTPS local troca offer/answer e ICE candidates.
- Depois de estabelecida a sessão, mídia segue por WebRTC.
- Expiração do token e encerramento explícito da sessão.

A implementação deve tratar firewall do Windows, isolamento de clientes Wi-Fi, redes guest e múltiplas interfaces.

### ICE

- Primeiro testar candidatos host na LAN, sem servidor externo.
- STUN/TURN ficam fora do MVP local.
- Se houver necessidade futura de conexão entre redes, isso será outro escopo, com análise de privacidade, custo e segurança.

## 4. Desktop Windows

### Camadas

- UI C#/.NET: pareamento, preview, controles e diagnóstico.
- Camada de sessão: estado de conexão e comandos.
- Biblioteca nativa C++: recepção WebRTC, decodificação e entrega de frames.
- Componente de câmera virtual: integração Media Foundation.

### Risco da câmera virtual

`MFCreateVirtualCamera` cria/gerencia um objeto de câmera virtual, mas não equivale a um driver completo nem gera frames por conta própria. A prova de conceito deve validar:
- Modelo de fonte de câmera virtual aceito pela API.
- Implementação/registro da source.
- Formatos e tipos de mídia aceitos pelos consumidores.
- Ciclo de vida, permissões e remoção.
- Comportamento em aplicativos x86/x64 e processos sandboxed, quando aplicável.
- Instalação sem privilégios excessivos, se possível.

Não usar o OBS como dependência obrigatória. O OBS pode ser um primeiro consumidor/teste, não o mecanismo central do produto.

## 5. Áudio

Fora do caminho crítico do MVP. Vídeo virtual e dispositivo de áudio virtual são problemas distintos. Na primeira versão, priorizar vídeo. Microfone do celular e driver de áudio virtual serão especificados em ADR próprio.

## 6. Segurança e privacidade

- Pareamento com token aleatório, curto prazo e uso único.
- WebRTC usa criptografia de transporte (DTLS-SRTP para mídia).
- Sinalização local autenticada; não expor endpoint sem token.
- Bind em interfaces necessárias, não em todas por padrão.
- Não criar telemetria remota por padrão.
- Não persistir frames.
- Limpar sessão e credenciais temporárias ao desconectar.
- Informar claramente quando câmera/microfone estiverem ativos.
