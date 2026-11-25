# StudioCam Android

Aplicativo Android nativo em Kotlin + Jetpack Compose.

## Estado
Ainda não inicializado. Não gerar a aplicação completa antes do inventário Camera2 do moto g35.

## Direção
- Camera2 para captura.
- MediaCodec para codificação.
- WebRTC para transporte.
- DataStore para preferências.
- Foreground Service com tipo/permite de câmera conforme versão Android.

## Primeira tarefa de implementação
Criar um app mínimo que:
1. solicite permissão de câmera;
2. liste `cameraId`;
3. consulte `CameraCharacteristics`;
4. mostre preview de uma câmera;
5. exporte um relatório técnico das capacidades detectadas.

Não implementar streaming nesta primeira tarefa.
