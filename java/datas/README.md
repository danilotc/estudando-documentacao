# Ler documentação habilidade importante para Devs

Quando comecei na área de tecnologia perguntava aos meus professores o que eu deveria estudar para programar, a resposta foi unanime, diziam "Estude lógica de programação". Recomendação seguida, já que havia (e ainda há) bastante conteúdo sobre isso.

Depois comecei a ter outro tipo de recomendação que era "ler a documentação". Na realidade eu percebi a importância disso, mas como estudá-la? Até hoje não tive ninguém que fizesse isso, estou tendo que aprender sozinho, como a maioria de nós, né?

Eu pensei é simplesmente pegar e ler? Percebi que não é simples assim! Por isso, escrevo este artigo para compartilhar a forma como eu exploro a documentação quando estou estudando Java, espero que sirva como um start inicial com alguns caminhos que você pode seguir.

Portanto, acomode-se, pegue aquele cafezinho e vamos entender algumas coisas juntos.

## A classe Calendar

Uma forma de estudar a documentação é dentro da própria IDE durante o desenvolvimento do código ou da leitura de algum. Neste caso, vou usar a classe Calendar para mostrar algumas coisas.

A primeira característica que achei estranho nesta classe e que ainda não havia aprendido foi que ela não é instanciada com **new**, para isso seria necessário usar alguns métodos, neste caso, o método **getInstance**.

![img01_calendar](https://user-images.githubusercontent.com/36853209/231048276-538d6506-bb34-4715-a8ce-5bcd4ec4212b.png)

A linha 9 está criando uma instância de Calendar e atribuindo seu retorno a uma variável do tipo Calendar. Mas onde está o `new` que é usado para criar instâncias de objetos?

Para sanar esta dúvida fiz o seguinte: mantendo a tecla Ctrl pressionada clique no nome da classe `Calendar`, com isso a IDE me levou até a implementação do código desta classe.

![img01_calendar2](https://user-images.githubusercontent.com/36853209/231049969-6ee6bdb2-11e1-4f60-9696-10b99ae79802.png)

Observei que esta é uma classe abstrata, por isso não é possível criar uma instância dela usando esta palavra-chave. Ah! Por isso não tem new.

```java
public abstract class Calendar implements Serializable, Cloneable, Comparable<Calendar> {
    // implementacao ocultada
}
```

Essa é a informação que sana minha dúvida sobre instância, devo criar instancia daquela forma porque a classe Calendar está definida como abstrata.

Segundo as regras da Orientação a Objetos classes abstratas não podem ser instanciadas, então ela deve possuir algum método que faz isso e o Calendar possui alguns, usei o método `getInstance`.

## Como o método getInstance está definido?

Toda classe que é definida como abstrata não pode ser instanciada, logo algum de seus métodos precisam fazer isso e este deve ser definido como estático, por isso o método `getInstance` é estático. Ele é o método que cria e retorna uma instância de Calendar, por ser estático podemos usá-lo para criar a instância a partir da própria classe. Mais uma dúvida sanada! =)

![img04_impl_metodo_getInstance](https://user-images.githubusercontent.com/36853209/231050442-154f6a04-c2ce-44f0-b6ee-7d5e55fc8508.png)

Observe o comentário de documentação que explica algumas coisas sobre o método, daqui a pouco falarei sobre ele, mas só de ler este comentário já é possível saber o que ele faz.

Assim, entendemos que este método _“Obtém um calendário usando a zona e localização padrão”_. Opa, já é possível entender algumas coisas sem mesmo sair da IDE, legal né?

Além disso, podemos observar também que antes de retornar a instância de Calendar existe outras dependências que estão sendo utilizadas, tais como:

* a chamada do método `getDefault` da classe `Locale`.
* o uso de outro método estático que irá criar o calendário com o time zone parão.

É só seguir esses mesmos passos para analisar mais profundamente cada uma dessas chamadas e tentar sanar todas as dúvidas que surgirem, por exemplo, por que o método `createCalendar` recebe esses dois parâmetros? De onde eles vem? O que eles fazem? E por ai vai… tente sanar cada dúvida indo atrás delas, basicamente essa é a técnica.

## A documentação online

Agora você já sabe como analisar a implementação das classes, lendo os comentários é possível entender o que cada parte da implementação faz, suas dependências e retornos, tudo isso sem mesmo sair da IDE.

Agora gostaria de mostrar como fazer essa mesma análise na API online disponibilizada pela Oracle, que é a mantenedora do Java.

Abra seu navegador e pesquise “java calendar api” ou uma variação dela. Você terá alguns retornos como este, por exemplo.

![img4_calendar_api7-2](https://user-images.githubusercontent.com/36853209/231019207-2971c9c1-e49f-4eb2-aea4-20e5cf87c368.jpg)

Clicando neste resultado você será direcionado para a API do Java 7 falando sobre a classe `Calendar`. De cara podemos ver que ela implementa algumas interfaces, também percebemo isso quando usamos `Crtl+Clique` na classe, lembra?

![img4_calendar_api7-3](https://user-images.githubusercontent.com/36853209/231019467-5de5e01f-e874-460a-bdf7-3f9268c2f0e6.jpg)

O problema nesse tipo de pesquisa é que eu pesquisei diretamente a classe no navegador, mas terei que depender sempre do sistema de busca do navegador? Não, essas informações são da API do Java, ela possui uma interface onde todos os códigos estão centralizados, faça a mesma pesquisa porém com as seguintes palavras ou variação "java api" e veja o resultado.

![img5_calendar_api7](https://user-images.githubusercontent.com/36853209/231019604-8b39ff9c-38c8-4411-be6e-c956233105cd.jpg)

Esta é a interface da API do Java na versão 7, contudo é sempre recomendado utilizar uma versão conhecida como LTS (Long Term Support) que é o período de suporte que a Oracle se propõe a fornecer para cada versão LTS lançada. Por isso, recomendo começar acessando a LTS mínima do Java que é a versão 8, para isso, apenas mude o número 7 para 8 na URL.

https://docs.oracle.com/javase/7/docs/api

https://docs.oracle.com/javase/8/docs/api

![temp2](https://user-images.githubusercontent.com/36853209/231019779-d48a26dc-4b49-48a0-bd10-57847e937d59.jpg)

Saiba que essa API é extremamente grande, por isso é importante saber o que buscar nela, ou seja, o que você quer saber, estudar ou se aprofundar em relação ao Java? Sendo ainda mais específico, qual classe ou método você quer analisar? De qual pacote? É bom saber antes de começar a navegar.

Sabendo o que buscar veja como essa interface está dividida, são três partes:

1. Mostra a lista de todos os pacotes do Java (`java.util`, `java.sql`, `java.io`, etc), o que você procura está em qual pacote?
2. Mostra a lista de todas as classes, ao selecionar um pacote, todas as classes daquele pacote serão listadas aqui, basta procurar aquela que você quer estudar.
3. Mostra todas as informações referentes a classe que você estava buscando, incluindo métodos, explicações, dependências, se está implementando ou estendendo alguma outra classe ou interface. Agora é só ler, normalmente essa página constuma ser bem grande, portanto tente filtrar novamente o que está procurando... só não esqueça que agora você está analisando tudo que está dentro daquela classe, neste caso, a classe `Calendar`.

![img04_api7_pesquisa](https://user-images.githubusercontent.com/36853209/231054623-69b00beb-b2a8-49f1-9011-2298a362cdb6.png)

É assim que você pode pesquisar e estudar a API do Java, mesmo sendo uma versão oficial e LTS navegar por esta API é complicado, além de ser mais demorado porque você precisa achar o pacote na área 1, depois procurar a classe na área 2 para então começar a estudar sua implementação na área 3, é possível e recomendo que faça isso, mas existe uma forma mais fácil e atualizada de pesquisar, vou mostrar daqui a pouco.

Por ora, seguindo as instruções apresentadas acima encontrei o método que eu queria analisar, o `getInstance`, consigo ver que ele é estático igual vimos lá na IDE. Falando nisso lembra daquele comentário que encontramos no código lá no começo? Então, olha ele aqui nos falando que este método _“Obtém um calendário usando a zona e localização padrão”._ 

![temp3](https://user-images.githubusercontent.com/36853209/231019972-93831fc9-f59b-43d9-a65c-ff3aae1f204d.jpg)

Clicando em `getInstance()` você será levado para uma outra área com mais informações sobre o método, tudo na mesma página. Se você é uma pessoa detalhista e observadora, deve estar se perguntando _“onde está o trecho do segundo parágrafo?”._

![img04_api8_pesquisa_getInstance2](https://user-images.githubusercontent.com/36853209/231057540-333f8773-4200-4b9d-902e-1aa903eca4c2.png)

Parabéns, realmente havia um segundo parágrafo no comentário do código quando analisamos sem sair da IDE, lembra? Então, essa foi uma informação adicionada a partir da versão 17 do Java. Cada versão lançada eles melhoram códigos e adicionam comentários...

A partir da versão 11 do Java eu só precisei digitar `getInstance` no campo `search` da API e ela trouxe aquela mesma área vista na imagem anterior. A busca foi infinitamente mais rápida, por isso pesquisar na API recente (11+) é mais fácil e rápido. E olha o segundo parágrafo ali, ele apareceu no código porque estou usando a versão 17, por isso houve essa diferença na pesquisa, pra você que é detalhista. ;)

> DICA: quando for estudar a documentação veja qual versão você está usando e tente pesquissar a mesma versão na documentação, além disso, considerando a API mais recente (11+) você tem a mesma facilidade da IDE para achar o que precisa, veja.

Quando estamos escrevendo código a prórpia IDE nos ajuda mostrando os métodos disponíveis que podem ser chamados, conforme a imagem abaixo. Ela mostra que dentro da classe `Calendar` há 3 métodos com mesmo nome (sobrecarregados) que podemos usar para criar uma instância.

![img04_ide_getInstance](https://user-images.githubusercontent.com/36853209/231058502-b766bca7-ed05-4f97-8f1e-c2c56edf3a36.png)

Agora acesse uma API mais recente (11+) e digite a mesma coisa no único campo de busca que existe lá, digite, `calendar.getinstance` e veja o resultado... é bem legal! Ela te dá as mesmas opções que a IDE fornece quando você está escrevendo código. Beleza, então qual a diferença?

1. Na IDE você está recebendo ajuda de um sistema que autocompleta seu código durante a escrita, a ferramenta tem isso por padrão, por isso fica aparecendo aquelas janelinhas quando está escrevendo.
2. Na documentação (API online) clicando em um dos resultados da pesquisa você será levado até a página com todas as informações sobre aquilo que você pesquisou, seja classe, método, interface, a lista é enorme.

![img05_api17_search_getInstance](https://user-images.githubusercontent.com/36853209/231058855-1233a172-b461-4fb5-9f8b-a0d97c806ad4.png)

Por isso, quando acessar a API do Java 11 ou superior a interface não estará mais dividida com frames (do html), ela estará atualizada com um sistema robusto de busca, por isso basta digitar o que você está buscando entender no java e ele irá retornar algumas opções, escolha aquela que atende a sua pesquisa.

![img05_api17_search](https://user-images.githubusercontent.com/36853209/231060460-259ae1c7-2801-4337-bf25-93c4f9bf97a1.png)


É realmente muita coisa e eu nem organizei do jeito que gostaria por falta de recursos, contudo espero que este artigo possa te ajudar a entender algumas formas de estudar a documentação do Java e encontrar informações em seu sistema robusto de busca... eu aprendo bastante coisa usando essas técnicas de estudo.

E você, conhece alguma outra forma de estudar a documentação? Por favor compartilhe, gostaria muito de aprender.

Bons estudo! 