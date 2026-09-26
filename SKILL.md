---
name: gerador-lgpd
description: Cria política de privacidade e termos de uso (LGPD) para software open source ou grátis. Use ao pedir gerador-lgpd, PRIVACIDADE.md, TERMOS.md ou privacy policy de app livre.
license: MIT
compatibility: Requires internet to fetch the current LGPD from planalto.gov.br
metadata:
  author: DanielSunami
  version: "1.0"
---

# Privacidade e termos (OSS / grátis)

Produz **os dois** arquivos de texto, sempre: `PRIVACIDADE.md` e `TERMOS.md`. A diferença entre eles é o ponto da skill. Não é parecer jurídico. Não inventa controlador, DPO, consentimento genérico, base legal nem anonimização.

A skill **só escreve texto** (Markdown no repositório). Não publica página, não sobe servidor, não registra domínio. **Cabe ao usuário** colocar os documentos num **link público** — o caminho usual é HTML num servidor web (`/privacidade`, `/termos`). Quem precisa apontar política em loja de app, rodapé ou art. 9º usa esse URL. No fim da entrega, lembre isso em uma linha.

## Os dois documentos

A LGPD **não exige termo de uso**. A GDPR também não. O que essas leis pedem, **quando há controlador**, é informação sobre o **tratamento** — isso vai na política de privacidade.

O termo de uso ainda vale, por outro motivo: o software é livre ou grátis. Alguém vai copiar, quebrar, perder dado no navegador ou hospedar um fork. O termo diz o que a licença já diz em prosa, para quem não abre o `LICENSE`:

- pode usar, copiar, modificar, distribuir (nos limites da licença);
- **não há garantia** — o código não promete funcionar, servir para o seu caso, estar disponível nem estar livre de erro (em inglês isso é o “AS IS”; em português **não** escreva “como está”. Use “sem garantia” e, se precisar de uma frase, “oferecido sem promessa de funcionamento”);
- autores não respondem por perda no dispositivo, conteúdo que o usuário inserir, nem por cópia que um terceiro hospedar;
- quem sobe um servidor com o código assume a própria política e os próprios termos.

| Arquivo | Responde | Não é |
|---|---|---|
| `PRIVACIDADE.md` | O que acontece com dado. Quem trata (se alguém). Direitos. | Licença, SLA, “pode copiar?” |
| `TERMOS.md` | Pode usar de graça? Tem garantia? De quem é o código? E o fork? | Aviso LGPD / lista de dados |

Gere os dois, mesmo no modo A (autores não tratam). A política nesse caso é curta e honesta; o termo carrega uso livre e ausência de garantia. Não funda os dois num arquivo só. Não chame o termo de “exigência da LGPD”.

## 0. Lei vigente (obrigatório, primeiro passo)

Antes de perguntar ou redigir, baixe o texto da LGPD nesta URL oficial:

https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm

Use a ferramenta HTTP que o ambiente tiver: WebFetch, browser, `curl`, etc. O HTML do Planalto costuma vir em latin-1 (ISO-8859-1); se o texto aparecer com `Ã` ou `�`, recodifique.

Exemplo com `curl`, se houver shell:

```bash
curl -sL -A 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36' \
  'https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm' \
  | iconv -f latin1 -t utf-8
```

Leia de novo: arts. 3º–5º, 6º–9º, 11–12, 16, 18, 20. Se o fetch falhar, diga isso ao usuário e siga com o que já estiver neste skill, sem fingir que leu a página.

## 1. Controlador, operador, software

- **Controlador** (art. 5º, VI): quem **decide** finalidade e meios do tratamento.
- **Operador** (art. 5º, VII): quem trata **em nome** do controlador. Pessoa distinta. Quem decide e executa sozinho no próprio aparelho **não** é operador de si mesmo — é só controlador (se a lei alcançar).
- **Software / autores:** se o binário só grava no dispositivo do usuário e os autores **não recebem** o conteúdo, eles **não são** controlador nem operador. São ferramenta (como um bloco de notas).
- **Uso só particular e não econômico** por pessoa natural: a lei pode não se aplicar (art. 4º, I).
- **Uso no trabalho:** controlador é o usuário ou a organização. Só existe operador se um terceiro tratar por eles (hospedagem, SaaS). Fork com servidor: **quem hospeda se torna responsável** e precisa da própria política.
- **Anonimização** (arts. 5º, XI, 12, 16): dever de quem trata. Se os autores não tratam, não coloque item de anonimização como obrigação do software. No art. 18, diga que anonimizar/bloquear **não existem como função**, se for o caso.
- **Dado sensível** (art. 5º, II / art. 11): só se o app **pedir** (campo de saúde, etc.). Texto livre e áudio podem carregar dado de terceiro; a responsabilidade é de quem anota. Voz gravada como anexo, em geral, é dado pessoal — biométrico só se usada para identificar.
- **Consentimento** (arts. 7º, I, e 8º): não use “ao usar você consente” como base dos autores se eles não tratam. Autorização genérica é nula (art. 8º, § 4º).
- **Art. 9º e 18:** se houver controlador, informe finalidade, forma, duração, quem é, contato, compartilhamento, responsabilidades e os direitos do art. 18 **um a um**. Se não houver tratamento dos autores, mapeie cada direito para o que o usuário já faz no dispositivo e marque o que não cabe (consentimento nosso, ANPD contra os autores).

Não invente DPO, RIPD, prazo de guarda nosso, criptografia extra, mailing nem base legal dos autores.

## 2. Descobrir o produto

Se estiver num repositório, inspecione armazenamento, rede, analytics, login, backup, arquivos/áudio. Preencha o quadro abaixo com o que já souber. O que faltar, **pergunte** (pode agrupar; não despeje questionário de escritório).

Quadro mínimo:

| Campo | Precisa para |
|---|---|
| Nome e uma linha do que o software faz | os dois docs |
| Autores e canal de contato (URL ou e-mail) | art. 9º / termos |
| Licença do código (MIT, etc.) | termos |
| Onde o dado vive: só o dispositivo / servidor dos autores / terceiro | papel dos autores |
| Conta, login, cookie, telemetria, crash, ads, pagamento | tratamento |
| O que o usuário insere (campos, texto livre, arquivo, áudio) | natureza dos dados |
| Backup / export / sync | portabilidade e saída |
| Quem hospeda o “oficial” vs clone local | cláusula de fork |
| País / lei (padrão: Brasil) | fecho |

Pergunte também se o app **pede** dado sensível ou só pode aparecer em texto/áudio.

## 3. Confirmar antes de escrever (obrigatório)

Mostre um **quadro de fatos** com o que você infereu e o que o usuário disse:

- papéis: autores (nem controlador nem operador **ou** controlador, com identificação) e, se houver, operador
- onde o dado fica
- o que entra no armazenamento
- o que **não** acontece (envio, analytics, conta…)
- contato, licença, data

Espere o usuário dizer que está correto. Corrija o que ele negar. **Não gere os arquivos antes disso.** Confira se cada tópico **obrigatório** do modo escolhido tem fato confirmado.

## 4. Tópicos por documento

Não pule obrigatório. Opcional só entra se o produto tiver aquele fato (não invente o tópico vazio). Os dois arquivos, sempre.

### `TERMOS.md`

**Obrigatório**

1. Nome do software e o que ele é (ferramenta; não é serviço com SLA nem contraprestação).
2. Ponte: isto não é a política de privacidade; o tratamento (se houver) está em `PRIVACIDADE.md`.
3. Uso livre alinhado à licença do código (usar, copiar, modificar, distribuir nos limites dela).
4. **Sem garantia** — sem promessa de funcionamento, adequação a um fim, disponibilidade, segurança ou ausência de erros. Título: *Sem garantia* ou *Ausência de garantia*. Em português não use “como está” nem “AS IS”.
5. Sem responsabilidade dos autores por: perda no dispositivo; conteúdo que o usuário inserir; fork, cópia ou hospedagem de terceiro.
6. Quem publica ou hospeda uma cópia responde por essa cópia (termos e privacidade dela).
7. Canal de contato, sem obrigação de suporte, correção ou resposta.
8. Lei aplicável (padrão: Brasil, no que couber a software grátis).
9. Data de publicação. Aviso curto de que o texto não é parecer.

**Opcional** (só se couber)

- Propriedade de marcas e nomes de terceiros que o usuário anotar.
- Inteligência artificial: o app envia dado a modelo, ou não envia (não misture “foi feito com IA” com tratamento dos registros).
- Natureza extra do produto (não é consulta jurídica, arquivo oficial, etc.).
- O que o usuário decide sozinho (ex.: se pode gravar áudio).
- Como o termo muda (publicação no repositório).
- Foro: só se o usuário pedir; não invente comarca exclusiva.

### `PRIVACIDADE.md`

Escolha o modo. **A** se os autores não recebem o dado. **B** se recebem (servidor, conta, analytics, cookie de rastreio, etc.). Não misture os dois.

#### Modo A — autores não tratam

**Obrigatório**

1. Uso **como distribuído**: sem conta, sem servidor nosso, sem envio dos registros.
2. Papel: autores não são controlador nem operador; o software grava no dispositivo do usuário.
3. Onde o dado fica (navegador / aparelho), em linguagem comum.
4. O que o usuário pode inserir (campos, texto, arquivo, áudio).
5. Operações locais (art. 5º, X): armazenar, acessar, buscar, modificar, reproduzir, extrair, eliminar — só neste dispositivo.
6. O que **não** há da nossa parte: coleta nossa, conta, telemetria, perfilamento, decisão automatizada, transferência internacional.
7. Compartilhamento: nenhum pelo software; saída só por ação do usuário (export, copiar, sync do SO/navegador).
8. Segurança: a do dispositivo; limpar dados do site / outro navegador / outro aparelho.
9. Retenção: enquanto o usuário não apagar; autores não guardam cópia. Sem prazo nosso de guarda.
10. Direitos do art. 18 mapeados ao dispositivo; o que não cabe (consentimento nosso, ANPD contra os autores), em uma linha cada.
11. Fork com servidor: quem hospeda se torna responsável por ela e precisa da própria política.
12. Canal de contato. Sem DPO, a menos que exista de verdade.
13. Lei (LGPD no que couber) e que o texto pode mudar no repositório.
14. Data de publicação. Aviso curto de que o texto não é parecer.

**Opcional**

- Tabela-resumo (agente, papel, natureza, finalidade, compartilhamento, proteção, direitos, transferência, decisão automatizada). **Sem** linha de anonimização.
- Dado sensível: o app não pede; texto/áudio ficam como inseridos; dado de terceiro é de quem anota — se houver texto livre ou áudio.
- Backup / export (o que vai e o que não vai, ex.: JSON sem áudio).
- Área de transferência, PWA, cookies de sessão do próprio site.
- Anonimização e bloqueio: só para dizer que **não existem como função**.

#### Modo B — autores tratam

Aviso do art. 9º. Base legal **confirmada pelo usuário**; não chute.

**Obrigatório**

1. Identificação do controlador e contato (art. 9º, III e IV).
2. Finalidade específica do tratamento (art. 9º, I).
3. Forma e duração do tratamento (art. 9º, II).
4. Base legal (art. 7º e, se sensível, art. 11) — a que o usuário confirmou. Sem “ao usar você consente”.
5. Quais dados, de onde vêm, se há dado sensível pedido pelo app.
6. Uso compartilhado: com quem e para quê (art. 9º, V). Se não houver, diga que não há.
7. Transferência internacional: se houver, o fato e o mecanismo; se não, diga que não há.
8. Responsabilidades dos agentes (art. 9º, VI): controlador; operador, se existir.
9. Direitos do art. 18 **um a um**, com canal para exercer (art. 9º, VII).
10. Segurança que de fato existe (não copie “melhores práticas” vazias).
11. Retenção: critério real de guarda e exclusão.
12. Decisão automatizada / perfilamento: se houver, o que o art. 20 exige; se não, diga que não há.
13. Fork / instância de terceiro: quem hospeda a própria cópia responde por ela.
14. Como o documento muda. Data. Aviso de que não é parecer.

**Opcional**

- Encarregado (DPO): contato só se existir.
- Interesse legítimo: descreva o interesse, se essa for a base.
- Cookies, telemetria, crash, ads, pagamento — o que o produto tiver.
- Crianças / idade, se o produto se destina a elas.
- Relatório de impacto: só se o usuário disser que existe.
- Tabela-resumo.
- Legítimo recusa de pedido (identidade não comprovada, guarda legal).

## 5. Redigir

Arquivos de texto na raiz do projeto (ou onde o usuário pedir): `PRIVACIDADE.md` e `TERMOS.md`. Português, seco, no tom do produto. Cubra cada obrigatório do modo escolhido. Data: hoje, salvo outro combinado.

Não gere site, rota, HTML nem deploy, salvo se o usuário pedir depois. Ao terminar, diga que os `.md` são o original e que **publicar o link** (em geral HTML no servidor) é com o usuário.

Não use detalhe técnico da implementação: localStorage, SQL, Postgres, Redis, key-value, IndexedDB, nome de biblioteca. Na maioria das vezes isso não é relevante para o leitor. Diga “neste navegador”, “no seu aparelho”, “num servidor nosso”. Só entre no jargão se o usuário pedir. Não funda os dois arquivos. Não chame o termo de exigência da LGPD.
