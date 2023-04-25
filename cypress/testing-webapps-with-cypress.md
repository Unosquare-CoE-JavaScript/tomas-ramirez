# Cypress

## Configuration
After installing Cypress, you need to configure it to work with your application. Cypress uses a configuration file
named cypress.json that should be located in the root of your project.

```json
{
  "baseUrl": "http://localhost:3000",
  "viewportWidth": 1280,
  "viewportHeight": 720,
  "testRunner": "mocha"
}
```

## Writing Tests

To write tests with Cypress, you can create a new file in the cypress/integration directory. Cypress supports several
testing frameworks

```js
describe('My App', () => {
    it('should load the home page', () => {
        cy.visit('/')
        cy.get('h1').should('contain', 'Welcome to My App')
    })

    it('should allow users to login', () => {
        cy.visit('/login')
        cy.get('input[type="email"]').type('user@example.com')
        cy.get('input[type="password"]').type('password')
        cy.get('button[type="submit"]').click()
        cy.url().should('eq', 'http://localhost:3000/dashboard')
    })
})
```

Cypress provides a set of commands that you can use to interact with your application, such as cy.visit, cy.get,
cy.type, cy.click, and cy.url.

## Running Tests

To run tests with Cypress, you can use the Cypress Test Runner. You can start the Test Runner by running the following
command in your terminal:


```

npx cypress open

yarn cypress open
``` 

This command will launch the Test Runner, which allows you to select which tests to run and see the results.

You can also run tests in headless mode by running the following command:

```
npx cypress run
yarn cypress run

```

This command will run all your tests in the background and generate a report of the results.

## Aliases

### Defining Aliases

To define an Alias in Cypress, you can use the Cypress.Commands.add() method. This method allows you to define a custom
command that can be used in your tests.

This is how we define an Alias that selects a specific element:

```js
Cypress.Commands.add('selectButton', () => {
    return cy.get('button[type="submit"]')
})
```

This Alias defines a custom command named selectButton that returns a Cypress command to select a button element with a
type attribute of submit.

You can also define an Alias that selects multiple elements, like this:

```js
Cypress.Commands.add('selectInputs', () => {
    return cy.get('input')
})
```

### Using Aliases

To use an Alias in your tests, you can call the custom command you defined using the cy object.

For example, to use the selectButton Alias we defined earlier, you can call it like this:

```js
cy.selectButton().click()
```


Similarly, and in order to use the selectInputs Alias we defined earlier, you can call it like this:

```js
cy.selectInputs().type('Hello, world!')
```

## Complex inputs

Cypress provides a number of useful methods to work with complex inputs such as dropdowns, radio buttons, checkboxes,
range sliders, lists, etc

### Range Sliders

To interact with a range slider using Cypress, you can use the invoke() method to set the value of the slider. Here's an
example of how to set the value of a range slider:

```js
cy.get('input[type="range"]').invoke('val', 50).trigger('input')
```

### Select Lists

To interact with a select list using Cypress, you can use the select() method. Here's an example of how to select an
option from a select list:

```js
cy.get('select').select('Option 1')
```

If the select list has an empty option as the first option, you can select it using the select() method and passing an
empty string as the argument, like this:

```js
cy.get('select').select('')
``` 

## Programmatically generated tests

Cypress allows you to programmatically generate tests using JavaScript. This can be useful if you have a large number of
test cases to write, or if you want to generate tests dynamically based on data from an API or database.

### Generating Tests

To programmatically generate tests in Cypress, you can use the Cypress.Commands.add() method to create a custom command.
This command can then be used to generate tests dynamically.

```js
Cypress.Commands.add('generateTest', (name, url) => {
    it(`should load ${name}`, () => {
        cy.visit(url)
        cy.get('h1').should('contain', name)
    })
})

const pages = [
    {name: 'Home', url: '/'},
    {name: 'About', url: '/about'},
    {name: 'Contact', url: '/contact'}
]

pages.forEach((page) => {
    cy.generateTest(page.name, page.url)
})
```

## Form Validations

Form validation is an important part of any web application. It ensures that user input is accurate, consistent, and
meets specific requirements. Cypress provides a simple and effective way to test form validation in your web
application.

### Writing Form Validation Tests

To test form validation in Cypress, you can use the cy.get() method to select the form elements you want to test. You
can then use the cy.type() method to enter data into the form fields.

```js
describe('Form Validation', () => {
    beforeEach(() => {
        cy.visit('/form')
    })

    it('should display error message for invalid email', () => {
        cy.get('#email').type('invalid_email')
        cy.get('#submit').click()
        cy.get('#email-error').should('be.visible')
    })

    it('should display error message for empty password', () => {
        cy.get('#password').type(' ')
        cy.get('#submit').click()
        cy.get('#password-error').should('be.visible')
    })

    it('should display success message for valid form', () => {
        cy.get('#email').type('valid_email@example.com')
        cy.get('#password').type('password123')
        cy.get('#submit').click()
        cy.get('#success').should('be.visible')
    })
})
``` 

This code tests a form with two input fields (#email and #password) and a submit button (#submit).

The first test checks that an error message is displayed when an invalid email is entered. It does this by entering "
invalid_email" into the email field, clicking the submit button, and checking that the error message with the ID
#email-error is visible.

The second test checks that an error message is displayed when the password field is left empty. It does this by
entering a single space into the password field, clicking the submit button, and checking that the error message with
the ID #password-error is visible.

The third test checks that a success message is displayed when a valid email and password are entered. It does this by
entering a valid email and password into the respective fields, clicking the submit button, and checking that the
success message with the ID #success is visible.

## Network Requests & Sessions

### Making Network Requests

Cypress provides a simple way to make network requests and assert on their responses. You can use the cy.request()
method to make a network request and assert on its response.


```js
describe('Network Request', () => {
    it('should make a successful GET request', () => {
        cy.request('GET', 'https://jsonplaceholder.typicode.com/posts/1')
            .its('body')
            .should('have.property', 'title', 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit')
    })
})
```

This code tests a GET request to the URL fakeapi.com/id The test asserts that the
response has a property named title with the value 'sunt aut facere repellat provident occaecati excepturi optio
reprehenderit'.

### Maintaining User Sessions

Cypress also provides a way to maintain user sessions across multiple tests. You can use the cy.setCookie() method to
set a cookie for the current domain.

```js
describe('Session', () => {
    it('should maintain user session', () => {
        cy.setCookie('session_id', '12345')
        cy.visit('/')
        cy.get('#username').should('have.value', 'Tom')
    })
})
``` 

We just set a  a cookie named session_id with the value '12345'. It then visits the root URL / and asserts that an input
field with the ID #username has the value 'Tom'.

### Mocking

Cypress provides a simple way to mock external dependencies in your web application tests. You can use the cy.route()
method to mock network requests and responses.

```js
describe('Mocking', () => {
    it('should mock external dependencies', () => {
        cy.route('GET', 'https://jsonplaceholder.typicode.com/posts/1', {
            title: 'mocked title'
        })
        cy.visit('/')
        cy.get('#title').should('have.text', 'mocked title')
    })
})
```

This code mocks a GET request to the URL fakeapi.com/id It sets the response to an object
with a title property that has the value 'mocked title'. It then visits the root URL / and asserts that an element with
the ID #title has the text 'mocked title'.

### Cypress Studio

Cypress Studio is a visual editor that allows you to create and modify Cypress test scripts without writing any code. It
provides a simple and intuitive interface for recording interactions with your application and generating test scripts.

- Open Cypress Studio by running the following command in your terminal:

``` 
npx cypress open-ct
```

- Click the "Record Test" button.

- Interact with your application to record a test script.

- Save the test script and run it using Cypress.

Cypress Studio is a great tool for creating and modifying test scripts quickly and easily. However, it's important to
note that it's not always possible to record all interactions with your application using Cypress Studio. In some cases,
you may need to write custom test scripts using the Cypress API.

## Continuous Integration

Cypress provides a way to automate testing using continuous integration tools like Travis CI or CircleCI. You can use
the cypress run command to run your tests in a headless browser environment.

Here's an example of how to use Cypress with Continuous Integration:

```yaml

language: node_js
node_js:

  - 12
    cache:
    directories:
      - ~/.npm
      - ~/.cache
        install:
  - npm ci
    script:
  - npm run build
  - npm run test:ci
    This code sets up a Travis CI job that installs dependencies using npm ci, builds the project using npm run build, and
    runs the tests using npm run test:ci. The test:ci script uses the cypress run command to run the tests in a headless
    browser environment.
  ```

Continuous Integration is a great way to ensure that your tests are always passing and that your application is working
as expected. By integrating Cypress with your Continuous Integration tool of choice, you can ensure that your tests are
run automatically and that any failures are caught as soon as possible.
