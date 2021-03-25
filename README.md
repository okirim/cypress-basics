# Basics

## config cypress

#### in cypress.json

```
{
    "baseUrl":"http//:localhost:3000"
}
```

#### in your package.json 
```
 "scripts": {
    "test": "cypress open"
  }
```
#### in your `cypress/integration` folder, create new javascript file `*.js`

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
    [//]: #(run before every 'test block')
})
before(() => {
    [//]: #(run before 'test block' once)
})
after(() => {
   [//]: #( run after 'test block' once)
})
afterAll(() => {
    [//]: #(run after all 'test block')
})
```
update our test file

```
 beforeAll(() => {
     cy.visit("/");
})
```
## selectors
```
 beforeAll(() => {
     cy.visit("/");
})
describe("selectors", () => {
    it("select html elements", () => {
    [//]: #(class)
        cy.get('.container');

    [//]: #(id)
        cy.get('#list');

    [//]: #(children)
        cy.get('#list > li');
        cy.get('#list').find('li');

    [//]: #(first child)
        cy.get('#list' > li).first();

    [//]: #(last child)
        cy.get('#list' > li).first();

    [//]: #(second child)
        cy.get('#list' > li).eq(1);

    [//]: #(input attribute)
        cy.get([name='email']);
    [//]: #(data attribute)
        cy.get("[data-test='test-footer']")

    [//]: #(siblings next)
        cy.get('.header').next();
        cy.get('.header').nextAll();
        cy.get('.header').nextUntil('footer');

    [//]: #(siblings prev)
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
    [//]: #(or)    
        cy.get("a[href*='cypress-tutorial']").click()
    [//]: #(click all button)
        cy.get("button").click({multiple:true}); 
    })
   
})
```
#### right click and double click

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
    [//]: #(or)
        cy.get("[name='email']").type('rand@gmail.com',{force:true});
    [//]: #(submit the form)
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
    [//]: #(select the value)
         cy.get('.lang-list').select('php');

    [//]: #(select the text)
         cy.get('.lang-list').select('PHP');
})
```
#### checkbox and radio-button

```
describe("actions", () => {
    it("simulate select checkbox and radioButton", () => {
    [//]: #(checkbox)
    [//]: #(check the value)
        cy.get("[value='en']").check();
    
    [//]: #(uncheck the value)
        cy.get("[value='fr']").uncheck();

    [//]: #(radio-button)
        cy.get("[type='radio']").check();
        cy.get("[type='radio']").uncheck();
})
```
#### focus and blur

```
describe("actions", () => {
    it("simulate focus and blur", () => {
       cy.get("[name='email']").focus()
       cy.get("[name='email']").blur()
})
```

#### trigger (click, mouse events)
```
describe("actions", () => {
    it("simulate focus and blur", () => {
    [//]: #(click)    
       cy.get('button').first().trigger('click');

    [//]: #( mouse events)
       cy.get('button').first().trigger('mouseover');
       cy.get('button').first().trigger('mouseenter');
       cy.get('button').first().trigger('mousemove');
       cy.get('button').first().trigger('mousedown');
       cy.get('button').first().trigger('mouseout');
       cy.get('button').first().trigger('mouseup');

})
```
## assertion
#### should('contain')
```
describe("assertions", () => {
    it("should contain", () => {
    cy.get('body').should('contain','Cypress tutorial');
})
```

#### should('have.text')
```
describe("assertions", () => {
    it("should have text", () => {
    [//]: #(this will fail)
        cy.get('body').should('have.text','Cypress tutorial');
    [//]: #(with (have.text) we should select the specific element that contain the text)  
       cy.get('.header > a').should('have.text','Cypress tutorial');
})
```
#### should('be.visible') and should('not.be.visible')
```
describe("assertions", () => {
    it("hidden and visible", () => {
    [//]: #(visible)
        cy.get('#visible').should('be.visible')
    [//]: #(hidden)   
        cy.get('#hidden').should('not.be.visible')
})
```
#### should('have.class')
```
describe("assertions", () => {
    it("have class", () => {
       cy.get('#list > li').should('have.class','list-item')
})
```
#### should('have.css')
```
describe("assertions", () => {
    it("have css", () => {
        cy.get('#hidden').should('have.css','display').and('eql','none');
})
```
#### should('be.enabled') and should('be.disabled')
```
describe("assertions", () => {
    it("have disabled attribute or not", () => {
     [//]: #(enabled element)    
        cy.get("[value='mercedes']").should('be.enabled');
    [//]: #(disabled element)  
        cy.get("[value='cz']").should('be.enabled');
})
```
#### should('have.attr')
```
describe("assertions", () => {
    it("have attribute", () => {
        cy.get('#img-1').should('have.attr','src').and('eql','img1.jpg');
})
```
#### should('have.value')
```
describe("assertions", () => {
    it("have value", () => {
        cy.get("[name='email']")type('kadiro@okirim.com').should('have.value','kadiro@okirim.com');
})
```