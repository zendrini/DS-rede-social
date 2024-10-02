## Você pode conhecer a biblioteca clicando no link abaixo ou adicionar esse trecho de código no seu index.html abaixo do seu arquivo CSS.   
```xml
  <script src="https://cdn.plot.ly/plotly-2.27.0.min.js" charset="utf-8"></script>
```

### [Link da biblioteca Plotly ](https://plotly.com/javascript/)

## Após adicionar a biblioteca de gráficos vamos capturar os dados de outra fonte externa então dentro da pasta já criada `graficos` crie mais um arquivo chamado: `quantidadeUsuarios.js`

## Depois, no arquivo `index.html`, vamos adicionar dentro do `<body>` mais um `script:module`, referenciando nosso novo arquivo pelo caminho `graficos/quantidadeUsuarios.js`.
```xml
<script type="module" src="graficos/quantidadeUsuarios.js"></script>
```

## No arquivo `quantidadeUsuarios.js`, faremos o mesmo feita anteriormente no arquivo `informacoesGlobais.js`.
```csharp
async function quantidadeUsuarios() {
  const url = 'https://raw.githubusercontent.com/guilhermeomrails/api/main/numero-usuarios.json'
  const res = await fetch(url)
  const dados = await res.json()
}

quantidadeUsuarios()
```

## Estruturando o gráfico

É importante saber que tipo de gráfico queremos gerar. Inicialmente, vamos gerar um gráfico de barras, onde teremos uma barra para cada rede social, definida pela quantidade em cada uma delas.

Primeiro vamos separar cada uma dessa informações dos dados entre chaves (  `keys`  ) e valores (  `values`  ).

No arquivo  `quantidadeUsuarios.js`, dentro da função, depois de  `const dados`, vamos criar uma nova variável  `const nomeDasRedes`  que recebe  `Object.keys(dados)`. Ou seja, essa variável conterá apenas os nomes das redes, que são as chaves (  `keys`  ).

Depois, vamos criar outra variável  `const quantidadeUsuarios`  que recebe  `Object.values(dados)`. Ou seja, nossa variável conterá apenas as quantidades de usuários de cada rede, que são nossos valores (  `values`  ).

```javascript
async function quantidadeUsuarios() {
  const url = 'https://raw.githubusercontent.com/guilhermeomrails/api/main/numero-usuarios.json'
  const res = await fetch(url)
  const dados = await res.json()
  const nomeDasRedes = Object.keys(dados)
  const quantidadeUsuarios = Object.values(dados)

}

quantidadeUsuarios()
```
Agora, vamos criar a estrutura do gráfico.

Teremos uma variável nomeada como  `const data`  ( data significa dado, informação), que receberá colchetes e chaves  `[{}]`.

Dentro das chaves, vamos inserir as informações (dados) que serão exibidas no gráfico. Ele terá um eixo  `x`  (  _horizontal_  ) e um eixo  `y`  (  _vertical_  ), além de um  `type`  (  _tipo_  ). Um gráfico sempre receberá essas três informações.

O eixo  `x`  vai receber  `nomeDasRedes`. O eixo  `y`  vai receber  `quantidadeUsuarios`. O  `type`  vai receber  `bar`, afinal, queremos criar um gráfico de barras.

```go
const data = [
  {
    x: nomeDasRedes,
    y: quantidadeUsuarios,
    type: 'bar'
  }
]
```
## Exibindo o gráfico

Para exibir esse gráfico, precisamos inseri-lo dentro da seção  `graficos-container`, que está no arquivo  `index.html`. Faremos isso diretamente pelo JavaScript.

Ainda no arquivo  `quantidadeUsuarios.js`, depois da  `const data`, vamos criar uma variável  `const grafico`  (no singular) que recebe  `document.createElement('div')`.

Logo depois, vamos criar uma classe de CSS para esse gráfico, com  `grafico.className = 'grafico'`.

```javascript
const grafico = document.createElement('div')
grafico.className = 'grafico'
document.getElementById('graficos-container').appendChild(grafico)
Plotly.newPlot(grafico, data)
```
Para acessar esse gráfico no HTML, em  `graficos-container`, podemos escrever  `document.getElementById('graficos-container')`, que é o local onde vamos gerar todos os gráficos, e adicionar  `.appendChild(grafico)`  para inserir o nosso novo gráfico.

Para finalizar, vamos pedir para o  `Plotly`  criar um novo gráfico, usando o método  `.newPlot()`  e passando como parâmetros a estrutura do gráfico e as informação que ele apresentará. Portanto:  `Plotly.newPlot(grafico, data)`.


## Unidade Ciência de dados: criando gráficos dinâmicos com JavaScript



Olá, estudante!

Nesta unidade, aprenderemos sobre Ciência de Dados utilizando JavaScript!

## O que vamos fazer?

Existem milhares de dados espalhados pelo mundo sobre diversos assuntos. Um desses assuntos são as redes sociais.

Já parou para pensar quantas pessoas utilizam redes sociais? Quais são as redes sociais com mais usuários no mundo?

Vamos explorar essas perguntas de forma prática, usando dados reais. Vamos coletar informações de uma API externa que traz dados globais das pessoas e transformar essas informações em um relatório visual incrível, com gráficos, números importantes, títulos, labels (etiquetas), descrições e muito mais. Faremos tudo isso do zero!

Observe como nosso projeto vai ficar:

![alt text: Captura de tela mostrando a página do projeto funcionando com o título “Relatório das redes sociais”. Na parte principal podemos ver gráficos em barra, da esquerda para direita, do maior para o menor, com as redes nessa ordem: “Facebook”, “Youtube”, “WhatsApp”, “Instagram”, “Tiktok”, “WeChat”.](http://cdn3.gnarususercontent.com.br/3614-ciencia-dados/Imagens/Ciencia%20de%20dados_1.1-FCF1.png)

Antes de começar a programar e escrever nosso relatório sobre redes sociais, vamos falar sobre o que é Data Science (Ciência de Dados).

## O que é e o que faz a Ciência de Dados?

Ciência de Dados é a análise de dados do passado e do presente para tomar decisões e ter ideias sobre o futuro.

Nosso projeto usará HTML, CSS e JavaScript para criar gráficos e textos.

Embora grande parte do mercado utilize Python para analisar dados, é possível fazer isso com outras linguagens como C#, por exemplo.

Após coletar dados de diferentes bancos de dados, analisar as informações e criar gráficos, a pessoa cientista de dados precisará ter muita curiosidade e criatividade para saber contar histórias. O nome técnico disso é Storytelling.

## Ciclo da Ciência de Dados

Na Ciência de Dados, sempre teremos uma questão, um problema, um desafio, algo que queremos validar. Para responder essa questão, obtemos dados, entendemos esses dados e elaboramos novas questões para, então, entender o mundo e o contexto em que estamos trabalhando.

![alt text: Fluxograma do ciclo da Ciência de Dados. Uma seta azul indica o caminho do fluxograma, começando por “Questão” e passando para “Obter os dados”. Depois, passando para “Entende os dados”, de onde três setas saem. Uma de volta para “Obter dados”, outra voltando para “Questão” e a última que vai para “Entende o mundo”, de onde pode voltar para “Questão”.](http://cdn3.gnarususercontent.com.br/3614-ciencia-dados/Imagens/Ciencia%20de%20dados_1.2-FCF1.png)

Depois que esse ciclo é finalizado, apresentamos um relatório das nossas conclusões, com soluções e decisões para o futuro.

## Nosso projeto

No desafio dessa unidade, vamos analisar as redes sociais. Vamos levantar algumas questões sobre o assunto para serem respondidas com dados:

-   **Quantas horas**, em média, as pessoas da sua escola passam nas redes sociais?
-   **Qual**  é a rede social mais usada pelas pessoas da sua sala? E pela sua família? e Pelo mundo?
-   **Quando**  as pessoas acessam as redes sociais como, Instagram, TikTok ou Facebook, qual é seu  **principal objetivo**? O que elas fazem?

Pensando nisso, vamos criar dois tipos de relatório. O primeiro será com base no mundo. Tendo acesso a um banco de dados sobre o uso de redes sociais no mundo, vamos tentar dizer algo como:

> No mundo, as pessoas passam em média X horas por dia conectadas nas redes sociais. A rede social mais usada por elas é Y. Quando elas acessam as redes sociais, geralmente procuram fazer W e Z.

Já temos, então, as questões. Na sequência, nosso objetivo é obter esses dados, entender como eles se relacionam e levantar novas questões ou entender o contexto e validar nossas respostas, pensando:

> Será que o mundo, nossa escola e a nossa sala se comportam da mesma forma quando o assunto é rede social?

Vamos descobrir!

 
