Cmd + Opt + K => Chrome javascript console
star wars api new domain
https://swapi.dev
# REACT TESTING
## JEST AND JEST-DOM ASSERTIONS
The assertions will determine if the test pass or fail, they are essential part of the test.
The expect() method that’s global in Jest, the argument this is what your assertion is assorting against; Jest will
examine and see if that element meet the expectations.

.toBeInTheDocument() this is matcher this is what the assertion match is. The matcher in this case “toBeInTheDocument()” 
comes from Jest-DOM and sometimes there is an argument in the matcher.

We can find several assertions at https://github.com/testing-library/jest-dom
when using some of these matchers, you may need to make sure you use a query function (like queryByTestId) 
rather than a get function (like getByTestId). 
Otherwise the get(--) function could throw an error before your assertion.

` test('uses jest-dom', () => {
document.body.innerHTML = 
<span data-testid="not-empty"><span data-testid="empty"></span></span>
<div data-testid="visible">Visible Example</div>

expect(screen.queryByTestId('not-empty')).not.toBeEmptyDOMElement()
expect(screen.getByText('Visible Example')).toBeVisible()
}) `

## JEST WATCH

The Jest watch plugin system provides a way to hook into specific parts of Jest and to define watch mode menu prompts 
that execute code on key press. Combined, these features allow you to develop interactive experiences custom for your workflow

## TDD

This helps to avoid duplication of code as we write a small amount of code at a time in order to pass tests. 
(Tests are nothing but requirement conditions that we need to test to fulfill them).

Test-Driven development is a process of developing and running automated test before actual development of the application.
Hence, TDD sometimes also called as Test First Development.

## REACT TESTNG  LIBRARY

The React Testing Library is a very light-weight solution for testing React components. 
It provides light utility functions on top of react-dom and react-dom/test-utils, in a way that encourages better testing practices. 
Its primary guiding principle is:

The more your tests resemble the way your software is used, the more confidence they can give you.

So rather than dealing with instances of rendered React components, your tests will work with actual DOM nodes. 
The utilities this library provides facilitate querying the DOM in the same way the user would. Finding form elements by their label text (just like a user would),
finding links and buttons from their text (like a user would). It also exposes a recommended way to find elements by a data-testid as an "escape hatch" for elements
where the text content and label do not make sense or is not practical.

This library encourages your applications to be more accessible and allows you to get your tests closer to using your 
components the way a user will, which allows your tests to give you more confidence that your application will work when 
a real user uses it.

This library is a replacement for Enzyme. While you can follow these guidelines using Enzyme itself, enforcing this is 
harder because of all the extra utilities that Enzyme provides (utilities which facilitate testing implementation details).

## FUNCTIONAL TESTING VS UNIT TESTING
### FUNCTIONAL TESTING

Functional Testing is carried out to ensure that the application’s overall functionality meets the business requirements.
Functional Testing tests the basic functionality of the application. It checks if the application runs as per the business 
requirements. You need to read and understand the operational requirements of an app before you begin writing the Functional test cases and testing the application.
Unit Testing is performed on every individual element of an application to ensure that the element works as expected.

### UNIT TESTING

Unit Testing is testing individual elements of an application. Each element, like a text box, button, and text display, 
is tested to check if it performs the expected actions. These individual elements are called ‘Units’ which gave rise to the term Unit Testing. 
It is run on even the smallest element in an app.

These elements are individually and independently tested for issues. It cannot be conducted on components that connect to an external entity. 
For example, Unit Tests cannot be undertaken on elements that connect to an external database, network, or file.
These tests are conducted right from the beginning of the development phase.

## TDD VS BDD
### TDD
This helps to avoid duplication of code as we write a small amount of code at a time in order to pass tests.
(Tests are nothing but requirement conditions that we need to test to fulfill them).

Test-Driven development is a process of developing and running automated test before actual development of the application.
Hence, TDD sometimes also called as Test First Development

Benefits of TDD
Reduces the amount of time required for rework
Explores bugs or errors very quickly
Faster feedback
Encourages the development of cleaner and better designs
Enhances the productivity of the programmer
Allows any team member to start working on the code without a specific team member. This encourages knowledge-sharing and collaboration.
It gives the programmer confidence to change an application’s large architecture quickly.
Results in the creation of extensive code that is flexible and easy to maintain

### BDD
(BDD) is a testing approach derived from the Test-Driven Development (TDD) methodology. In BDD, tests are mainly based on systems behavior.
This approach defines various ways to develop a feature based on its behavior. In most cases, 
the Given-When-Then approach is used for writing test cases. Let’s take an example for a better understanding of TDD vs BDD:

Key benefits of BDD
Helps reach a wider audience through the usage of non-technical language
Focuses on how the system should behave from the customer’s and the developer’s perspective
BDD is a cost-effective technique
Reduces efforts needed to verify any post-deployment defects}


Given the user has entered valid login credentials
When a user clicks on the login button
Then display the successful validation message
As shown above, the behavior is illustrated in a very simple English language, also known as a shared language. 
This helps everyone in the team responsible for development to understand the feature behavior.

## TEST BEHAVIOUR WHEN CLICKING 
We first need to find or query, somehow get the element we want to click/interact with
Then fireEvent.click(the element we queried)
after that you can use any kind of assertions you expect after that click action

This is only one form to "Fake interaction" when testing.
## INITIAL CONDITIONS 
We can check initial conditions for those interactive components
For example a button has a "disabled" property, and a checkbox a "checked" property
For fully testing our apps we want to test both initial conditions and after some actions conditions
With "common" properties like the button enabled property we can use the .toBeEnabled assertion. and in general .toBe...

### FIRE EVENT VS USER EVENT 
When we are testing our goal is to test every case that we may find using our application
The main difference between uservent and fireEvent is that userEvent allows us to simulate
complete interactions and not only single isolated events. 
The best example would be the event sequence case
for example we can test the click action burt also the hover that a real user would see
just before clicking a button

So, if you are testing a very specific event you would choose fireEvent
otherwise you would always want to use userEvent
