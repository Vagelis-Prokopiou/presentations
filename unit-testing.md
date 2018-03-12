# Unit testing

## What is a unit test?

It is the test on a “unit of work” (usually a function) that provides verification that a known, fixed input produces a known, fixed output.

## What are the benefits of unit testing?
* Unit tests find bugs early.
* Unit tests significantly reduces production bugs.
* Unit tests make complex code easy to understand.
* Unit tests provide dependant documentation for the code base.
* Unit tests save development time (less time spend on bug hunting).
* Unit tests make easier (even possible in some cases) to change and refactor code.
* Unit tests remove the fear of changing/breaking the codebase.
* Ultimately unit test prevent the “rotting” of the codebase.

## Examples of unit testing.
`const add = function(int1, int2) {return int1 + int2; }`
```javascript
const add = function(int1, int2)
{
    return int1 + int2;
}
```
```javascript
describe('#add', function ()
{
    test('should correctly add two integers', function ()
    {
        tests = [
            {int1: 1, int2: 1, expected: 2}
            , {int1: 100, int2: 1, expected: 101}
        ];

        tests.forEach(function (test)
        {
            expect(add(test.int1, test.int2)).toBe(test.expected);
        });
    });

    test('should throw exception if invalid parameter is passed', function ()
    {
        tests = [
            {int1: null, int2: 1}
            , {int1: undefined, int2: 1}
            , {int1: false, int2: 1}
        ];

        tests.forEach(function (test)
        {
            expect(function() { add(test.int1, test.int2); }).toThrowError('Invalid parameter');
        });
    });
});
```

## Assignment.
* Difficult: Create a `dateToTimestamp` function, which accepts an ISO date, returns the Unix timestamp, throws exception if date is invalid. Hint: You can use the `moment(date).format('X')` method of the `moment.js` library.
* Easy: Create a calulator object with `add`, `delete`, `multiply`, `divide` methods, and provide a test for each method.

## Requirements.
* [Node.js](https://nodejs.org/en/download/)
* Git Bash (https://git-scm.com/downloads)
For both of them, you can download the portable binaries and place them in a `bin` folder at the root of your user's folder. Example: `C:\Users\Vangelisp\bin`.