# StudioCam

**Seu smartphone. Sua câmera profissional.**

StudioCam é um projeto para transformar smartphones Android em câmeras para computadores Windows, com transmissão local, controles de câmera e uma webcam virtual nativa.

> Nome provisório. A disponibilidade de marca, domínio e pacote Android ainda precisa ser verificada.

## Estado atual

- **Fase:** 0 — Fundação e especificação
- **Versão documental:** 0.1.0
- **Dispositivo de referência:** Motorola moto g35 5G
- **Sistema de referência:** Windows 11
- **Ferramentas:** Google AI Studio, Android Studio, Antigravity e GitHub
- **Estado do código:** ainda não iniciado

## Objetivo do MVP

Entregar vídeo ao vivo do moto g35 para um computador Windows 11 pela rede local e disponibilizá-lo como uma câmera selecionável por aplicativos de videoconferência.

A primeira meta de engenharia é **1080p a 30 FPS estáveis**, não 4K60. Resoluções e taxas maiores só serão anunciadas quando forem medidas em hardware compatível.

## Estrutura

```text
StudioCam/
├── docs/                  # Documentação normativa do projeto
├── android/               # Aplicativo Kotlin/Android
├── desktop/               # Aplicativo Windows e motor nativo
├── shared/
│   ├── protocol/          # Contratos de mensagens e sinalização
│   └── specifications/    # Especificações compartilhadas
├── .gitignore
└── README.md
```

## Documentos essenciais

1. `docs/PLANO_MESTRE.md`
2. `docs/ARQUITETURA.md`
3. `docs/REQUISITOS.md`
4. `docs/PROTOCOLO_COMUNICACAO.md`
5. `docs/ROADMAP.md`
6. `docs/PLANO_DE_TESTES.md`
7. `docs/DECISOES_TECNICAS.md`
8. `docs/PERFIL_HARDWARE_MOTO_G35.md`
9. `docs/GUIA_DE_TRABALHO_COM_IA.md`

## Princípios

- Rede local por padrão; nenhuma conta ou nuvem obrigatória para o uso básico.
- Pareamento autenticado e sessões protegidas.
- Recursos exibidos conforme capacidade real do dispositivo.
- Sem anúncios, marca d'água ou bloqueio artificial de funções essenciais.
- Nenhuma fase é considerada concluída apenas porque o código foi gerado.
- O GitHub é a fonte oficial da verdade; arquivos locais e conversas com IA não substituem commits e documentação.

## Como iniciar

1. Crie um repositório GitHub chamado `StudioCam` (recomendação: privado durante a fase inicial).
2. Extraia este pacote e envie o conteúdo para o repositório.
3. Clone o repositório no computador.
4. Abra a pasta no Antigravity e mantenha o Android Studio instalado para compilar e depurar.
5. Execute as tarefas de Fase 0 em `docs/ROADMAP.md`.
6. Não comece a implementação de streaming antes de concluir o inventário real de capacidades do moto g35.

## Fontes técnicas de referência

- Motorola — especificações do moto g35: https://pt-br.support.motorola.com/app/answers/detail/a_id/184470
- Android — CameraCharacteristics: https://developer.android.com/reference/android/hardware/camera2/CameraCharacteristics
- Android — foreground service types: https://developer.android.com/develop/background-work/services/fgs/service-types
- Android — restrições de foreground services: https://developer.android.com/develop/background-work/services/fgs/restrictions-bg-start
- Microsoft — MFCreateVirtualCamera: https://learn.microsoft.com/windows/win32/api/mfvirtualcamera/nf-mfvirtualcamera-mfcreatevirtualcamera
- WebRTC — documentação: https://webrtc.org/getting-started/overview
