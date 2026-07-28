# mba-eng-fullcycle

Repositório de estudo do MBA. Cada matéria/disciplina vira uma pasta de conteúdo na raiz.

## Matéria: Design Docs

- `design-docs/` — material bruto que o usuário vai alimentando ao longo do curso (anotações, resumos, exemplos, links, etc.). Sem estrutura fixa; aceite o que for adicionado.
- `.claude/skills/` — skills do Claude Code destiladas desse conteúdo. O objetivo final é ter, ao fim do MBA, um compilado de skills relevantes para o processo de engenharia de software com IA.

### Workflow esperado

Sempre que novo conteúdo for adicionado em `design-docs/`:

1. Ler o conteúdo novo e decidir: isso vira uma skill nova, ou incrementa/melhora uma skill existente em `.claude/skills/`?
2. Skills devem seguir o formato padrão SKILL.md (frontmatter `name` + `description` iniciando com "Use when...", foco em técnica/processo reutilizável — não em resumo do conteúdo estudado).
3. Preferir menos skills, bem consolidadas, a uma skill por post. Só criar uma nova quando o tema for claramente distinto das existentes.
4. Ao editar uma skill existente, verificar se o novo conteúdo não conflita com o que já está lá; se conflitar, atualizar em vez de duplicar.
