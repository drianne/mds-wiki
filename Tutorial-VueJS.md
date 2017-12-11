# Introdução

<p align="justify"> Vue JS é um framework javascript voltado para a construção de interfaces de usuário, sendo utilizável também em SPA's (Single Page Applications). Ao utilizá-lo é possível ter acesso aos conceitos dos frameworks reativos como data bind, two way, events e criação de componentes. O mais importante nesse caso é entender de uma maneira clara como se dá o uso de componentes.</p>

# Estrutura básica

<p align="justify">A estrutura básica do Vue JS gira em torno do uso de componentes em que cada componente apresenta um template, uma área de script e uma tag style, por meio dos quais é possível utilizar html, javascript e CSS, respectivamente (de maneira exemplificada). Nesse modelo, é praticável o uso de vue JS nas áreas de Html e javascript por meio do qual é estabelecido o conceito de data-bind. No que diz respeito ao javascript criam-se as funções normalmente e por meio de vue js no html atualiza-se de maneira dinâmica o valor dos dados para o que é apresentado ao usuário.</p>


# Componentes

<p align="justify">Como foi dito anteriormente, o conceito de componente é bastante forte com relação ao vueJS, isso por que é uma abstração que torna possível a construção de aplicações de larga escala de maneira modularizada, com pequenos componentes reutilizáveis. Nesse sentido, essa estrutura se comporta como uma árvore, como pode ser observado na figura abaixo: </p>

![](http://i63.tinypic.com/2iqgzee.png)


Um exemplo de uma estrutura básica de componente encontra-se a seguir :

![](http://i64.tinypic.com/f2rhn6.png)

# Instância Vue

Uma aplicação Vue é uma instância Vue raiz, criada com new Vue, conforme representação abaixo. Além disso, todos os componentes são também instâncias.

![](http://i65.tinypic.com/t02dq8.png)

## Dados e métodos

Ao criar uma instância Vue, as propriedades do objeto data passam a fazer parte do sistema de reatividade, de modo que quando um dado se altera, a camada visual re-renderiza. Abaixo há um exemplo de data.

data: {
  name: '',
  idade: 0
}

## Ciclo de Vida da Instância

É importante para a dinâmica de componentes saber que as instâncias Vue passam por várias etapas na inicialização por meio das quais são invocados gatilhos do ciclo de vida, que traz controle ao desenvolvedor o suficiente para realizar execução de lógicas personalizadas em determinadas etapas. Todas as fases podem ser observadas no diagrama abaixo.

![](http://i64.tinypic.com/2hgd8gz.png)

Se pegarmos um gatilho, como por exemplo, o created vemos que o código atribuido à ele será executado assim que a instância for criada. Sua declaração se dá da seguinte maneira, a ser utilizado na região de javascript :

created() {
  exampleMethod();
}

# Sintaxe de Templates

A sintaxe de templates do vue js, como dito anteriormente é baseada em HTML e há diversas formas de utilizá-la. Com texto, por exemplo, consegue-se utilizar o data binding através das chaves, conforme exemplo:

![](http://i68.tinypic.com/168zxi1.png)

Em que msg é uma variável utilizada na seção script do component, por exemplo.

![](http://i63.tinypic.com/iw3n7a.png)

Como exemplificado acima, a diretiva v-once utiliza o valor mas não torna-o reativo. Em casos de atributos HTML utiliza-se a diretiva v-bind:

![](http://i63.tinypic.com/ruo0gk.png)

## Diretivas

Tem como objetivo realizar alguma ação quando um valor é modificado (ex: v-if, v-else, v-else-if, v-for).

![](http://i66.tinypic.com/53pztl.png)

Algumas diretivas, entretanto, aceitam parâmetros, como por exemplo, o v-bind, utilizada para atualizar um atributo HTML de maneira reativa. Exemplos:

![](http://i65.tinypic.com/23w348g.png)
![](http://i63.tinypic.com/mn2u09.png)

# Dados Computados

Os templates contidos nos componentes devem ser simples, a partir do momento que começa a possuir muita lógica embutida, surge a necessidade de utilizar dados computados. Estes funcionam como dados definidos no data. Exemplo :

![](http://i68.tinypic.com/14tx4iu.png)

# Renderização Condicional e de Listas

É possível utilizar no html uma condição para que uma determinada informação apareça ou não, nesse sentido, existe a tag v-if, v-else-if e v-else, cuja sintaxe básica  é a seguinte :

![](http://i63.tinypic.com/t816ah.png)

É possível ainda iterar sobre uma lista utilizando o Vue, por meio do qual, obtém-se:

![](http://i65.tinypic.com/qntmqq.png)

Sendo que object é uma lista.

# Comunicação entre componentes

Um dos pontos mais importantes a serem observados é a maneira como os componentes se comunicam entre si. De maneira geral, numa estrutura de árvore, como demonstrado anteriormente, há uma hierarquia em que um componente pode ser considerado "filho" de outro. Nesse sentido, às vezes torna-se necessário passar dados entre os componentes e isso depende do seu parentesco na hierarquia. De pai para filho a informação é passada por meio de propriedades ou 'props', enquanto que se a troca for inversa, de filho para pai, é necessário utilizar eventos. Em caso de utilização de props, tem-se que o componente filho declara uma props cujo nome pode ser utilizado livremente pelo template, como observado no exemplo abaixo :

![](http://i68.tinypic.com/16j0axk.png
  )
Nesse caso, o componente pai deve passar como atributo da tag que chama o componente filho, como expresso a seguir:

![](http://i65.tinypic.com/2aklgkx.png)

Para se comunicar de filho para pai, entretanto, utiliza-se de eventos, uma vez que todas as instâncias do Vue implementam uma interface de eventos personalizada. Para escutar um evento, utiliza-se $on, para emitir $emit(), para propagar um evento para cima da cadeia utiliza-se $dispatch() e para baixo, sobre os descendentes, $broadcast(). Um exemplo dessa dinâmica encontra-se no código a seguir :

No componente filho :

![](http://i65.tinypic.com/2j2alid.png)

  No componente pai :

![](http://i65.tinypic.com/20t5b0j.png)

## Referências

[The Progressive JavaScript Framework](https://vuejs.org/v2/guide/)
