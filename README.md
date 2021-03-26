# A- Basics

## install 
 install Cypress
 `npm install cypress - - save- dev && npx cypress open`

## 1- Config cypress

#### in cypress.json

```
{
    "baseUrl":"http//:localhost:3000"
}
```

#### in your cypress.json 

```
 "scripts": {
    "test": "cypress open"
  }
```
#### in your `cypress/integration` folder, create new javascript file `*.js`

for auto- completion add at the top of the file or install `npm i - - save- dev @types/cypress`
```
/// <reference types="Cypress"/>

```

#### eslint config

install eslint plugin for cypress `npm install eslint- plugin- cypress - - save- dev`

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

## 2- hooks 

```
 beforeAll(() => {
    // (run before every 'test block')
})
before(() => {
    // (run before 'test block' once)
})
after(() => {
   // ( run after 'test block' once)
})
afterAll(() => {
    // (run after all 'test block')
})
```
update our test file

```
 beforeAll(() => {
     cy.visit("/");
})
```
## 3- Selectors

```
 beforeAll(() => {
     cy.visit("/");
})
describe("selectors", () => {
    it("select html elements", () => {
    // (class)
        cy.get('.container');

    // (id)
        cy.get('#list');

    // (children)
        cy.get('#list > li');
        cy.get('#list').find('li');

    // (first child)
        cy.get('#list' > li).first();

    // (last child)
        cy.get('#list' > li).first();

    // (second child)
        cy.get('#list' > li).eq(1);

    // (input attribute)
        cy.get([name='email']);
    // (data attribute)
        cy.get("[data- test='test- footer']")

    // (siblings next)
        cy.get('.header').next();
        cy.get('.header').nextAll();
        cy.get('.header').nextUntil('footer');

    // (siblings prev)
        cy.get('footer').prev();
        cy.get('footer').prevAll();
        cy.get('footer').prevUntil('footer');

    })
})
```
## 4- Actions

#### click

```
describe("actions", () => {
    it("simulate click action", () => {
        cy.get('a').first().click();
    // (or)    
        cy.get("a[href*='cypress- tutorial']").click()
    // (click all button)
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
    // (or)
        cy.get("[name='email']").type('rand@gmail.com',{force:true});
    // (submit the form)
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
    // (select the value)
         cy.get('.lang- list').select('php');

    // (select the text)
         cy.get('.lang- list').select('PHP');
})
```
#### checkbox and radio- button

```
describe("actions", () => {
    it("simulate select checkbox and radioButton", () => {
    // (checkbox)
    // (check the value)
        cy.get("[value='en']").check();
    
    // (uncheck the value)
        cy.get("[value='fr']").uncheck();

    // (radio- button)
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
    // (click)    
       cy.get('button').first().trigger('click');

    // ( mouse events)
       cy.get('button').first().trigger('mouseover');
       cy.get('button').first().trigger('mouseenter');
       cy.get('button').first().trigger('mousemove');
       cy.get('button').first().trigger('mousedown');
       cy.get('button').first().trigger('mouseout');
       cy.get('button').first().trigger('mouseup');

})
```
## 5- Assertions

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
    // (this will fail)
        cy.get('body').should('have.text','Cypress tutorial');
    // (with (have.text) we should select the specific element that contain the text)  
       cy.get('.header > a').should('have.text','Cypress tutorial');
})
```
#### should('be.visible') and should('not.be.visible')

```
describe("assertions", () => {
    it("hidden and visible", () => {
    // (visible)
        cy.get('#visible').should('be.visible')
    // (hidden)   
        cy.get('#hidden').should('not.be.visible')
})
```
#### should('have.class')

```
describe("assertions", () => {
    it("have class", () => {
       cy.get('#list > li').should('have.class','list- item')
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
     // (enabled element)    
        cy.get("[value='mercedes']").should('be.enabled');
    // (disabled element)  
        cy.get("[value='cz']").should('be.enabled');
})
```
#### should('have.attr')

```
describe("assertions", () => {
    it("have attribute", () => {
        cy.get('#img- 1').should('have.attr','src').and('eql','img1.jpg');
})
```
#### should('have.value')

```
describe("assertions", () => {
    it("have value", () => {
        cy.get("[name='email']")type('kadiro@okirim.com').should('have.value','kadiro@okirim.com');
})
```

## 6- Commands

#### url()

```
describe("commands", () => {
    it("get url", () => {
        cy.url().should('contain','index.html');
})
```
#### title()

```
describe("commands", () => {
    it("get title", () => {
        cy.title().should('eql','cypress');
})
```
#### go()

```
describe("commands", () => {
    it("navigate", () => {

        cy.get('[href="/home.html"]').click();
        cy.title().should('eql','home');

        cy.go('back');
        cy.title().should('eql','cypress');

        cy.go('forward');
        cy.title().should('eql','home');
})
```
#### Cookie

```
describe("commands", () => {
    it("handle cookies", () => {
    // (get cookie created in index.html) 
        cy.getCookie('username').should('have.property','value','John Doe')

    // (set cookie, we use have property to access the cookie value because is returned as an object)
        cy.setCookie('currentUser','okirim').should('have.property','value','okirim');

    // (get cookies) 
        cy.getCookies().should('have.length',2);
})
})
```
#### clock()

```
describe("commands", () => {
    it("handle cookies", () => {
      // (to test your website in a specific time)
         const data=new Date(2020,04,10);
         cy.clock(date);
         cy.visit(/'home.html');
})
})
```
#### wrap()

```
describe("commands", () => {
    it("wrap data", () => {
        const user={
            name:'okirim',
            age:27,
            country:'Algeria'
        }
    // (we can not do that)

        user.should('have.property','name','okirim');
         
    // (we have to wrap it before doing any assertion)

        cy.wrap(user).should('have.property','name','okirim');    
     
})
})
```
#### invoke()

```
describe("commands", () => {

   it('invoke jquery command',()=>{
    //we use invoke to import jquery method text()
       cy.get('h1').invoke('text') 
   }) 
     
})
})
```
#### then()

```
describe("commands", () => {

   it('then commands access the selected element as argument',()=>{
    //we use invoke to import jquery method text()
       cy.url().then(url=>{
           cy.log(url);
       })
    //we can also use Jquery command in the returned element
       cy.get('button').first().then(element=>{
           element.click();
       })    
   }) 
     
})
})
```
#### expect()  [docs](https://www.chaijs.com/api/bdd/)

```
describe("commands", () => {

   it('expect command',()=>{

    expect(function () {}).to.not.throw();

    expect({a: 1}).to.not.have.property('b');

    expect([1, 2]).to.be.an('array').that.does.not.include(3);

   }) 
     
})
})
```
#### each()

```
describe("commands", () => {

   it('each command take a function',()=>{
    
    cy.get('button').each(el=>{
        el.click()
    })
   }) 
})
})
```
## 7- Async and Sync 

#### Async

```
describe('asynchronous',()=>{
    it('cypress command is async',()=>{
        cy.visit('/home.html');// action 1
        cy.url(); //action 2
    })
})
```
#### Sync

```
describe('synchronous',()=>{
    it('external command are not async',()=>{
        let $url;
        cy.visit('/home.html');
        cy.url().then(url=>{
            let $url=url;
        });
        console.log($url);//this will return undefined

        // we should do it like this 
        cy.visit('/home.html');
        cy.url().then(url=>{
            let $url=url;
            console.log($url);
        });
    })
})
```

## 8- Variables

#### create variable

```
describe('variables',()=>{
    it('create homePageUrl variable',()=>{
        cy.visit('/home.html');
        cy.url().as('homePageUrl'); 
        
        // we use @ before the name of the variable to access it
        cy.get('@homePageUrl');

    })

     it('access the homePageUrl variables',()=>{
        
        // we can not access homePageUrl in other block
        cy.get('@homePageUrl');//error
    })
})
```
#### access the variable from our blocks

```
describe('variables',()=>{
    beforeEach(()=>{
        cy.visit('/home.html');
        cy.url().as('homePageUrl'); 
    })
    it('access the  homePageUrl variable (first block)',function(){
     
        // we use this to access variable
        cy.get(this.homePageUrl);

    })

     it('access the homePageUrl variables (second block)',function(){
        
        // we use this to access variable
        cy.get(this.homePageUrl);

    })
})
```
## 9- fixtures

##### to access the data in Cypress (json, csv, html, text, jpg, png, jpeg, jpg, tif, gif) 


create `car.json` file and add :
`
{
    "brand":"BMW",
    "name":"X5"
}
`
we place our `car.json` file in the fixtures folder and access it like this :

```
describe('access file',()=>{
    it('cypress command is async',()=>{
        cy.fixture('car').then(car=>{
            cy.log(car.name)
        })
    })
})
```
[//]: # (we can change the fixtures folder)

`in pour Cypress.json file`

`
{
    "baseUrl":"http//:localhost:3000",
    "fixturesFolder":"cypress/RandomName"
}
`

#### read and write file
```
describe('read and write',()=>{
    it('read file',()=>{
        cy.readFile('filePath/filename.txt')
    })
     it('write file',()=>{
       cy.writeFile('filePath/filename.txt','hello world !')
    })
})
```
## 10- Api Request

#### GET

```
describe("GET REQUEST", () => {
  it("GET REQUEST ALL TODOS", () => {
    cy.request("GET", "https://jsonplaceholder.typicode.com/todos").then(
      (res) => {
        cy.log(res.body);
      }
    );
  });
    // BY DEFAULT THE METHOD = GET

     it("GET ALL TODOS", () => {
       cy.request("https://jsonplaceholder.typicode.com/todos").then(
         (res) => {
           cy.log(res.body);
         }
       );
     });
    
    
  it("GET SINGLE TODO", () => {
    cy.request("https://jsonplaceholder.typicode.com/todos/1").then((res) => {
      cy.log(res.body);
    });
  });
      it("GET All COMMENTS WHERE postId=1", () => {
        cy.request("https://jsonplaceholder.typicode.com/comments?postId=1").then((res) => {
          cy.log(res.body);
        });
      });
    
       //or
    
       it("GET All COMMENTS WHERE postId=1", () => {
         cy.request({
           url: "https://jsonplaceholder.typicode.com/comments",
           method: "GET",
           qs: {
             postId: 1,
           },
         }).then((res) => {
           cy.log(res.body);
         });
       });
});

```
#### POST

```
describe("POST REQUEST", () => {
    it('create new post', () => {
        cy.request('POST', "https://jsonplaceholder.typicode.com/posts" , {
           "userId": 1,
           "id": 999,
           "title": "PHP FRAMEWORK",
           "body":"LARAVEL IS THE BEST PHP..........."
        }).then(res => {
            expect(res.status).to.equal(201);
      });
  })
});
```
#### PUT AND PATCH

```
describe("PUT AND PATCH REQUEST", () => {
  it("PUT : update post with id=17", () => {
    cy.request("PUT", "https://jsonplaceholder.typicode.com/posts/17", {
      title: "HOW TO USE...."
    }).then((res) => {
      expect(res.status).to.equal(200);
    });
  });
  it("PATCH : update post with id=11", () => {
    cy.request("PATCH", "https://jsonplaceholder.typicode.com/posts/11", {
      title: "HOW TO USE...."
    }).then((res) => {
      expect(res.status).to.equal(200);
    });
  });
});
```
#### DELETE

```
describe("DELETE REQUEST", () => {
  it("delete post with id=17", () => {
    cy.request("DELETE", "https://jsonplaceholder.typicode.com/posts/17").then((res) => {
      expect(res.status).to.equal(200);
    });
  });
});
```
#### SECURE API

```
describe("GET REQUEST", () => {
  it("GET REQUEST : unAuthorized url", () => {
    cy.request("https://random-url",{
        'auth': {
           'bearer': 'token'
          }
    }).then((res) => {

      expect(res.status).to.equal(200);
    });
  });
});
```