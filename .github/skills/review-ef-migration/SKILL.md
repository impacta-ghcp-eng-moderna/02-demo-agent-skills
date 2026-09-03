---
name: review-ef-migration
description: Revisa migrations do Entity Framework Core antes da aplicação, com foco em risco para dados, coerência com entidade e model snapshot e limitações do provedor SQLite. Use quando uma migration for criada ou alterada.
argument-hint: "[caminho da migration]"
user-invocable: true
disable-model-invocation: false
---

# Revisar migrations do Entity Framework Core

Use esta skill para revisar uma migration criada ou alterada. Não a use para
explicar consultas, endpoints ou regras de negócio sem mudança de esquema.

## Procedimento

1. Leia `Up`, `Down`, model snapshot, entidade, configuração do EF Core e
   especificação aplicável.
2. Compare a intenção declarada com as operações e com o modelo atual.
3. Classifique separadamente problemas confirmados e riscos que dependem dos
   dados existentes, do SQL gerado ou do provedor.
4. Use [checklist.md](checklist.md) quando a revisão detalhada for necessária.
5. Consulte
   [examples/risky-column-change.md](examples/risky-column-change.md) quando
   houver `DropColumn` seguido de `AddColumn`, mudança de nulabilidade ou
   possível reconstrução de tabela.

Se algum artefato estiver ausente, registre a limitação. Segurança em banco
vazio não comprova segurança sobre dados existentes.

## Inspeção estática opcional

Escolha o script compatível com o ambiente:

- [scripts/inspect-migration.sh](scripts/inspect-migration.sh) para Bash;
- [scripts/inspect-migration.ps1](scripts/inspect-migration.ps1) para
  PowerShell.

Os dois apenas localizam padrões para revisão humana. Leia a versão escolhida
antes de solicitar sua execução e use-a somente após aprovação normal da tool.
Não trate correspondências como veredito.

Não aplique nem reverta a migration. Não altere arquivos durante a revisão.

## Formato da resposta

Apresente achados por severidade. Para cada um, informe arquivo e operação,
evidência, impacto e menor ação de correção ou validação. Se não houver problema
confirmado, não declare risco zero: liste o que ainda exigiria um banco
descartável com estado conhecido.
