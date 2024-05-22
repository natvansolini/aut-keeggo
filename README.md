# aut-keeggo

# Automação de Login e Compra de Produto com Cypress

Este projeto é uma automação de teste que realiza o login e a compra de um produto em um site utilizando o framework de testes Cypress. O objetivo é garantir que o fluxo de login e compra esteja funcionando corretamente.

## Requisitos

- Node.js (versão 12 ou superior)
- npm (gerenciador de pacotes do Node.js)
- Cypress (instalado via npm)

## Instalação

1. Clone o repositório:

   ```sh
   git clone https://github.com/seu-usuario/seu-repositorio.git
   ```

2. Navegue até o diretório do projeto:

   ```sh
   cd seu-repositorio
   ```

3. Instale as dependências:

   ```sh
   npm install
   ```

## Estrutura do Projeto

A estrutura do projeto é a seguinte:

```
/cypress
  /fixtures
    - example.json
  /integration
    - login.spec.js
    - purchase.spec.js
  /plugins
    - index.js
  /support
    - commands.js
    - index.js
cypress.json
package.json
README.md
```

- `fixtures/`: Contém arquivos JSON com dados de exemplo para os testes.
- `integration/`: Contém os arquivos de teste.
  - `login.spec.js`: Testes relacionados ao login.
  - `purchase.spec.js`: Testes relacionados à compra de produtos.
- `plugins/`: Arquivos de configuração e extensões do Cypress.
- `support/`: Comandos customizados e configurações globais.

## Configuração

Atualize o arquivo `cypress.json` com a URL base do site que será testado:

```json
{
  "baseUrl": "https://www.exemplo.com"
}
```

## Comandos Customizados

No arquivo `support/commands.js`, você pode definir comandos customizados para simplificar os testes. Exemplo:

```js
Cypress.Commands.add('login', (email, password) => {
  cy.visit('/login');
  cy.get('input[name=email]').type(email);
  cy.get('input[name=password]').type(password);
  cy.get('button[type=submit]').click();
});

Cypress.Commands.add('purchaseProduct', (productName) => {
  cy.visit('/products');
  cy.contains(productName).click();
  cy.get('button.add-to-cart').click();
  cy.get('a[href="/checkout"]').click();
  cy.get('button[type=submit]').click();
});
```

## Testes

### Login

O arquivo `login.spec.js` contém testes para o fluxo de login:

```js
describe('Login', () => {
  it('deve fazer login com sucesso', () => {
    cy.login('usuario@exemplo.com', 'senha123');
    cy.url().should('include', '/dashboard');
    cy.contains('Bem-vindo').should('be.visible');
  });

  it('deve falhar ao fazer login com credenciais inválidas', () => {
    cy.login('usuario@exemplo.com', 'senhaerrada');
    cy.contains('Credenciais inválidas').should('be.visible');
  });
});
```

### Compra de Produto

O arquivo `purchase.spec.js` contém testes para o fluxo de compra de um produto:

```js
describe('Compra de Produto', () => {
  beforeEach(() => {
    cy.login('usuario@exemplo.com', 'senha123');
  });

  it('deve adicionar um produto ao carrinho e finalizar a compra', () => {
    cy.purchaseProduct('Nome do Produto');
    cy.url().should('include', '/confirmation');
    cy.contains('Compra realizada com sucesso').should('be.visible');
  });
});
```

## Executando os Testes

Para executar os testes em modo interativo:

```sh
npx cypress open
```

Para executar os testes em modo headless:

```sh
npx cypress run
```

## Contribuição

Sinta-se à vontade para contribuir com este projeto. Você pode abrir uma issue ou enviar um pull request com melhorias e correções.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

---

Este readme fornece uma visão geral do projeto de automação de login e compra de produto utilizando Cypress, incluindo a instalação, configuração e execução dos testes.
