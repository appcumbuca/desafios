# Desafio de Programação Back-End
Primeiramente, agradecemos por seu interesse na Cumbuca. Somos uma fintech que busca ajudar as pessoas a cuidarem melhor das 
finanças coletivas, ajudando-as a realizarem sonhos e cuidar de quem mais importa para elas. No âmbito dessa missão, sempre
buscamos pessoas excepcionais para nossa equipe. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.


## Introdução

Seu desafio será fazer um **banco de dados chave-valor transacional, persistente
e multi-usuário** usando a linguagem Elixir.

Isso significa que esse banco permitirá a vários usuários salvarem valores sob 
chaves definidas e depois recuperá-los e modificá-los - incluindo com uso concorrente.

Adicionalmente, o banco deverá oferecer a capacidade de entrar em um 
estado onde todas as operações realizadas podem ser desfeitas ou aplicadas 
no banco - mas apenas se estas não conflitarem com as operações de outro usuário.

Seu programa deve ser implementado como um servidor que irá expor a interface
do banco de dados em uma porta específica da máquina que a executa. O banco será
manipulado através de uma interface HTTP descrita abaixo.


## Restrições

O desafio deve ser implementado utilizando a linguagem de programação Elixir.
Outras linguagens não serão aceitas.

Para implementar a comunicação via HTTP, sugerimos o uso do framework 
[Phoenix](https://github.com/phoenixframework/), mas qualquer framework ou 
biblioteca que implemente conexões HTTP poderá ser utilizada.

Solicitamos que o uso de bibliotecas externas além daquelas necessárias para
a implementação da comunicação via HTTP seja minimizado.

O repositório entregue deve especificar o comando a ser utilizado para
inicializar o servidor.

## A ferramenta

O banco de dados deve ser implementado como um servidor onde os comandos
serão enviados via HTTP.

### Enviando comandos

Os comandos serão enviados como uma chamada HTTP POST contendo o texto do 
comando no seu corpo. Para fins de testes, pode ser utilizado o comando
`curl` ou qualquer outra ferramente que permita realizar requisições HTTP.

Presumindo que o servidor do banco de dados esteja rodando na porta 4444,
o comando abaixo envia o comando `SET ABC 1` para o banco.

```
curl -H 'X-Client-Name: A' -X POST -d 'SET ABC 1' localhost:4444
```

A resposta HTTP enviada deve conter o texto da resposta do banco de dados 
ao comando em seu corpo.

Notar o header `X-Client-Name`. Esse header será usado para simular
múltiplos clientes conectados ao banco. O banco deve considerar que comandos
com o mesmo header `X-Client-Name` pertencem ao mesmo usuário. Isso será
especialmente importante para a implementação de transações, conforme descrito
abaixo na seção **Transações**.

Para a lista de comandos a serem implementados, ver a seção **Comandos** abaixo.

A maioria dos comandos a serem implementados se referem à manipulação de chaves
e valores. A próxima seção esclarece a sintaxe a ser utilizada para estes.

## Chaves e valores

As chaves do banco devem ser strings. Ao passar uma chave para um comando que espere isso,
a chave é passada simplesmente escrevendo o seu valor - exceto caso a chave contenha espaços
em branco, caso no qual ela deve ser cercada de aspas duplas. Chaves serão representadas da
mesma forma que valores do tipo string, com as mesmas restrições e o uso de aspas duplas
conforme necessário.

Os valores podem ser inteiros, strings ou booleanos.

Um inteiro será indicado por sua representação numérica. 
Por exemplo, `10` é um inteiro. Um inteiro deve conter apenas dígitos.

Uma string será representada pelo seu texto. Qualquer sequência de caracteres não contenha
somente dígitos e que seja diferente de `TRUE`, `FALSE` ou `NIL` será interpretada como uma string. 
Caso a string contenha espaços em branco, contenha somente dígitos, seja `TRUE`, `FALSE`, ou `NIL`, 
ela deve ser cercada de aspas duplas. 

Caso uma string contenha o caractere "aspa dupla" em seu conteúdo, esse deve ser precedido
de uma barra invertida `\` para que não seja considerado como encerrando a string.

Por exemplo, `abcd`, `a10`, `"uma string com espaços"`, `"\"teste\""` `"101"` e `"TRUE"` 
são todas strings, com os valores `abcd`, `a10`, `uma string com espaços`, `"teste"`, `101`
e `TRUE` respectivamente.

Um booleano é representado pelos símbolos `TRUE` e `FALSE`.

Além desses tipos, o valor `NIL` pode ser retornado ao consultar uma chave inexistente.
Esse valor não pode ser inserido.

### Exemplos

- O input `ABC` representa a sequência de caracteres `ABC`.
- O input `"ABC"` representa a exata mesma sequência de caracteres que o input anterior.
- O input `你好` representa a sequência de caracteres `你好`.
- O input `TRUE` representa o booleano verdadeiro.
- O input `"TRUE"` representa a sequência de caracteres `TRUE` (que não deve ser confundida com o booleano verdadeiro)
- O input `AB C` representa duas entradas separadas: `AB` e `C`.
- O input `"AB C"` representa a sequência de caracteres `AB C`.
- O input `"AB"C"` é inválido, por conter uma aspa simples descasada.
- O input `"AB\"C"` representa a sequência de caracteres `AB"C`.
- O input `a10` representa a sequência de caracteres `a10`.
- O input `10a` representa a sequência de caracteres `10a`.
- O input `10`, por conter apenas dígitos, representa o número 10.

## Persistência

O banco de dados implementado neste desafio deve ser persistente. Isto é, as 
operações que o banco reporte como completas devem gerar uma escrita em 
armazenamento durável ou, de outra forma, garantir que os valores escritos
possam depois ser recuperados, mesmo que o servidor do banco seja encerrado.

Para tal fim, sugerimos usar escrita em arquivos com uma estratégia apropriada.

## Transações

O banco de dados implementado deve suportar transações.
Uma transação é um estado especial no qual um cliente pode entrar, no qual
alterações feitas pelo usuário não serão visíveis para outros usuários.

Isto é, enquanto um usuário estiver numa transação, alterações feitas pelo
mesmo no banco só serão visíveis para ele mesmo. A transação pode ser "cancelada"
(descartando todas as transações feitas) ou "aplicada" (tornando suas alterações
visíveis).

Leituras feitas pelo próprio usuário numa transação também irão ignorar escritas
feitas por outros usuários após o início da transação.

Para mais detalhes, ver as seções `BEGIN`, `COMMIT` e `ROLLBACK` em **Comandos**.

## Comandos


Devem ser implementados os comandos abaixo a serem interpretados pela interface do banco.
Caso se tente invocar um comando que não seja um dos abaixo, deve ser emitido um erro apropriado. O formato dos erros fica a cargo do candidato, mas deixamos uma sugestão nos exemplos abaixo. Erros de usuário devem ser retornados com status HTTP 400, e requisições executadas com sucesso com status HTTP 200.

Todos os comandos devem ser seguros quando executados num ambiente concorrente - suponha sempre que pode haver múltiplos usuários conectados ao servidor. Nunca nenhuma execução de comandos deve deixar o servidor em um estado inválido.


Nos exemplos abaixo, a linha `Request` contém o corpo da requisição `POST` e a linha `Reponse` contém o corpo da respectiva resposta.

### Exemplos de Erros

#### Comando inexistente

Caso se tente invocar um comando que não seja um dos abaixo, deve ser emitido um erro apropriado.

```
Request: TRY
Response: ERR "No command TRY"
```

#### Sintaxe inválida

Caso um comando seja chamado com sintaxe incorreta, deve também ser emitido um erro.

```
Request: SET x
Response: ERR "SET <chave> <valor> - Syntax error"
```

Os comandos descritos a seguir também podem definir casos de erro específicos a cada comando.

### SET <chave> <valor>

O comando `SET` deve definir o valor de uma chave. Caso a chave não exista, ela deve ser criada.
Caso a chave já existe, ela será sobreescrita. O comando deve retornar o valor
antigo da chave (caso este existisse, caso contrário `NIL`) e o novo valor dela.

Não deve ser possível inserir o valor `NIL`. Tentar fazer isso irá gerar um erro.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
Request: SET teste 1
Response: NIL 1
Request: SET teste 2
Response: 1 2
```

Valores que não sejam strings não podem ser utilizados como chaves:
```
Request: SET 10 1
Response: ERR "Value 10 is not valid as key"
```

Inserir `NIL` é um erro:
```
Request: SET teste NIL
Response: ERR "Cannot SET key to NIL"
```

### GET <chave>

O comando `GET` deve recuperar o valor de uma chave. Caso a chave não exista, deve ser retornado
o valor NIL. Caso a chave exista, deve ser retornado o valor armazenado nela.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
Request: GET teste
Response: NIL
Request: SET teste 1
Response: NIL 1
Request: GET teste
Response: 1
```

Chaves no banco podem ser somente strings. 
Tentativas de buscar chaves que não sejam strings são um erro:

```
Request: GET 10
Response: ERR "Value 10 is not valid as key"
Request: GET NIL
Response: ERR "Value NIL is not valid as key"
```

### BEGIN

O comando `BEGIN` deve iniciar uma transação.
Enquanto um cliente estiver em "modo de transação", modificações inseridas 
por ele não devem ser visíveis para outros clientes. Todavia, caso o
próprio cliente busque as chaves alteradas, as modificações devem ser retornadas.

A resposta de `BEGIN` deve ser `OK`.
Se `BEGIN` for utilizado com uma transação já aberta, isso deve ser um erro.

Nos exemplos abaixo, presumimos dois clientes simultaneamente conectados, `A` e `B`.
Suas respectivas requisições e resposta são escritas como `RequestA` e `ResponseA` ou
`RequestB` e `ResponseB` respectivamente.

Notar que uma transação será encerrada através dos comandos `COMMIT` ou `ROLLBACK` 
descritos abaixo.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
RequestA: BEGIN
ResponseA: OK
RequestA: SET teste 1
RsponseA: NIL 1
RequestB: GET teste
ResponseB: NIL
RequestA: GET teste
ResponseA: 1
```

Não é possível abrir uma transação dentro de uma transação já em andamento:
```
RequestA: BEGIN
ResponseA: OK
RequestA: BEGIN
ResponseA: ERR "Already in transaction"
```

Em uma transação, alterações feitas por outros usuários não são visíveis:

```
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
RequestA: BEGIN
ResponseA: OK
RequestB: SET teste 1
ResponseB: NIL 1
RequestB: GET teste
ResponseB: 1
RequestA: GET teste
ResponseA: NIL
```

### ROLLBACK

O comando `ROLLBACK` deve encerrar uma transação *sem aplicar suas alterações*. Isto é,
todas as alterações criadas na transação atual devem ser descartadas. Deve retornar o nível de
transação após o rollback.

O comando ROLLBACK deve emitir um erro caso usado no nível de transação 0.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
RequestA: BEGIN
ResponseA: OK
RequestA: SET teste 1
ResponseA: FALSE 1
RequestB: GET teste
ResponseB: NIL
RequestA: GET teste
RequestA: 1
RequestA: ROLLBACK
ResponseA: OK
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
```

Notar que, para o usuário B, é como se a transação nunca tivesse existido.

### COMMIT

O comando `COMMIT` irá submeter os efeitos de uma transação para visualização
por todos os usuários - desde que essa transação seja _aplicável_.
Uma transação é aplicável se todas as chaves lidas por ela permanecem com
os mesmos valores que elas tinham no momento em que foram lidas, caso
tenham sido lidas dentro da transação.

Isto é: Cada vez que for lida uma chave numa transação, a transação deve
lembrar-se de qual o valor lido e na hora em que o comando COMMIT for
executado, este deve dar erro a não ser que os valores lidos continuem
os mesmos. Alterações feitas pelo próprio usuário dono da transação são 
isentas dessa regra.

O objetivo dessa regra é que uma transação deve poder ser vista como
uma unidade atômica. Caso isso não seja possível, o cliente deve retentar
a transação.

Caso o COMMIT falhe por essa razão, ele deve mostrar a lista de variáveis
que causou a falha.

**Exemplos**:

Após executar o COMMIT com sucesso, suas alterações tornam-se visíveis para todos
```
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
RequestA: BEGIN
ResponseA: OK
RequestA: SET teste 1
ResponseA: FALSE 1
RequestB: GET teste
ResponseB: NIL
RequestA: GET teste
RequestA: 1
RequestA: COMMIT
ResponseA: OK
RequestA: GET teste
ResponseA: 1
RequestB: GET teste
ResponseB: 1
```

Caso um valor lido na transação tenha sido alterado, o COMMIT falha:
```
RequestA: GET teste
ResponseA: NIL
RequestB: GET teste
ResponseB: NIL
RequestA: BEGIN
ResponseA: OK
RequestA: SET teste 1
ResponseA: FALSE 1
RequestB: GET teste
ResponseB: NIL
RequestA: GET teste
RequestA: 1
RequestB: SET teste 10
ResponseB: NIL 10
RequestA: COMMIT
ResponseA: ERR "Atomicity failure (teste)"
RequestA: GET teste
ResponseA: 10
```

Notar que após a falha do commit, o cliente A saiu da transação como se 
`ROLLBACK` tivesse sido executado.

## Avaliação 

Seu desafio deve ser disponibilizado por meio de um repositório Git acessível
à equipe da Cumbuca. Caso não queira disponibilizá-lo publicamente, converse
conosco para combinarmos como podemos acessar seu código.

### Critérios de avaliação

#### Testes
Devem ser fornecidos testes automatizados que validem as regras de negócio 
especificadas para a ferramenta.

#### Ausência de bugs
Seu código deve funcionar corretamente, atendendo a todos os requisitos da especificação representada por este documento e sem apresentar erros

#### Legibilidade e Formatação
Lembre-se que um trecho de código em geral será lido muito mais vezes do que
escrito. Escreva seu código pensando em quem for lê-lo. Busque minimizar
dificuldades de leitura. Use a indentação a seu favor. Siga boas práticas de
formatação de código da linguagem escolhida.

#### Clareza
Seu código deve deixar a sua intenção clara para o leitor. Tanto quanto seja
plausível, deve ser possível entender o que o código faz apenas lendo ele.
Explicações usando comentários deveriam ser redundantes.

#### Desacoplamento
Seu código não deve criar dependências desnecessárias entre módulos.
Ao alterar uma parte do código, não deveria ser necessário alterar partes sem
relação lógica com a parte alterada.

## Após o desafio
Em geral, iremos avaliar seu código poucos dias após o envio. Uma vez que nossa
avaliação esteja completa, iremos enviar um feedback sobre sua resolução. Caso
seu código seja aprovado, além do feedback, iremos marcar uma data para uma
conversa por videochamada com você.

### Conversa pós-entrega
Após a entrega de seu desafio, conversaremos com você sobre a estrutura do seu código e as escolhas feitas por você. Esteja pronta(o) para explicar as decisões que tomou e conversar sobre alternativas.

## Dúvidas

Caso tenha qualquer dúvida ou incerteza, fique à vontade para enviar um email
para tech@cumbuca.com pedindo esclarecimentos.
