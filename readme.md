# Types in Javascript
What is a "type" in javascript? You're probably familiar with:
- Number
- String
- Boolean
- Array
- Object
- Function
- Null
- Undefined


# Getting Started
This repo has everything you need to compile a basic typescript file into plain old javascript. 

First, we need to install our dependencies by running `npm install`. Then, we can compile our `index.ts` by running `npm run compile`. Check the dist directory to see the result!

# Isn't this just javascript?
Yes! Typescript is a SUPER set of javascript, which means regular javascript is valid Typescript. Typescript also gives us access to additional tools and special syntax in addition to everything regular javascript can do, so lets try adding some of that.

In `./src/index.ts` lets update the function `sayHello`:

```javascript


function sayHello(name: string) {
  return `Hello ${name}!`;
}

```

To see how this is usefull, lets also try changing our function evocation to something _other_ than a string.

```javascript

console.log(sayHello('Simon'));

```

When you run `npm run compile` notice what happens! We get compile time type verifcation, and you will see an error `Argument of type '123' is not assignable to parameter of type 'string'.`. We know immediately that we made a mistake! But it gets better. Let's change our function evocation back to a string and try something else. `console.log(sayHello('Simon'));`

# VScode TypeScript integration
VScode has _awesome_ built in type script integrations. First and formost, you might notice that once you've declared what type some variable should be, VScode will now autocomplete the correct properties of that type for you: 

![VScode suto completion](https://markwilkins.co/files/auto.png "VScode intelisense")

# Custom Types
Typescript not only lets you specify what native type a variable should be, you can also define and use custom types. There are two ways to do this:

## Interfaces
You can think of an interface a bit like a Schema declaration in Mongoose. We will define an object, and what sorts of types various properties of that object will be. Here's an example:

```javascript

interface Teacher {
  name: string,
  yearsTeaching: number,
  isActive: boolean
}

```

Now, we can adjust our function definition to expect an object of this type:

```javascript 

function sayHello(person: Teacher) {
  return `Hello ${person.name}!`;
}

```

and if we try to compile this, we get `Argument of type '"Simon"' is not assignable to parameter of type 'Teacher'.`. Did you catch that? `type 'Teacher'`! We created a new type! 

Typescript will be very strict when checking if our objects match our definitions, try passing an incomplete "Teacher" object:

```javascript

const ourTeacher = {
  name: 'Simon',
  yearsTeaching: 25
};

console.log(sayHello(ourTeacher)); 

```

Check out the compliler error if you run `npm run compile`:
`Argument of type '{ name: string; yearsTeaching: number; }' is not assignable to parameter of type'Teacher'.
  Property 'isActive' is missing in type '{ name: string; yearsTeaching: number; }'.`

  Typescript checked our argument to make sure it matched our definition, and since it didn't we got an error! 


## Classes

## Hooking it up to webpack