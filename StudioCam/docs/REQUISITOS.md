# Requisitos — StudioCam

## 1. Requisitos funcionais

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| FR-001 | Exibir preview da câmera | P0 | Preview contínuo no Android |
| FR-002 | Listar câmeras disponíveis | P0 | IDs e características detectadas |
| FR-003 | Alternar frontal/traseira | P0 | Alternância sem crash |
| FR-004 | Transmitir vídeo pela LAN | P0 | Desktop recebe stream |
| FR-005 | Parear por QR Code | P0 | Sessão autenticada criada |
| FR-006 | Exibir preview no desktop | P0 | Frames recebidos e renderizados |
| FR-007 | Registrar câmera virtual | P0 | Dispositivo selecionável no Windows |
| FR-008 | Encerrar sessão | P0 | Câmera e rede liberadas |
| FR-009 | Reconectar após falha | P1 | Recuperação controlada |
| FR-010 | Selecionar resolução/FPS | P1 | Apenas modos suportados |
| FR-011 | Consultar bateria/temperatura | P1 | Dados disponíveis e identificados |
| FR-012 | Controles manuais | P1 | Somente capacidades suportadas |
| FR-013 | Espelhar imagem | P1 | Orientação correta no destino |
| FR-014 | Presets | P2 | Salvar e restaurar configuração |
| FR-015 | Histograma/zebra/focus peaking | P2 | Ferramentas visuais validadas |

## 2. Requisitos não funcionais

| ID | Requisito | Critério |
|---|---|---|
| NFR-001 | Segurança | Sessão autenticada e mídia criptografada |
| NFR-002 | Privacidade | Uso local sem conta ou nuvem |
| NFR-003 | Estabilidade | Teste contínuo mínimo de 60 min |
| NFR-004 | Desempenho | Medir FPS, latência, bitrate, jitter e CPU |
| NFR-005 | Compatibilidade | Registrar versão Android, Windows e hardware |
| NFR-006 | Resiliência | Tratar perda de Wi-Fi e encerramento abrupto |
| NFR-007 | Usabilidade | Fluxo de conexão sem digitação manual de IP |
| NFR-008 | Manutenção | Código modular, logs úteis e testes |
| NFR-009 | Acessibilidade | Contraste e controles legíveis |
| NFR-010 | Distribuição | Instaladores reproduzíveis e assináveis |

## 3. Perfis de vídeo iniciais

Perfis são opções condicionais, não garantias universais.

| Perfil | Resolução | FPS alvo | Estado |
|---|---:|---:|---|
| Econômico | 1280×720 | 30 | Candidato |
| Padrão | 1920×1080 | 30 | Meta principal |
| Fluido | 1920×1080 | 60 | Experimental |
| Alta resolução | 3840×2160 | 30/60 | Fora do MVP; validar |

A lista final deve ser a interseção de:
1. tamanhos e FPS suportados pela câmera;
2. capacidades do encoder;
3. perfil negociado pelo WebRTC;
4. capacidades do decoder e consumidor Windows;
5. estabilidade térmica e de rede.

## 4. Estados da sessão

`DISCONNECTED → DISCOVERING → PAIRING → CONNECTING → STREAMING → RECONNECTING → DISCONNECTED`

Estados de erro devem conter código, mensagem legível e ação sugerida. Não deixar a UI em estado de conexão indefinido.

## 5. Fora de escopo

- Gravação em nuvem.
- Login obrigatório.
- Streaming público pela internet.
- Compartilhamento de vídeo sem consentimento.
- Acesso remoto silencioso à câmera.
