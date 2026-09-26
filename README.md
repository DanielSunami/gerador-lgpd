# gerador-lgpd

[Agent Skill](https://agentskills.io) para criar **Política de privacidade** e **Termos de uso** de software open source ou distribuído de graça, à luz da [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm).

Pasta com um `SKILL.md`. Funciona em clientes que leem o padrão Agent Skills (Claude Desktop, Claude.ai, Claude Code, Grok, Cursor, Codex, etc.). Onde não houver skills, anexe a pasta ou cole o `SKILL.md` no início do chat.

Não é modelo jurídico pronto. O agente busca a lei no Planalto, pergunta o que o app faz com dado, confirma os fatos com você e só então escreve **os dois** arquivos de texto: `PRIVACIDADE.md` e `TERMOS.md`. A diferença entre eles é o ponto da skill.

A skill entrega Markdown. **Publicar** — um link público, em geral HTML num servidor web — é com você.

## Instalar

```bash
npx skills add DanielSunami/gerador-lgpd
```

## Privacidade e termos

A [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) **não pede** termo de uso (a GDPR também não). Pede, do **controlador**, informação sobre o **tratamento** — isso é a política de privacidade.

O termo de uso existe porque o software é livre ou grátis. Ele traduz a licença para quem não abre o `LICENSE`: pode usar e copiar; **não há garantia** (o código não promete funcionar); os autores não respondem por perda no seu aparelho nem por um fork com servidor. Em inglês isso é o “AS IS”; em português a skill escreve **sem garantia**, não “como está”.

| | Privacidade | Termos |
|---|---|---|
| Pergunta | O que acontece com o dado? | Posso usar? Tem garantia? |
| Lei típica | LGPD, quando há tratamento | Licença do código (MIT etc.) |
| Sem controlador nosso | Continua útil: diz que o dado fica no dispositivo | Continua o documento principal de uso livre |

## Claude Desktop e Claude.ai

1. Empacote a pasta **como pasta na raiz do ZIP** (o nome da pasta = `gerador-lgpd`):

```bash
zip -r gerador-lgpd.zip gerador-lgpd
```

Estrutura certa:

```
gerador-lgpd.zip
└── gerador-lgpd/
    ├── SKILL.md
    ├── README.md
    └── LICENSE
```

2. No Claude: **Customize → Skills → + → Create skill → Upload a skill**.
3. Envie o ZIP e ligue a skill na lista.

Detalhes: [Use skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

## Claude Code

```bash
cp -R gerador-lgpd ~/.claude/skills/gerador-lgpd
```

No repositório do app: `.claude/skills/gerador-lgpd/`.

## Outros clientes

| Cliente | Onde colocar |
|---|---|
| Cursor | `.cursor/skills/gerador-lgpd/` no projeto, ou a pasta de skills do usuário |
| Grok | `~/.grok/skills/gerador-lgpd/` |
| Qualquer chat | anexe `SKILL.md` (ou a pasta) e peça a política / os termos |

O `name` no frontmatter é `gerador-lgpd` e precisa coincidir com o nome da pasta.

## O que ela assume

- Política de Privacidade = tratamento de dados. Termos = uso livre e **sem garantia**.
- Autores de um app que só grava no dispositivo do usuário **não são** controlador nem operador.
- Quem decide o tratamento é o controlador. Operador é quem trata **em nome** dele. Você no próprio PC não é operador de si mesmo.
- Anonimizar é dever de quem trata. Se os autores não tratam, isso não vira item da política.
- Fork com servidor: quem hospeda se torna responsável.

## Licença

MIT. Os documentos gerados no seu projeto são seus; revise antes de publicar.
