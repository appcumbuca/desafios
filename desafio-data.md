O desafio pode ser feito em python ou R e para a entrega devem ser anexados os seguintes arquivos em um email respondendo à Fê Bernardo na data solicitada:

- Arquivo com o código para gerar um notebook com as respostas
- Documento resultante do notebook renderizado em PDF
- Arquivos com definições de funções, métodos e classes, se existirem

# Critérios de Avaliação

Algumas das questões que serão avaliadas, entre outras, são:

- A redação das respostas é clara e concisa? Busque a “resposta mínima suficiente”.
- Seu código é, tanto quanto plausível, separado em componentes isolados nomeados apropriadamente? Deveria ser possível, em algum nível, explicar o que o seu código faz apenas o lendo.
- Seu código é reutilizável e basta fazer leves alterações para satisfazer mudanças pequenas nos requerimentos do problema?

# Problemas

# Transcrição DNA → RNA

Os quatro nucleotídeos encontrados no DNA são adenina (A), citosina (C), guanina (G) e timina (T). Os nucleotídeos no RNA são adenina (A), citosina (C), guanina (G) e uracila (U). 

A transcrição de DNA em RNA acontece com as seguintes associações:

- `G` -> `C`
- `C` -> `G`
- `T` -> `A`
- `A` -> `U`

Então uma sequência de DNA `GGCTA` deveria ser transcrita em uma sequência `CCGAU` de RNA. Implemente uma função que recebe uma string com uma sequência de DNA (e.g. `"ACTGATA"`) e retorna outra string, com sua transcrição em RNA (e.g. `"UGACUAU"`)

# Processando e explorando dados em um banco relacional

A biblioteca `nyclfights13`, disponível para Python e R, traz cinco tabelas com dados de voos que passaram pela cidade de Nova Iorque em 2013. A documentação da biblioteca descreve o que significa cada coluna em cada tabela, mas resumidamente:

- `flights` tem um livro de voos
- `airports` lista os aeroportos envolvidos
- `planes` dados da construção dos aviões usados em cada voo
- `airlines` descreve as empresas aéreas operando
- `weather` dá medidas climáticas de hora em hora para o três aeroportos da cidade

Todas as tabelas podem ser conectadas usando as chaves apropriadas. Por exemplo, a aeronave de cada voo na tabela `flights` está identificada na variável `tailnum`, que também identifica unicamente cada linha na tabela `planes`. Com base nesse conjunto de dados, encontre:

- Gere um dataframe contendo o atraso médio, bem como o desvio-padrão e os percentis p25, p50, p90 e p99 para cada dia do ano. Explique sucintamente quais as tendências observadas ao longo do ano, clarifique que tipo de caso extremos são observados e pontue limitações da sua análise, se existirem.
- Existe alguma empresa aérea ou grupo pequeno de empresas que concentra a maior parte dos atrasos?
- Considerando a base como um todo, existe alguma relação entre a distancia a ser percorrida pelo voo e a fabricante do avião utilizado? Essa conclusão se mantém no nível de empresa aérea?

# Pensamento estatístico

Suponha que uma operadora de cartão está debatendo suas regras de atribuição de limite e um stakeholder envolvido gera uma visualização cruzando limite e inadimplência. Na visualização é nítido que a taxa de inadimplência cai linearmente no limite do cartão, argumentando a favor de uma regra mais relaxada de atribuição de limite.

- Sob que condições a conclusão apontada pela visualização se mantém?
- Como você explicaria para um stakeholder os limites da conclusão tirada dessa visualização?
- Que tipo de experimento você recomendaria para coletar evidência e respaldar essa conclusão?
- É comum que, para garantir um poder de teste mais elevado, a escala de um experimento tome proporções estratégicas para uma empresa, já que o custo de oportunidade de perda no grupo com resultados piores é potencialmente alta. Você recomendaria o mesmo desenho de experimento se fosse esse o caso? Se não, que desenho alternativo você sugeriria?
