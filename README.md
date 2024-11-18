# Chat em Tempo Real

Este projeto é um chat em tempo real, desenvolvido com as tecnologias **Vue.js**, **Vuetify**, **Vite**, **Socket.io**, **SCSS**, **Node.js** e **Nodemon**. O chat permite que múltiplos usuários enviem e recebam mensagens instantaneamente, com suporte para múltiplas salas de chat, onde os usuários podem entrar em diversas salas para se comunicar de forma organizada.

## Funcionalidades

- **Mensagens em tempo real**: Usuários podem enviar e receber mensagens instantaneamente.
- **Salas de chat**: Usuários podem entrar em diferentes salas para conversar em grupos separados.
- **Lista de mensagens**: Exibe todas as mensagens enviadas dentro da sala de chat.
- **Identificação de usuários**: Usuários podem se identificar ao entrar no chat.
- **Notificações de novos membros**: Usuários são notificados quando novos membros entram ou saem das salas.
- **Interface responsiva**: A interface do chat se adapta a diferentes tamanhos de tela.
- **Sistema de entrada/saída de salas**: Usuários podem se juntar a várias salas de chat e sair delas conforme necessário.

## Tecnologias Utilizadas

- **Vue.js**: Framework para a construção de interfaces de usuário interativas.
- **Vuetify**: Biblioteca de componentes de interface do usuário baseada no Material Design para Vue.js.
- **Vite**: Ferramenta de build para projetos Vue.js, que oferece rápido carregamento e compilação.
- **SCSS**: Pré-processador CSS para criar folhas de estilo de forma mais eficiente e modular.
- **Node.js**: Ambiente de execução JavaScript no servidor.
- **Express**: Framework para aplicações web em Node.js.
- **Socket.io**: Biblioteca para comunicação em tempo real entre cliente e servidor.
- **Nodemon**: Ferramenta para reiniciar automaticamente o servidor durante o desenvolvimento.

## Estrutura do Projeto

O projeto está dividido em duas pastas principais:

- **client**: Contém a aplicação frontend, construída com Vue.js e Vuetify.
- **server**: Contém o servidor backend, onde o Node.js e o Socket.io são configurados.

## Pré-requisitos

Antes de começar, você precisará ter o **Node.js** instalado em sua máquina. Você pode baixá-lo em [nodejs.org](https://nodejs.org/).

## Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/gabrielbotandev/vue-chat.git
```

### 2. Instale as dependências

Acesse as duas pastas do projeto e instale as dependências separadamente:

- **Para o servidor**:

  ```bash
  cd server
  npm install
  ```

- **Para o cliente**:

  ```bash
  cd client
  npm install
  ```

### 3. Rodando o projeto

- **Para rodar o servidor em modo de desenvolvimento**:

  Dentro da pasta **server**, execute:

  ```bash
  npm run dev
  ```

- **Para rodar o frontend em modo de desenvolvimento**:

  Dentro da pasta **client**, execute:

  ```bash
  npm run dev
  ```

### 4. Acesse a aplicação

Abra o seu navegador e acesse `http://localhost:3000`. Você verá a interface do chat em tempo real onde pode entrar em diferentes salas e interagir com outros usuários.

## Uso

1. Acesse o chat no navegador através de `http://localhost:3000`.
2. Entre em uma sala de chat.
3. Envie mensagens que serão instantaneamente exibidas para todos os participantes da sala.
4. Adicione novos usuários e visualize notificações quando alguém entrar ou sair da sala.

## Contribuições

Sinta-se à vontade para contribuir com melhorias ou correções. Faça um fork deste repositório, crie suas mudanças e envie um pull request!
