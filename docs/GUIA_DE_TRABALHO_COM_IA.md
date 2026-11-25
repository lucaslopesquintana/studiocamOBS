# Guia de trabalho com IA — StudioCam

## 1. Regra central

A IA implementa tarefas delimitadas. A arquitetura, os requisitos e os critérios de aceite deste repositório prevalecem sobre sugestões improvisadas no chat.

## 2. Antes de qualquer alteração

O agente deve:
1. Ler `README.md` e os documentos relevantes em `docs/`.
2. Identificar a fase e o requisito atendido.
3. Inspecionar o código existente antes de propor mudanças.
4. Explicar arquivos que pretende criar/alterar.
5. Não substituir arquivos ou arquitetura sem justificativa.
6. Não introduzir dependências sem explicar necessidade, versão e licença.

## 3. Durante a implementação

- Trabalhar em uma tarefa por vez.
- Não inventar resultados de testes.
- Não afirmar suporte de hardware sem consultar capacidades.
- Não esconder erros com fallbacks silenciosos.
- Não inserir chaves, tokens ou credenciais no código.
- Não coletar frames ou telemetria fora do dispositivo sem consentimento.
- Preservar compatibilidade com a versão mínima Android definida no projeto.
- Atualizar documentação quando contrato ou comportamento mudar.

## 4. Ao concluir

O agente deve entregar:
- Resumo da implementação.
- Arquivos criados/alterados.
- Comandos executados.
- Resultado real de build e testes.
- Limitações e riscos conhecidos.
- Passos manuais necessários.
- Confirmação de que não alterou escopo não solicitado.

## 5. Prompt-base para Antigravity / Gemini

```text
Você está trabalhando no projeto StudioCam. Antes de editar, leia README.md e os documentos relevantes em docs/, especialmente PLANO_MESTRE.md, ARQUITETURA.md, REQUISITOS.md e ROADMAP.md.

A tarefa desta sessão é: [DESCREVER UMA ÚNICA TAREFA].

Regras:
- Respeite a arquitetura e os requisitos documentados.
- Inspecione o estado atual do repositório antes de modificar.
- Não reescreva arquivos inteiros sem necessidade.
- Não adicione dependências sem justificar versão, função e licença.
- Não presuma capacidades do aparelho: consulte Camera2/MediaCodec em runtime.
- Não marque testes como aprovados sem executá-los.
- Não implemente funcionalidades fora da tarefa.
- Atualize documentação e testes relacionados.
- Ao final, informe arquivos alterados, comandos executados, resultados, limitações e próximos passos.

Critério de aceite: [CRITÉRIO OBJETIVO].
Se houver ambiguidade técnica que altere arquitetura, pare e apresente opções com consequências antes de codificar.
```
