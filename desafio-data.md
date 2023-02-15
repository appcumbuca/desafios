O desafio pode ser feito em python ou R e para a entrega devem ser anexados os seguintes arquivos em um email respondendo à Fê Bernardo na data solicitada:

- Arquivo com o código para gerar um notebook com as respostas
- Documento resultante do notebook renderizado em PDF
- Arquivos com definições de funções, métodos e classes, se existirem

# Critérios de Avaliação

Algumas das questões que serão avaliadas, entre outras, são:

- A redação das respostas é clara e concisa? Busque a “resposta mínima suficiente”.
- Seu código é, tanto quanto plausível, separado em componentes isolados nomeados apropriadamente? Deveria ser possível, em algum nível, explicar o que o seu código faz apenas o lendo.
- Seu código é extensível? O quão fácil é alterar suas soluções para atender a mudanças nos requerimentos do problema?

# Problemas

# Transcrição DNA → RNA

Os quatro nucleotídeos encontrados no DNA são adenina (A), citosina (C), guanina (G) e timina (T). Os nucleotídeos no RNA são adenina (A), citosina (C), guanina (G) e uracila (U). 

A transcrição de DNA em RNA acontece com as seguintes associações:

- `G` -> `C`
- `C` -> `G`
- `T` -> `A`
- `A` -> `U`

Então uma sequência de DNA `GGCTA` deveria ser transcrita em uma sequência `CCGAU` de RNA. Implemente uma função que recebe uma string com uma sequência de DNA (e.g. `"ACTGATA"`) e retorna outra string, com sua transcrição em RNA (e.g. `"UGACUAU"`)

# Momentos Estatísticos

Implemente uma função que computa o $k$-ésimo momento amostral. Suponha que a amostra será representada por uma estrutura de dados iterável como uma lista ou um vetor com as medidas da amostra. Modifique a implementação para que tenha um argumento adicional, `central` que recebe um valor lógico e caso verdadeiro, retorna o $k$-ésimo momento central.

# Processando e explorando dados em um banco relacional

A biblioteca `nyclfights13`, disponível para Python e R, traz cinco tabelas com dados de voos que passaram pela cidade de Nova Iorque em 2013. A documentação da biblioteca descreve o que significa cada coluna em cada tabela, mas resumidamente:

- `flights` tem um livro de voos
- `airports` lista os aeroportos envolvidos
- `planes` dados da construção dos aviões usados em cada voo
- `airlines` descreve as empresas aéreas operando
- `weather` dá medidas climáticas de hora em hora para o três aeroportos da cidade

Todas as tabelas podem ser conectadas usando as chaves apropriadas. Por exemplo, a aeronave de cada voo na tabela `flights` está identificada na variável `tailnum`, que também identifica unicamente cada linha na tabela `planes`. A documentação da biblioteca detalha quais são as informações disponíveis e como estão representadas. Com base nesse conjunto de dados:

1 - Compute a média móvel 30 dias e o desvio-padrão móvel, também na janela de 30 dias, dos atrasos. Gere uma visualização com as duas séries temporais.

2 - Encontre a porcentagem de voos que atrasam mais de 5 minutos por empresa aérea, por mês. Qual foi o pior mês do ano para a Delta Airlines?

3 - Calcule quantos aviões distintos são operados e quantos voos foram realizados para cada fabricante. Qual é a fabricante com menos voos?

4 - Qual é a empresa aérea que mais realizou voos com aviões da Airbus?

5 - Compute quantos voos cada aeroporto da cidade recebeu entre 18h e 22h do dia 3 de março.
