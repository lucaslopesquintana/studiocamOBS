# Plano de testes — StudioCam

## 1. Ambiente de referência

- Telefone: Motorola moto g35 5G.
- Android: versão instalada no aparelho; especificar no relatório.
- PC: Windows 11; registrar edição, build e arquitetura.
- Rede: roteador local; registrar banda, canal e sinal.
- Cabo: USB-C de dados; validar que não é apenas cabo de carga.

## 2. Inventário Android

Registrar para cada `cameraId`:
- facing e orientação;
- hardware level;
- capacidades Camera2;
- tamanhos de saída por formato;
- FPS ranges;
- sensor active array;
- focal lengths;
- zoom ratio, quando suportado;
- controle AF/AE/AWB;
- faixas de ISO e exposição;
- flash disponível;
- logical/physical camera relationships;
- codecs disponíveis via MediaCodec.

Não inferir disponibilidade de lente física apenas pela ficha comercial.

## 3. Testes de captura

| ID | Teste | Resultado esperado |
|---|---|---|
| CAM-01 | Abrir câmera traseira | Preview sem crash |
| CAM-02 | Abrir câmera frontal | Preview sem crash |
| CAM-03 | Trocar câmera | Troca limpa de sessão |
| CAM-04 | Enumerar capacidades | Relatório completo |
| CAM-05 | Captura 720p30 | FPS medido |
| CAM-06 | Captura 1080p30 | FPS medido |
| CAM-07 | Encoder H.264 | Bitstream válido |
| CAM-08 | Captura 30 min | Sem encerramento térmico |

## 4. Testes de rede

- Pareamento válido.
- Token expirado.
- Token reutilizado.
- Dispositivos em redes diferentes.
- Wi-Fi desconectado durante streaming.
- Mudança de banda/roteador.
- Perda e retorno da rede.
- Firewall bloqueando sinalização.
- Cliente não autorizado tentando conectar.

## 5. Métricas

Registrar:
- resolução negociada;
- FPS de captura, encoder, receiver e renderização;
- bitrate;
- RTT;
- jitter;
- packet loss;
- latência ponta a ponta;
- uso de CPU e memória no PC;
- temperatura/bateria no Android;
- eventos de reconexão.

Não confundir FPS de captura com FPS renderizado. Latência deve ser medida por método repetível, por exemplo, timestamp de origem sincronizado ou gravação de alta velocidade de evento visual e monitor.

## 6. Testes Windows

- Registrar câmera virtual.
- Listar câmera no Windows.
- Abrir preview em aplicativo de teste.
- Abrir no OBS.
- Abrir em Meet/Zoom/Teams, conforme disponibilidade.
- Desconectar telefone durante uso.
- Encerrar app desktop.
- Reiniciar Windows.
- Remover câmera virtual.
- Reinstalar e atualizar.

## 7. Critério de aprovação

Nenhum teste crítico será aprovado apenas por inspeção visual informal. Registrar versão do código, aparelho, OS, condições, resultado, logs e evidência.
