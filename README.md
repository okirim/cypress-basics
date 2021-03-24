# after installing cypress

## config cypress

#### in cypress.json

```
{
    "baseUrl":"http://localhost:3000"
}
```

#### in your package.json 
```
 "scripts": {
    "test": "cypress open"
  }
```
#### in your cypress/integration folder, create new file demo.js

for auto-completion add at the top of the file or install `npm i --save-dev @types/cypress`
```
/// <reference types="Cypress"/>

```

#### eslint config

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
#### run your first code

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
        //data attribute
        cy.get("[data-test='test-footer']")

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

#### click
```
describe("actions", () => {
    it("simulate click action", () => {
    cy.get('a').first().click();
    //or    
    cy.get("a[href*='cypress-tutorial']").click()
    })
    //click all button
    cy.get("button").click({multiple:true}); 
})
```
### right click and double click

```
describe("actions", () => {
    it("simulate right click and double click", () => {
        cy.get('button').first().rightclick();
        cy.get('button').last().dbclick();
})
```
#### type
```
describe("actions", () => {
    it("simulate type action", () => {
    cy.get("[name='email']").type('rand@gmail.com')
     //or
    cy.get("[name='email']").type('rand@gmail.com',{force:true});
    //submit the form
    cy.get("[type='submit']").click();

})
```
#### clear
```
describe("actions", () => {
    it("simulate clear action", () => {

    cy.get("[name='email']").clear()
})
```

#### select
```
describe("actions", () => {
    it("simulate select action", () => {
    //select the value
    cy.get('.lang-list').select('php');

      //select the text
      cy.get('.lang-list').select('PHP');
})
```
### checkbox and radio-button

```
describe("actions", () => {
    it("simulate select checkbox and radioButton", () => {
    //checkbox
    //check the value
    cy.get("[value='en']").check();
    
    //uncheck the value
    cy.get("[value='fr']").uncheck();

    //radio-button
     cy.get("[type='radio']").check();
     cy.get("[type='radio']").uncheck();
})
```
### focus and blur

```
describe("actions", () => {
    it("simulate focus and blur", () => {
    cy.get("[name='email']").focus()
    cy.get("[name='email']").blur()
})
```

### trigger (click, mouse events)
```
describe("actions", () => {
    it("simulate focus and blur", () => {
    //click    
    cy.get('button').first().trigger('click');

    // mouse events
    cy.get('button').first().trigger('mouseover');
    cy.get('button').first().trigger('mouseenter');
    cy.get('button').first().trigger('mousemove');
    cy.get('button').first().trigger('mousedown');
    cy.get('button').first().trigger('mouseout');
    cy.get('button').first().trigger('mouseup');



})
```
