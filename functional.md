# Functional Programming

#### Declarative Approach

**Pure** functions are easier to test.

### Pure function

Output depends only on input (no side-effects)

```
let port: number = 8081;

const portToString = (port: number) => `PORT: ${port.toString()}`;
console.log(portToString(port));
```

### Functional code is stateless 
Immutable data

## First order function 
Function that takes a value and returns another (to mutate data = new data)

```
const appendPM = (val: number) => val.toString() + ' PM';
console.log(appendPM(1));
```

## Higher order function

Function that takes function as an argument or returns a function itself

### Functions as arguments

```
const startTimes: number[] = [1, 3, 5];
console.log(startTimes.map(appendPM));
```

### Functions as return value

```
const appendColor = (fixed:string) => (dynamic:string) => fixed + dynamic;
const white = appendColor('white');
const black = appendColor('black');

console.log(white('knight'));
console.log(white('bishop'));
```
