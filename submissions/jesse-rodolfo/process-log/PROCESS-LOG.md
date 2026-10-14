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

Início: __:__  Fim: __:__

8:00 a 8:02 parado por bloqueio de permissão do macOS na pasta Documentos, resolvido liberando acesso para o Terminal. Tempo de setup, não de análise.

**O que pedi à IA:**

**O que a IA afirmou e eu mandei verificar:**

**Onde a IA errou e como corrigi:**

**O que os dados permitem concluir e o que não permitem:**

**Decisão minha:**

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
