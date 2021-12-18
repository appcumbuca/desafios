# Desafio Data

O desafio pode ser feito em python ou R e para a entrega devem ser anexados os seguintes arquivos em um email para `data@comadre.com.br`:

- Arquivo com o código para gerar um notebook com as respostas
- Documento resultante do notebook renderizado em PDF
- Arquivos com definições de funções, métodos e classes, se existirem

# Critérios de Avaliação

A avaliação é holística e irá considerar o todo do que for apresentado. É melhor apresentar algum esboço de solução do que nada. É melhor apresentar uma solução ineficiente que funciona do que um esboço de uma solução eficiente. É melhor apresentar uma solução com espaço para melhoras, clara e fácil de modificar do que uma solução otimizada, complexa e de difícil extensão. 

Algumas das questões que serão avaliadas, entre outras, são:

- Se os requisitos do problema forem levemente alterados basta alterar levemente a sua solução original?
- O código é internamente consistente nas suas escolhas estéticas, de indentação e fácil de ler? Considere tamanho e possíveis ambiguidades dos nomes que usar para entidades no seu código.
- O código consiste de componentes reutilizáveis que podem ser aplicados em outros contextos? Scripts são reutilizáveis, mas não são componentes, funções (ou classes com métodos) são componentes reutilizáveis.

Diferenciais:

- Uso dos padrões e semântica sugeridos pelo seu framework de Data Science de escolha (e.g. pandas, tidyverse, data.table, polars, DataFrames, DataFramesMeta, etc).
- Testes unitários para as suas soluções.
- Usar ideias de programação funcional.

# Problemas

# Transcrição DNA → RNA

Os quatro nucleotídeos encontrados no DNA são adenina (A), citosina (C), guanina (G) e timina (T). Os nucleotídeos no RNA são adenina (A), citosina (C), guanina (G) e uracila (U). 

A transcrição de DNA em RNA acontece com as seguintes associações:

- `G` -> `C`
- `C` -> `G`
- `T` -> `A`
- `A` -> `U`

Então uma sequência de DNA `GGCTA` deveria ser transcrita em uma sequência `CCGAU` de RNA. Implemente uma função `dna_to_rna(dna)` que recebe uma string com uma sequência de DNA (e.g. `"ACTGATA"`) e retorna outra string, com sua transcrição em RNA (e.g. `"UGACUAU"`)

# Fibonacci

A sequência de Fibonacci é definida recursivamente:

```
x_1 = 1 
x_2 = 1
x_n = x_{n-1} + x_{n-2} ; n > 2
```
- Primeira parte: Implemente uma função `fibonacci(n)` que retorna o n-ésimo termo da sequência de Fibonacci.
- Segunda parte: Implemente uma função `fibonacci_seq(n)` que retorna a sequência de Fibonacci até o seu n-ésimo termo.

# Processando e explorando dados em um banco relacional

A biblioteca `nyclfights13`, disponível para Python e R, traz cinco tabelas com dados de voos que passaram pela cidade de Nova Iorque em 2013. A documentação da biblioteca descreve o que significa cada coluna em cada tabela, mas resumidamente:

- `flights` tem um livro de voos
- `airports` lista os aeroportos envolvidos
- `planes` dados da construção dos aviões
- `airlines` descreve as empresas aéreas operando
- `weather` dá medidas climáticas de hora em hora para o três aeroportos da cidade

Todas as tabelas podem ser conectadas usando as chaves apropriadas. Por exemplo, a aeronave de cada voo na tabela `flights` está identificada na variável `tailnum`, que também identifica unicamente cada linha na tabela `planes`.

Com base nesse conjunto de dados, gere um *dataframe* com as informações pertinentes para cada item:

- Calcule o atraso médio, bem como o desvio-padrão, a assimetria e a curtose dos atrasos em cada dia do ano. Plote um gráfico com as séries históricas de média e desvio-padrão.
- Quantos voos foram feitos em segundas-feiras com aviões fabricados em anos bissextos? Plote um gráfico de barras com os valores para cada ano.
- Quantos voos cada empresa aérea operou por aeroporto?
- Mude o formato da resposta do item anterior de *long* para *wide* (dica: atenção com o número de colunas resultante).
- Qual o percentual de voos que decolou em condições de visibilidade abaixo da média (use como referência a visibilidade média do ano todo) em cada aeroporto, no mês de dezembro?

# Um pouco de Estatística Computacional

- Implemente uma função que sorteia números aleatoriamente de uma Distribuição Uniforme entre 0 e 1 até que a soma dos valores sorteados seja maior que 1 e retorna a quantidade de números sorteados.

Exemplos:
    - Sorteio: `0.1, 0.3, 0.22, 0.9, 0.07, 0.63`, resultado: 4
    - Sorteio: `0.84, 0.33, 0.91, 0.12, 0.41`, resultado: 2
- Realize vários ensaios do experimento acima e reporte a média dos resultados. Plote um gráfico relacionando a diferença entre a média e o número de Euler com o número de ensaios realizados.
- Se o experimento for modificado para medir quantos números são sorteados da mesma distribuição até sua soma seja maior que 2, qual é a média dos resultados de um número grande de ensaios?
- Se o experimento for modificado para medir quantos números são sorteados de uma Distribuição Chi-Quadrado com 1 grau de liberdade até sua soma seja maior que 3, qual é a média dos resultados de um número grande de ensaios?
