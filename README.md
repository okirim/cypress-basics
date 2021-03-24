# after installing cypress

## config cypress

### in cypress.json

```
{
    "baseUrl":"http://localhost:3000"
}
```

### in your package.json 
```
 "scripts": {
    "test": "cypress open"
  }
```
### in your cypress/integration folder, create new file demo.js

for auto-completion add at the top of the file or install `npm i --save-dev @types/cypress`
```
/// <reference types="Cypress"/>

```

### eslint config

install eslint plugin for cypress `npm install eslint-plugin-cypress --save-dev`

create .eslintrc.json file and add :

```
{
    "plugins": ["cypress"],
    "env":{
        "cypress/globals":true
    },
    "extends":[
        "plugin:cypress/recommended"
    ]
}
```
### run your first code

in your demo.js file
```
describe("launch the browser", () => {
    it("our first test", () => {
         cy.visit("/");
    })
})
```
run `npm test`

## hooks 

```
 beforeAll(() => {
    //run before every block
})
before(() => {
    //run before once
})
after(() => {
   // run after once
})
afterAll(() => {
    //run after all
})
```
update our file demo.js

```
 beforeAll(() => {
     cy.visit("/");
})
```
## selectors
```
/// <reference types="Cypress"/>
 beforeAll(() => {
     cy.visit("/");
})
describe("selectors", () => {
    it("select html elements", () => {
        //class
        cy.get('.container');
        //id
        cy.get('#list');
        //children
        cy.get('#list > li');
        cy.get('#list').find('li');
        //first child
        cy.get('#list' > li).first();
        //last child
        cy.get('#list' > li).first();
         //second child
        cy.get('#list' > li).eq(1);
        //input attribute
        cy.get([name='email']);
        //siblings next
        cy.get('.header').next();
        cy.get('.header').nextAll();
        cy.get('.header').nextUntil('footer');
         //siblings prev
        cy.get('footer').prev();
        cy.get('footer').prevAll();
        cy.get('footer').prevUntil('footer');

    })
})
```
## actions

```
describe("actions", () => {
    it("simulate actions", () => {
    cy.get('a').first().click();
    //or    
    cy.get(a[href*='cypress-tutorial']).click()
    })
})
```