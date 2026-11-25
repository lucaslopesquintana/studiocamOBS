# Roadmap e execução

## Fase 0 — Fundação (agora)

### Entregáveis
- [x] Plano mestre inicial
- [x] Arquitetura proposta
- [x] Requisitos iniciais
- [x] Contrato de comunicação preliminar
- [x] Perfil do hardware de referência
- [x] Plano de testes inicial
- [x] Criar repositório GitHub (`lucaslopesquintana/studiocamOBS`)
- [x] Fazer primeiro commit (estrutura Fase 0 + `.gitignore` e `.editorconfig` sincronizados)
- [x] Reorganizar raiz do repositório (conteúdo de `StudioCam/` promovido para a raiz, `StudioCam-Fase-0.zip` e artefatos web auxiliares removidos, `.gitignore` expandido)
- [ ] Confirmar Android SDK/JDK/Gradle/Android Studio
- [ ] Confirmar modelo exato/variante e versão de software do moto g35
- [ ] Instalar ADB e validar conexão USB
- [ ] Executar inventário Camera2 real
- [ ] Validar suporte do Windows 11 à câmera virtual em prova isolada
- [ ] Registrar ADRs aprovados

### Gate de saída
Repositório criado, ambiente reproduzível, inventário real do aparelho salvo e riscos críticos documentados.

## Fase 1 — Prova de captura Android

1. Criar app mínimo Kotlin.
2. Solicitar permissões e exibir preview Camera2.
3. Enumerar todas as câmeras e capacidades.
4. Listar resoluções e FPS ranges.
5. Testar MediaCodec H.264 com Surface input.
6. Medir FPS, bitrate, CPU, memória e temperatura.
7. Testar 30 minutos de captura local.

**Gate:** captura e codificação estáveis no moto g35, com relatório de capacidades.

## Fase 2 — Prova de transmissão

1. Criar sinalização local.
2. Implementar WebRTC Android.
3. Criar receiver de teste no desktop/browser.
4. Parear com token efêmero.
5. Medir latência, jitter, perda e bitrate.
6. Testar redes 2.4 GHz e 5 GHz.
7. Testar reconexão.

**Gate:** stream estável por 60 minutos em LAN, com métricas registradas.

## Fase 3 — Receptor Windows e câmera virtual

1. Criar app desktop mínimo.
2. Receber e decodificar vídeo.
3. Implementar preview próprio.
4. Fazer spike isolado da Media Foundation Virtual Camera.
5. Definir e implementar source/plugin exigido.
6. Registrar/remover câmera.
7. Testar OBS e um app de reunião.

**Gate:** câmera virtual aparece, entrega frames e pode ser removida sem deixar estado residual.

## Fase 4 — Integração e UX

- QR Code e descoberta.
- Painel de conexão.
- Controles remotos.
- Indicadores de qualidade.
- Reconexão e mensagens de erro.
- Fluxo de instalação.

## Fase 5 — Controles profissionais

- ISO, exposição e foco manuais quando suportados.
- Balanço de branco.
- Presets.
- Zebra, histograma e focus peaking.
- Modo tela escura seguro.
- Ajustes de imagem.

## Fase 6 — Distribuição

- Instalador Windows.
- APK assinado.
- Atualização.
- Auditoria de licenças.
- Documentação de usuário.
- Matriz de compatibilidade.
- Testes de regressão.

## Plano imediato — próximas tarefas

**Tarefa 0.1:** criar repositório GitHub vazio `StudioCam`, preferencialmente privado.

**Tarefa 0.2:** enviar esta estrutura e criar o commit `chore: establish StudioCam project foundation`.

**Tarefa 0.3:** clonar no PC e abrir no Antigravity.

**Tarefa 0.4:** instalar/validar Android Studio, JDK compatível, Android SDK Platform Tools e ADB.

**Tarefa 0.5:** conectar o moto g35 por USB, habilitar depuração USB conscientemente e executar `adb devices`.

**Tarefa 0.6:** criar um projeto Android mínimo e gerar o relatório de capacidades Camera2.

Não iniciar implementação WebRTC antes de concluir 0.6.
