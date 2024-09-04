# Desafio de Programação - Backend Pleno
Primeiramente, agradecemos por seu interesse na Cumbuca. Somos uma fintech que busca ajudar as pessoas a cuidarem melhor das 
finanças coletivas, ajudando-as a realizarem sonhos e cuidar de quem mais importa para elas. No âmbito dessa missão, sempre
buscamos pessoas excepcionais para nossa equipe. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.

## Introdução

Seu desafio será fazer um **banco de dados chave-valor** com **transações recursivas** usando 
a linguagem Elixir.

Isso significa que esse banco permitirá salvar valores sob chaves definidas e depois
recuperá-los e modificá-los.

Adicionalmente, o banco deverá oferecer a capacidade de entrar em um estado onde todas as operações
realizadas podem ser desfeitas ou aplicadas no banco.

Adicionalmente, deve ser possível criar "transação dentro de transação" - caso uma transação seja
aplicada sobre uma outra transação, o resultado de todas as operações da transação "interna" deve
ser adicionado ao estado da transação externa.

## Restrições

O desafio deve ser implementado utilizando a linguagem de programação Elixir.
Outras linguagens não serão aceitas.

O desafio deve ser implementado utilizando *apenas funções da biblioteca padrão do Elixir*.
Soluções que utilizem bibliotecas externas em sua implementação *não serão aceitas*.
O uso de bibliotecas externas é permitido *somente* para implementação de testes.

O desafio deve gerar um binário a ser executado no terminal ao executar o comando
`mix escript.build`. Disponibilizamos um template já configurado dessa forma 
[neste repositório](https://github.com/appcumbuca/template_desafio_cli).

Notar que a ferramente buildada por esse repositório se inicia executando a função
`DesafioCli.main/1`, que irá receber os argumentos de linha de comando como lista.

A ferramenta criada aqui não deve receber argumentos de linha de comando e deve ignorar
quaisquer argumentos passados.

## A ferramenta

O banco de dados deve ser implementado como uma ferramenta de linha de comando interativa.

Ao iniciar a ferramenta, deve aparecer apenas um prompt, como no exemplo abaixo:

```
> 
```

Você pode usar um prompt diferente, mas deve ficar claro que a ferramenta está pronta para
receber comandos.

## Chaves e valores

As chaves do banco devem ser strings. Ao passar uma chave para um comando que espere isso,
a chave é passada simplesmente escrevendo o seu valor - exceto caso a chave contenha espaços
em branco, caso no qual ela deve ser cercada de aspas simples. Chaves serão representadas da
mesma forma que valores do tipo string, com as mesmas restrições e o uso de aspas simples
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

## Observações

- O banco de dados implementado neste desafio não precisa ser persistente. Todavia, 
consideraremos como ponto positivo caso a persistência seja implementada. Ver a subseção
"Pontos adicionais" na seção de "Avaliação" abaixo.

- O banco deve ser fechado utilizando a combinação padrão de programas de terminal Ctrl+C.
Caso a persistência seja implementada, deve ser garantido que quaisquer valores definidos
no nível de transação 0 (ver a documentação do comando `BEGIN` abaixo) estejam persistidos
antes do programa ser fechado. 

- Valores em nível de transação 1 ou superior devem ser descartados ao fechar o banco.

## Comandos

Devem ser implementados os comandos abaixo a serem interpretados pela interface do banco.
Caso se tente invocar um comando que não seja um dos abaixo, deve ser emitido um erro apropriado.
Por exemplo:

```
> TRY
ERR "No command TRY"
```

Caso um comando seja chamado com sintaxe incorreta, deve também ser emitido um erro.

```
> SET x
ERR "SET <chave> <valor> - Syntax error"
```

Em linhas gerais, em situações inesperadas ou impossíveis do banco tratar, deve ser emitido
um `ERR` apropriado.


### SET <chave> <valor>

O comando `SET` deve definir o valor de uma chave. Caso a chave não exista, ela deve ser criada.
Caso a chave já existe, ela será sobreescrita. O comando deve retornar se a chave já existia e o
novo valor dela.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
> SET teste 1
FALSE 1
> SET teste 2
TRUE 2
```

### GET <chave>

O comando `GET` deve recuperar o valor de uma chave. Caso a chave não exista, deve ser retornado
o valor NIL. Caso a chave exista, deve ser retornado o valor armazenado nela.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
> GET teste
NIL
> SET teste 1
FALSE 1
> GET teste
1
```

### BEGIN

O comando `BEGIN` deve iniciar uma transação. Ele deve retornar o atual nível de transação -
i.e. quantas transações abertas existem. O banco se inicia no nível de transação 0.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
> GET teste
NIL
> BEGIN
1
> SET teste 1
FALSE 1
> GET teste
1
```

Transações recursivas:
```
> BEGIN
1
> BEGIN
2
```

### ROLLBACK

O comando `ROLLBACK` deve encerrar uma transação *sem aplicar suas alterações*. Isto é,
todas as alterações criadas na transação atual devem ser descartadas. Deve retornar o nível de
transação após o rollback.

O comando ROLLBACK deve emitir um erro caso usado no nível de transação 0.

**Exemplos**:

Supondo que a chave `teste` não exista no início da interação:
```
> GET teste
NIL
> BEGIN
1
> SET teste 1
FALSE 1
> GET teste
1
> ROLLBACK
0
> GET teste
NIL
```
Notar que após o rollback, as mudanças da transação em curso são descartadas.

Transações recursivas:
```
> GET teste
NIL
> BEGIN
1
> SET teste 1
FALSE 1
> GET teste
1
> BEGIN
2
> SET foo bar
FALSE foo
> SET bar baz
FALSE baz
> GET foo
bar
> GET bar
baz
> ROLLBACK
1
> GET foo
NIL
> GET bar
NIL
> GET teste
1
```
Notar que o rollback cancela apenas as alterações da transação que ele encerra. As alterações de
transações "abaixo" permanecem inafetadas.

### COMMIT

O comando `COMMIT` deve encerrar a transação atual *aplicando todas as suas alterações*. Isto é,
as alterações da transação atual devem ser inclusas nas alterações da transação inferior, ou,
caso após o `COMMIT` estejamos no nível de transação 0, as transações devem ser efetivadas no banco.
O comando `COMMIT` deve retornar o nível de transação após o commit.

**Exemplos**:

```
> GET teste
NIL
> BEGIN
1
> SET teste 1
FALSE 1
> GET teste
1
> COMMIT
0
> GET teste
1 
```

Transações recursivas:
```
> GET teste
NIL
> BEGIN
1
> SET teste 1
FALSE 1
> GET teste
1
> BEGIN
2
> SET foo bar
FALSE foo
> SET bar baz
FALSE baz
> GET foo
bar
> GET bar
baz
> COMMIT
1
> GET foo
bar
> GET bar
baz
> GET teste
1
> ROLLBACK
0
> GET teste
NIL
> GET foo
NIL
> GET bar
NIL
```

Notar que as alterações da transação no nível 2 foram inclusas na transação no nível 1,
e então foram canceladas junto à alteração introduzida no nível 1.

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

### Pontos adicionais
O banco de dados implementado neste desafio *não precisa ser persistente*.
Isto é, o banco pode ser implementado mantendo os valores apenas durante uma mesma
sessão de interação. Todavia, consideraremos como um ponto positivo na avaliação 
caso haja implementação de persistência entre sessões de interação. Sugerimos
fazer isso salvando o estado do banco em um arquivo.

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
