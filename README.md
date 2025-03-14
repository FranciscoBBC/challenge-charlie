# <img src="https://avatars1.githubusercontent.com/u/7063040?v=4&s=200.jpg" alt="HU" width="24" /> Desafio Charlie

## Sumário

-   [Demonstração da aplicação em produção](#Demo-da-Aplicação)
-   [Requisitos para rodar o projeto](#Requisitos-Para-Rodar-o-Projeto)
-   [Instalação das dependencias](#Instalação-das-Dependências)
-   [Executar o projeto](#Executar-o-Projeto)
-   [Processo de desenvolvimento](#Processo-de-Desenvolvimento)
-   [Mudanças no layout](#Mudanças-no-Layout)
-   [Problemas encontrados](#Problemas-Encontrados)

---

## Demo da Aplicação

A build de produção está rodando na netlify no link:

[https://thirsty-roentgen-8cfd09.netlify.app](https://thirsty-roentgen-8cfd09.netlify.app)

---

## Requisitos Para Rodar o Projeto

-   [Node](https://nodejs.org/)
-   [Yarn](https://yarnpkg.com/)
-   [Docker(opcional)](https://www.docker.com)

---

## Instalação das Dependências

### Clone o repositório

```
$ git clone git@github.com:FranciscoBBC/challenge-charlie.git
```

### Instale as dependências

Se você optar por rodar o projeto com docker, por favor utilize **yarn**

```
$ yarn
```

ou

```
$ npm install
```

---

## Executar o Projeto

Você pode executar o projeto de duas formas:

### Rodando localmente

Se você optar por rodar o projeto localmente utilize o comando abaixo:

```
$ yarn start
```

ou

```
$ npm run start
```

A aplicação estará disponível no endereço [http://localhost:3000](http://localhost:3000)

### Utilizando docker

Foram criados stages para produção e desenvolvimento.

-   Para criar a imagem e rodar o stage de desenvolvimento basta utilizar o comando abaixo e

    ```
    $ yarn dev
    ```

    Sua aplicação vai estar disponível em [http://localhost:3000](http://localhost:3000)

-   Para gerar a imagem de produção basta rodar o comando abaixo:

    ```
    $ yarn build:docker
    ```

    Em seguida utilize o comando abaixo para ver a versão de produção da aplicação

    ```
    $ yarn prod
    ```

    Sua aplicação vai estar disponível em [http://localhost](http://localhost)

---

## Processo de Desenvolvimento

### Framework e bibliotecas utilizadas:

Utilizei o React atravez do _create-react-app_ como base da minha aplicação. Hoje trabalho e sou bastante familiarizado com o _Next Js_ também, mas como não especificava ele no escopo do desafio e pela simplicidade do projeto, acabei optando pelo react puro mesmo.

Para os estililos optei pelo [styled-components](https://styled-components) por conta da facilidade de trabalhar os módulos de estilos e tema global.

Tive problema para baixar o pacote de ícones que foi solicitado no projeto e para contornar o problema, utilizei a lib [react-icons](https://react-icons.github.io/react-icons) e tentei importar os ícones mais parecidos possíveis dos requisitados no projeto.

Nos 🔬testes utilizei o _Jest_ integrado com a 🐙 [testing-library](https://testing-library.com) para realizar os testes nos componentes. Dentro de cada página é possível visualizar o teste (_componente_.test.tsx) e snapshot gerado.

Também habilitei o coverage mas se você baixou o projeto agora só vai conseguir visualizar utilizando comando:

```
$ yarn test
```

Também criei outro comando para ficar testando os componentes durante o desenvolvimento.

```
$ yarn test:watch
```

Para melhorar a qualidade do código utilizei o 🐶[husky](https://github.com/typicode/husky) junto com [lint-staged](https://github.com/okonet/lint-staged). A configuração do husky pode ser vista em _./.husky_ e a do lint staged dentro do _package.json_. Lá adicionei o comando para corrigir falhas de estilo de código com o _eslint_, forçar formatação com o _prettier_ e passar a bateria de testes com o _jest_.

---

## Mudanças no Layout

Não fiz grandes mudanças visuais na aplicação, apenas ajustei as fontes para visualização mobile e deixei a escala cinza somente enquanto o usuário não habilita a localização, se ele negar deixei como padrão o centro da cidade do Rio de Janeiro.

Quando o usuário digita uma cidade que não é encontrada pelo openCage o input fica com a borda avermelhada e as informações de temperatura somem.

Também adicionei as informações da localização do usuário nos cookies por 30 minutos para não precisar ficar consultando a api do openCage a todo momento, quando o cache reseta voltam as informações do centro do Rio de Janeiro.

A imagem de fundo também fica salva nos cookies por 2 horas, para que da próxima vez que o usuário acesse o link não haja troca da cor de fundo padrão para a imagem, ajudando a melhorar consequentemente o SEO.

---

## Problemas Encontrados

Além do problema com o pacote de ícones que mencionei acima, tive um problema em pegar a imagem de fundo da api do bing. Requests vindos de aplicações que rodam no browser estão tendo problema de cors como mencionado nessa [issue](https://github.com/hurbcom/challenge-charlie/issues/29) do próprio desafio. Como é descrito que faz parte do teste, inicialmente utilizei esse [proxy](https://github.com/Rob--W/cors-anywhere) para conseguir pegar a imagem, porêm é preciso habilitar esse serviço diariamente. Para contornar isso, criei uma api bem simples que retorna apenas essa imagem. O código pode ser visto aqui [https://github.com/FranciscoBBC/fran-bing-proxy](https://github.com/FranciscoBBC/fran-bing-proxy), ela está rodando no heroku e o link para viasualizar o retorno da api é [esse](https://fran-bing-proxy.herokuapp.com).
