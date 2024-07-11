# Desafio de Programação - Eng. Suporte
Primeiramente, agradecemos por seu interesse na Cumbuca. Somos uma fintech que busca ajudar as pessoas a cuidarem melhor das 
finanças coletivas, ajudando-as a realizarem sonhos e cuidar de quem mais importa para elas. No âmbito dessa missão, sempre
buscamos pessoas excepcionais para nossa equipe. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.

## Introdução

O reino de Cumbúquia perdeu os registros históricos de sua família real, e agora ninguém sabe mais a numeração
correta dos reis e rainhas do país. Sua tarefa, como o melhor programador de Cumbúquia, será desenvolver uma
**ferramenta de linha de comando** que irá resolver essa crise.

Claro, como você tem anos e anos de experiência, sabe que precisa fazer isso usando uma linguagem robusta e
expressiva, e por isso este desafio precisa ser resolvido em Elixir. Para ajudar você, preparamos um template
para criação de uma ferramenta de linha de comando em Elixir que pode ser consultado [neste link](https://github.com/appcumbuca/template_desafio_cli).

Sinta-se à vontade para clonar esse repositório e usá-lo como base.

## A ferramenta

A ferramenta de linha de comando que você irá desenvolver deve receber a lista dos reis e rainhas de Cumbúquia
em ordem e retornar os mesmos nomes, cada um com sua devida numeração.

Ao iniciar o binário, ele deve primeiro exibir uma breve explicação de seu uso. Ele irá então esperar o usuário
inserir uma lista de nomes. Os nomes serão inseridos um por linha, e a lista será considerada terminada quando
for lida uma linha em branco.

Após a lista ser finalizada, a ferramenta irá repetir os nomes inseridos, porém, os nomes serão acrescidos de um
número romano conforme necessário.

Por exemplo, se a lista for:

```
Eduardo
Maria
Daniel
Eduardo
```

A ferramenta deverá emitir a seguinte saída:

```
Eduardo I
Maria I
Daniel I
Eduardo II
``` 

Já se a lista for:

```
João
João
João
João
``` 

A saída deve ser:

```
João I
João II
João III
João IV
```

Ou seja, cada vez que um nome de um rei se repetir o algarismo romano que se segue ao
nome deve ser incrementado em 1 desde o nome anterior.

## Avaliação 

Seu desafio deve ser disponibilizado por meio de um repositório Git acessível
à equipe da Cumbuca. Caso não queira disponibilizá-lo publicamente, converse
conosco para combinarmos como podemos acessar seu código.

### Critérios de avaliação

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
Embora testes automatizados não sejam obrigatórios neste desafio, incluí-los será 
considerado um ponto em seu favor.

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
