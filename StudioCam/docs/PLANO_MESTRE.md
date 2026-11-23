# Plano Mestre — StudioCam

**Versão:** 0.1.0  
**Data:** 23/11/2026  
**Estado:** Proposta de engenharia — sujeita às provas de viabilidade da Fase 0

## 1. Visão

Transformar um smartphone Android em uma câmera de vídeo para Windows, com transmissão local de baixa latência, controles remotos e disponibilização como webcam virtual.

### Proposta de valor

- Gratuito para as funções essenciais.
- Sem anúncios e sem marca d'água.
- Conexão simples e segura na rede local.
- Controles compatíveis com o hardware real do aparelho.
- Webcam virtual independente do OBS.
- Transparência sobre resolução, FPS, latência e limitações.

O projeto não deve competir apenas por uma lista de funcionalidades. Deve competir por confiabilidade, qualidade mensurável, facilidade de conexão e manutenção.

## 2. Público inicial

- Profissionais em reuniões online.
- Professores e palestrantes.
- Criadores de conteúdo e streamers.
- Produtores de cursos e gravações.
- Usuários que desejam melhorar a webcam sem comprar outra câmera.

## 3. Escopo inicial

**Plataforma de referência:** Android no Motorola moto g35 5G + Windows 11.

**Conexão principal:** Wi-Fi na mesma rede local.

**MVP:** câmera traseira/frontal, preview, pareamento, transmissão H.264, preview desktop e webcam virtual Windows.

**Meta inicial de qualidade:** 1920×1080 a 30 FPS, se suportado pelo caminho de captura/encoder e sustentado termicamente. 60 FPS será experimental e condicionado ao hardware.

## 4. Fora do escopo do MVP

- iOS, macOS e Linux.
- Streaming pela internet.
- Conta de usuário ou infraestrutura em nuvem.
- Multi-câmera.
- LUTs e correção avançada de cor.
- Áudio virtual próprio.
- 4K60 como promessa de compatibilidade universal.
- Conexão USB sem ADB ou sem instalação/configuração adicional.

## 5. Princípios arquiteturais

1. Separação entre UI, domínio, captura, transporte e integração Windows.
2. Capacidades consultadas em runtime; não presumir recursos de câmera.
3. Codificação por hardware quando disponível e validada.
4. WebRTC como transporte inicial de mídia e canal de dados.
5. Sinalização local separada do transporte de mídia.
6. Segurança desde o pareamento: token efêmero, autenticação e criptografia.
7. Telemetria local e consentida; não coletar dados pessoais desnecessários.
8. Compatibilidade testada em aplicativos reais, não apenas em preview próprio.
9. Dependências e licenças auditadas antes de distribuição.
10. Cada fase exige evidências e critérios de aceite.

## 6. Indicadores de qualidade

| Indicador | Meta de engenharia inicial |
|---|---|
| Perfil principal | 1080p30 |
| FPS recebido | Sustentar 30 FPS em teste de 60 min |
| Latência ponta a ponta | Medir; objetivo inicial ≤150 ms na LAN |
| Estabilidade | 60 min sem encerramento ou travamento |
| Reconexão | Recuperar sessão após interrupção de Wi-Fi |
| Temperatura | Sem aviso térmico crítico ou interrupção |
| Webcam virtual | Selecionável em pelo menos OBS e um app de reunião |
| Segurança | Pareamento autenticado; sessão criptografada |
| Recursos manuais | Exibir apenas os controles suportados |

Esses números são metas de validação, não resultados já alcançados. Latência precisa ser medida ponta a ponta com método documentado.

## 7. Estratégia de entrega

- Primeiro: provar captura e codificação no moto g35.
- Segundo: provar recepção de vídeo no Windows em um viewer próprio.
- Terceiro: implementar a webcam virtual.
- Quarto: controles remotos e UX de conexão.
- Quinto: recursos avançados e otimização.

A integração com a câmera virtual é um risco técnico relevante e deve ter uma prova de conceito isolada. Não presumir que `MFCreateVirtualCamera` sozinho implemente a fonte de vídeo.

## 8. Critérios de conclusão do MVP

- Instalação reproduzível do Android e desktop.
- Conexão local autenticada por QR Code ou fluxo equivalente.
- Vídeo recebido com perfil 1080p30 no dispositivo de referência, se o hardware permitir.
- Webcam virtual registrada e removível corretamente.
- Teste documentado com OBS e pelo menos um aplicativo de videoconferência.
- Teste contínuo de 60 minutos.
- Reconexão após queda de rede.
- Sem falhas críticas conhecidas.
- Documentação, limitações e versões atualizadas.

## 9. Governança

- `main` deve permanecer estável.
- Implementações ocorrem em branches curtas.
- Alterações arquiteturais relevantes geram ADR em `DECISOES_TECNICAS.md`.
- Não aceitar código gerado sem revisão, compilação e teste.
- Nenhum segredo, token ou chave deve ser commitado.
- Toda dependência precisa ter versão e licença verificadas.
