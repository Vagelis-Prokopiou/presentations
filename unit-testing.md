# Testing (unit testing)

## Types of testing
1. Unit testing.
2. Integration testing (a.k.a acceptance/end to end testing).
3. Performance testing.

## What is a unit test?

It is the test on a “unit of work” (usually a function) that provides verification that a known, fixed input produces a known, fixed output.

## What are the benefits of unit testing?
1. Unit tests find bugs early.
2. Unit tests significantly reduce production bugs.
3. Unit tests make complex code easy to understand.
4. Unit tests provide dependant documentation for the codebase.
5. Unit tests save development time (less time spent on bug hunting).
6. Unit tests make easier (even possible in some cases) to change and refactor the code.
7. Unit tests create better APIs.
8. Unit tests remove the fear of changing/breaking the codebase.
9. Unit tests prevent the “rotting” of the codebase.

## What are the negative aspects of unit testing?
Most people say it is the time needed to write the tests.

Experience shows that writing tests reduces the overall time needed to reach production.

## What is the recipe for good unit tests?

No secret recipe.
1. Writing testable code.
2. Write tests first.

## Examples of testable code.
### Bad
```javascript
// Bad
function emailClients(clients)
{
  clients.forEach(function(client)
  {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive())
    {
      email(client);
    }
  });
}
```

### Good
```javascript
// Good.
function emailActiveClients(clients)
{
  clients
    .filter(isActiveClient)
    .forEach(email);
}

function isActiveClient(client)
{
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

## Examples of unit testing.

### Test suite structure
```javascript
describe('suiteName', function()
{
    test('testDescription', function()
    {
        expect(expectation).toBe(expectedResult);
    });
});
```

```javascript
// Example 1, involving pure functions:

const add = function(int1, int2) { return int1 + int2; }

describe('#add', function ()
{
    test('should correctly add two integers', function ()
    {
        expect(add(1, 1)).toBe(2);
        expect(add(-1, 1)).toBe(0);
        expect(add(1.9, 0.1)).toBe(2);
    });

    test('should throw exception if invalid parameter is passed', function ()
    {
        expect(function() { add(null, 1); }).toThrowError('Invalid parameter');
        expect(function() { add(undefined, 1); }).toThrowError('Invalid parameter');
        expect(function() { add(false, 1); }).toThrowError('Invalid parameter');
    });
});
```
```javascript
// Example 2, involving DOM manipulation (needs Karma.js):

describe('#resetElementValue(domSelector)', function()
{
    beforeEach(function()
    {
        const fixture = '<div id="fixture">' +
            '<input type="hidden" id="packageID" name="packageID" value="1e-eru6">' +
            '<input type="hidden" id="covers" name="covers" value="1,3,5">' +
            '<input type="hidden" id="covers_extra" name="covers_extra" value="1,2">' +
            '</div>';

        $('body').append(fixture);
    });

    afterEach(function()
    {
        $('#fixture').remove();
    });

    test('should reset (set to empty string) the value of the provided selector', function()
    {
        resetElementValue('#packageID');
        resetElementValue('#covers');
        resetElementValue('#covers_extra');
        expect($('#packageID').val()).toBe('');
        expect($('#covers').val()).toBe('');
        expect($('#covers_extra').val()).toBe('');
    });
});
```

## Assignment.
* Difficult: Create a `dateToTimestamp(date)` function, which accepts an ISO 8601 date, returns the Unix timestamp, throws exception if date is invalid. Hint: You can use the `moment(date).format('X')` method of the `moment.js` library.
* Easy: Create a Calculator with `add`, `substract`, `multiply`, `divide` methods, and provide a test for each method.

Use [Jest](https://facebook.github.io/jest/docs/en/getting-started.html) as the testing framework.

## Requirements.
* [Node.js](https://nodejs.org/en/download/)
* [Git Bash](https://git-scm.com/downloads)

For both of them, you can download the portable binaries and place them in a `bin` folder at the root of your user's folder. Example: `C:\Users\Vangelisp\bin`.

Presentation URL: http://slides.com/vagelis_prokopiou/deck#/

PS: The Calculator:
```javascript
const Calculator = {
    add: function(int1, int2) { return int1 + int2; },
    delete: function(int1, int2) { return int1 - int2; },
    multiply: function(int1, int2) { return int1 * int2; },
    divide: function(int1, int2) { return int1 / int2; }
};
```
