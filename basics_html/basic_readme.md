

### Dynamically update DOM

```javascript
const newParagraph = document.createElement('p');
newParagraph.textContent = 'Another comment';
document.getElementById('root').append(newParagraph);
```

### Understand different concepts
1. Let , const and var
2. arrow functions
3. array destructuring
4. object destructuring
5. String literals



## Understand const
#### const is immutable
```javascript
const greet = "hello world";
greet = "somethingelse"

```

## Understand block scope for let
#### this results in error since let is block scope
```javascript
function greet(){
    console.log('hello');
    const boolVal = true;
    if(boolVal){
        let somevar = 'hello world';
        console.log(somevar);
    }
    console.log(somevar)
}


greet();
```

## Understand block scope for var
## since var has function scope it will display value
```javascript
function greet(){
  console.log('hello');
  const boolVal = true;
  if(boolVal){
    var somevar = 'hello world';
    console.log(somevar);
  }
  console.log(somevar)
}


greet();
```

### understand hoisting
#### with var - no error just undefined
```javascript
console.log(testvar);
var testvar = 'hello'
```

#### with let - throw error
```javascript
console.log(testvar);
let testvar = 'hello'
```

## understand redeclaration

#### With var - no error
```javascript
var hello = 'hello';
var hello = 'nonhello';
console.log(hello);
```

## with let
we see syntax error
```javascript
var hello = 'hello';
var hello = 'nonhello';
console.log(hello);
```


#### Understand arrow functions
```javascript
function greet(){
  console.log('hello world')
}

const greet1 = () => {console.log('hello world2')}

greet()
greet1()
```

#### Understand array destructuring
```javascript
const testarr = [1, "one", ()=>{console.log('hello')}]

const[first,second,third]=testarr;

console.log(first);

third()
```

#### Understand object destructuring
```javascript
const person = {
    name : "megha",
    age : 14,
    address : "India"
}

const {name, ...rest} = person;
console.log(rest);

console.log('name',name)
```

