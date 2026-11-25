# Registro de decisões técnicas (ADR)

Este documento registra decisões aprovadas e pendências. Decisões provisórias não devem ser tratadas como fatos imutáveis.

## ADR-0001 — Android como primeira plataforma

- **Estado:** aprovado
- **Decisão:** começar por Android e Windows 11.
- **Motivo:** reduzir escopo e validar o caso de uso central.
- **Consequência:** iOS/macOS/Linux ficam fora do MVP.

## ADR-0002 — moto g35 como dispositivo de referência

- **Estado:** aprovado para testes iniciais
- **Decisão:** usar Motorola moto g35 5G.
- **Motivo:** hardware disponível para validação real.
- **Consequência:** requisitos do MVP precisam ser realistas para esse aparelho, sem limitar a arquitetura futura.

## ADR-0003 — Camera2 como API inicial

- **Estado:** aprovado, sujeito à prova de capacidades
- **Decisão:** usar Camera2 para controle e captura.
- **Motivo:** acesso às características e controles de câmera.
- **Consequência:** consultar capacidades em runtime e oferecer fallback.

## ADR-0004 — WebRTC como transporte inicial

- **Estado:** aprovado para protótipo
- **Decisão:** WebRTC para vídeo e DataChannel para comandos.
- **Motivo:** transporte em tempo real, criptografia e adaptação de rede.
- **Consequência:** sinalização local e gestão de sessão precisam ser implementadas.

## ADR-0005 — H.264 como codec inicial

- **Estado:** aprovado para protótipo
- **Decisão:** iniciar com H.264.
- **Motivo:** interoperabilidade ampla.
- **Consequência:** validar encoder e decoder reais; HEVC fica para avaliação posterior.

## ADR-0006 — Webcam virtual nativa Windows

- **Estado:** direção aprovada; implementação pendente de prova
- **Decisão:** investigar Media Foundation Virtual Camera.
- **Motivo:** evitar dependência obrigatória do OBS.
- **Consequência:** criar spike isolado; `MFCreateVirtualCamera` não deve ser confundida com implementação completa da source.

## ADR-0007 — Vídeo antes de áudio

- **Estado:** aprovado
- **Decisão:** áudio virtual não faz parte do caminho crítico do MVP.
- **Motivo:** reduzir complexidade de drivers.
- **Consequência:** áudio será tratado em etapa posterior.

## ADR-0008 — 1080p30 como meta principal

- **Estado:** aprovado como meta, não como garantia
- **Decisão:** validar 1080p30 antes de 4K ou 60 FPS.
- **Motivo:** equilíbrio entre qualidade, consumo, temperatura e estabilidade.
- **Consequência:** perfis superiores dependem de benchmark.

## Pendências para ADR futuro

- Biblioteca WebRTC Android e desktop escolhida e licença.
- Biblioteca de QR Code.
- Transporte de sinalização e porta padrão.
- Arquitetura exata da source Media Foundation.
- Estratégia de distribuição/assinatura do componente nativo.
- Estratégia USB sem ADB.
