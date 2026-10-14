# Process Log: Jessé Rodolfo Machado, Challenge 002

Ferramentas: Claude Code (sessão dirigida pelo CLAUDE.md da pasta), Python, Git.
Regra deste log: escrito durante o trabalho, por mim, com horário. A IA lista o que fez; eu escrevo o que decidi e por quê.

---

## Bloco 0: Leitura do problema (antes de abrir qualquer dado)

Início: 07:30  Fim: 07:55

O que o diretor quer saber: onde o time está perdendo tempo, o que dá pra deixar a IA fazer sem estragar o atendimento, e ver alguma coisa funcionando de verdade, não slide.

O que eu acho antes de olhar os dados:

O tempo não se perde resolvendo o problema, se perde esperando. Ticket parado sem ninguém pegar, ticket esperando o cliente responder, fila de um canal mais lenta que a de outro. Vi isso na fábrica e vi na logística: espera é o desperdício mais fácil de cortar e o que ninguém mede.
Desconfio que o ticket marcado como crítico não está sendo resolvido mais rápido que o médio. Se for isso, a prioridade é só uma etiqueta que ninguém usa.
Telefone e rede social devem demorar mais pra resolver que e-mail e chat, porque não fica registro organizado do que o cliente pediu.
O que derruba a nota do cliente é demorar pra dar a primeira resposta, mais do que demorar pra resolver. Cliente aguenta esperar a solução se alguém falou com ele logo.
Reembolso, problema de pagamento e cancelamento são os tickets que mais custam quando atrasam. Reembolso é dinheiro saindo, pagamento é dinheiro entrando, cancelamento é cliente indo embora. Esses merecem uma fila separada.
Classificar ticket pelo texto a IA faz bem e barato. O que não pode ser automático é decidir sobre dinheiro e lidar com cliente que já está irritado. Aprendi isso operando meus próprios agentes.

Como vou usar os dois arquivos: o dataset 1 é a operação que eu vou diagnosticar; o dataset 2 é o material para provar que a classificação automática funciona antes de propor ela para a operação. São duas organizações diferentes e não vou misturar.

O que vai me fazer desconfiar dos dados: coluna de tempo que na verdade é data e hora, não duração; nota de satisfação preenchida só em parte dos tickets; texto de ticket com cara de inventado; quantidade de linhas diferente dos 30 mil que o brief fala; e aquele “outros” do Kaggle, que eu já percebi que pode ser só o jeito do site resumir a coluna, e não uma categoria perdida.

O que eu decidi não fazer: não vou propor automação antes de fechar o diagnóstico; não vou misturar os dois arquivos como se fossem a mesma empresa; e não vou montar tela bonita antes de medir se o classificador acerta.

**Problema de setup encontrado:** o .gitignore da raiz do repositório ignora submissions/. Resolvido com `git add -f` dentro da minha pasta, sem tocar em arquivo fora dela.

Commit:

---

## Bloco 1: Auditoria dos dados

Início: 07:58  Fim: 08:15

8:00 a 8:02 parado por bloqueio de permissão do macOS na pasta Documentos, resolvido liberando acesso para o Terminal. Tempo de setup, não de análise.

**O que pedi à IA:**

**O que a IA afirmou e eu mandei verificar:**

**Onde a IA errou e como corrigi:**
- Primeira versão de `solution/analise/01_auditoria.py` usou a coluna `Product`, que não existe no dataset 1 (o nome real é `Product Purchased`). O script quebrou com KeyError antes de calcular qualquer coisa. Corrigido o nome e rodado de novo; nenhum número foi afirmado com a versão errada.

**Hipóteses do Bloco 0 confirmadas pela auditoria (escritas às 07:30, antes de abrir os dados):**
- Tempo como carimbo de hora: First Response Time e Time to Resolution são data e hora, todos entre 2023-05-31 21:53 e 2023-06-02 00:55. Não existe data de abertura, então não há duração calculável.
- O "outros" do Kaggle: o dataset 2 tem exatamente 8 categorias nomeadas, somando 47.837 de 47.837 linhas, sem nulo e sem categoria "Other". O "outros" era resumo da página do Kaggle, não categoria perdida.
- Satisfação preenchida só em parte: Customer Satisfaction Rating existe em 2.769 de 8.469 tickets (33%), só nos de status Closed.
- Texto com cara de inventado: 8.469 de 8.469 descrições têm o placeholder `{product_purchased}` sem substituir, e só 16 frases de abertura distintas.
- Quantidade diferente dos 30 mil: o D1 tem 8.469 tickets (28% dos 30 mil do brief).

**Lista da IA: o que fez e o que achou (para eu editar):**
- Escreveu e rodou `solution/analise/01_auditoria.py` nos dois CSVs brutos; resultado completo em `docs/auditoria-dados.md`.
- D1: 8.469 tickets (28% dos 30 mil do brief), 0 duplicados, 139 e-mails repetidos sempre com nome diferente.
- D1: nulos seguem o status. Open (2.819) sem nenhum tempo; Pending Customer Response (2.881) só com primeira resposta; Closed (2.769) com tudo.
- D1: Time to Resolution menos First Response Time é negativo em 1.365 de 2.769 fechados (49%).
- D1: CSAT só nos fechados, plano de 1 a 5, nenhum teste significativo (chi2 e Kruskal com p entre 0,148 e 0,876 para prioridade, canal, tipo, assunto, produto, gênero).
- D1: texto gerado. 100% com `{product_purchased}` sem substituir, 16 frases de abertura distintas, Resolution aleatório, tipo x assunto independentes (p=0,981).
- D1: categorias uniformes; prioridade não depende do tipo (p=0,561) nem do canal (p=0,078).
- D2: 47.837 textos realistas, 8 categorias desbalanceadas (Hardware 28,5% a Administrative rights 3,7%), ruído de rótulo visível.
- D1 x D2: categorias não correspondem; classificador não pode ser medido no texto do D1.

**O que os dados permitem concluir e o que não permitem:**

**Decisão minha:**
O D1 não serve para medir tempo nem satisfação, e eu vou provar isso em vez de fingir que serve. O que ele tem de confiável é a estrutura do backlog: 67% não fechados (33% abertos e 34% esperando o cliente), o que já sustenta a minha hipótese de que o desperdício está na espera. O diagnóstico vai dizer com clareza o que dá para afirmar, o que não dá, e o que a operação precisa registrar para passar a dar. O desperdício eu calculo em faixa, por premissa, sobre os 30 mil tickets por ano do brief, com cada premissa escrita para o diretor trocar pelo número dele. O D2 fica para provar que classificar ticket por texto funciona. Já vivi essa situação na logística: o indicador oficial escondia 500 pedidos, e a decisão certa foi consertar a medição antes de expandir. Aqui é a mesma coisa: instrumentar antes de automatizar.

Commit:

---

## Bloco 2: Diagnóstico

Início: __:__  Fim: __:__

**Os cinco números que importam:**
1.
2.
3.
4.
5.

**Premissas que eu defini para o cálculo de desperdício:**

**Onde a IA errou e como corrigi:**

**O que eu adicionei que a IA sozinha não faria:**

Commit:

---

## Bloco 3: Proposta de automação

Início: __:__  Fim: __:__

**Fluxo decidido (ticket entra até humano):**

**O que NÃO automatizar e o exemplo dos dados que justifica cada item:**

**De onde veio o critério do portão humano (minha experiência operando agentes):**

**Onde a IA quis automatizar demais e eu segurei:**

Commit:

---

## Bloco 4: Protótipo

Início: __:__  Fim: __:__

**O que construí e o que deixei de fora de propósito:**

**Como medi (tamanho da amostra aleatória, acurácia, matriz de confusão):**

**Testes de regressão escritos:**

**Onde a IA errou (código, avaliação, categorias) e como corrigi:**

**Iterações até funcionar:**

Commit:

---

## Bloco 5: Fechamento

Início: __:__  Fim: __:__

**O que cortei do documento final para ficar curto:**

**Limitações que assumi por escrito:**

**Tempo total:**

Commit:

---

## Resumo para o README (preencher no fim)

| Ferramenta | Para que usei |
|---|---|
| Claude Code | |
| Python | |
| Git | |

Iterações totais:
Maior erro da IA no processo:
Maior contribuição minha:
