# Protocolo de comunicação — StudioCam

**Versão do protocolo:** 0.1 — proposta inicial

## 1. Canais

1. **Sinalização:** HTTP/WebSocket local autenticado para trocar SDP e ICE.
2. **Mídia:** WebRTC PeerConnection.
3. **Comandos/telemetria:** WebRTC DataChannel confiável e ordenado no MVP.

## 2. QR Code de pareamento

O QR Code não deve conter senha permanente nem credencial reutilizável.

Exemplo ilustrativo de payload:

```json
{
  "v": 1,
  "sessionId": "uuid",
  "host": "192.168.1.20",
  "port": 43821,
  "token": "random-single-use-token",
  "expiresAt": "2026-11-23T12:00:00Z"
}
```

O formato final deve ser validado e versionado. Token deve ser criptograficamente aleatório, expirar rapidamente e ser invalidado após uso.

## 3. Envelope de mensagem

```json
{
  "version": 1,
  "messageId": "uuid",
  "type": "camera.set",
  "timestamp": "2026-11-23T12:00:00Z",
  "payload": {}
}
```

Campos:
- `version`: versão do protocolo.
- `messageId`: idempotência/rastreamento.
- `type`: tipo de mensagem.
- `timestamp`: diagnóstico; não usar como relógio confiável.
- `payload`: conteúdo validado pelo tipo.

## 4. Tipos iniciais

### Comandos desktop → Android

- `session.start`
- `session.stop`
- `camera.list`
- `camera.select`
- `camera.set`
- `stream.configure`
- `device.get_status`
- `ping`

### Respostas Android → desktop

- `command.ack`
- `command.error`
- `camera.capabilities`
- `device.status`
- `stream.stats`
- `pong`

## 5. Exemplo de comando de câmera

```json
{
  "version": 1,
  "messageId": "e8d7...",
  "type": "camera.set",
  "timestamp": "2026-11-23T12:00:00Z",
  "payload": {
    "cameraId": "0",
    "controls": {
      "exposureMode": "manual",
      "iso": 400,
      "exposureTimeNs": 10000000,
      "focusMode": "manual",
      "focusDistance": 2.0
    }
  }
}
```

Este exemplo não garante suporte. O Android deve validar cada campo contra as capacidades atuais e responder com valores aplicados ou erro específico.

## 6. ACK e erros

Exemplo:

```json
{
  "version": 1,
  "messageId": "e8d7...",
  "type": "command.ack",
  "payload": {
    "status": "applied",
    "applied": {
      "iso": 400
    }
  }
}
```

Códigos sugeridos:
- `UNSUPPORTED`: recurso não suportado.
- `OUT_OF_RANGE`: valor fora do intervalo.
- `INVALID_STATE`: comando incompatível com estado atual.
- `CAMERA_BUSY`: câmera ocupada.
- `PERMISSION_DENIED`: permissão negada.
- `TIMEOUT`: comando expirou.
- `INTERNAL_ERROR`: falha inesperada.

## 7. Regras

- Validar schema e tamanho máximo de mensagem.
- Comandos de configuração devem ser idempotentes quando possível.
- Nunca confiar em valores enviados pelo desktop sem validar no Android.
- Limitar taxa de comandos para evitar saturação.
- Não enviar dados pessoais desnecessários.
- Registrar versão do protocolo em toda sessão.
