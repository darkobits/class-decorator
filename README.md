![class-decorators](https://user-images.githubusercontent.com/441546/36626828-a3f00872-18ee-11e8-8a02-1200e3961d9d.png)

[![][npm-img]][npm-url] [![][travis-img]][travis-url] [![][codacy-img]][codacy-url] [![][cc-img]][cc-url] [![][xo-img]][xo-url]

This package attempts to improve the way classes are decorated (see: [decorator proposal](https://ponyfoo.com/articles/javascript-decorators-proposal)) by not polluting the prototype chain, encouraging _composition over inheritance_.

## Install

This package requires [`@babel/plugin-proposal-decorators`](https://new.babeljs.io/docs/en/next/babel-plugin-proposal-decorators.html).

```bash
$ npm i -D @babel/plugin-proposal-decorators
$ npm i @darkobits/class-decorators
```

Then, update your `.babelrc` file:

```
{
  "plugins": [
    ["@babel/plugin-proposal-decorators", {
      "legacy": true
    }]
  ]
}
```

## Use

### `ClassDecorator`

This package's default export is a function that accepts a decorator implementation function and returns a decorator that may be applied to a class. The decorator implementation function is invoked with the target class. If the decorator implementation returns
a function, that function will be used as a proxy constructor for the decorated class. The proxy constructor will be passed an object with the following shape:

```ts
{
  // Invoke this function to call the decorated class' original constructor.
  constructor: Function;
  // Array of any arguments passed to the constructor.
  args: Array<any>;
}
```

**Example:**

In this example, we will create a higher-order decorator that accepts a list of superpowers to apply to class instances.

First, we will look at how this is done using the typical approach, then how to accomplish it using this package.

```ts
function AddSuperpowers (...powers) {
  return function (Ctor: Function): Function {
    return class AddSuperPowers extends Ctor {
      constructor(...args) {
        super(...args);

        powers.forEach(power => {
          this[power] = true;
        });
      }

      hasSuperpower(power: string): boolean {
        return this[power];
      }
    }
  };
}

@AddSuperpowers('strength', 'speed', 'flight')
class Person {
  name: string;

  constructor(name) {
    this.name = name;
  }

  getName(): string {
    return this.name;
  }
}

const bob = new Person('Bob');

bob.strength; //=> true
bob.speed; //=> true
bob.flight; //=> true
```

This approach works, but if we examine the prototype chain of the `bob` instance, it will look something like this:

```
bob: {
  name: 'Bob'
  strength: true
  speed: true
  flight: true
  [[Prototype]] => AddSuperpowers: {
}                    hasSuperpower()
                     [[Prototype]] => Person: {
                   }                    getName()
                                        [[Prototype]] => Object
                                      }
```

If we used 5 decorators on the `Person` class, we would find 5 degrees of inheritance added to each instance of `Person`. Decorators should faciliate _composition_, not exacerbate existing issues with inheritance.

Let's see how with a few modifications we can improve this situation:

```ts
import ClassDecorator from '@darkobits/class-decorators';

const AddSuperpowers = (...powers: Array<any>): Function => ClassDecorator(Ctor => {
  // Add hasSuperpower to the decorated class.
  Ctor.prototype.hasSuperpower = function (power: string): boolean {
    return this[power];
  };

  // Returning a function which will serve as a delegate for the original
  // constructor.
  return function ({constructor, args}): void {
    powers.forEach(power => {
      this[power] = true;
    });

    // Call the original constructor, forwarding any arguments provided.
    constructor(...args);
  }
});


@AddSuperpowers('strength', 'speed', 'flight')
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  getName(): string {
    return this.name;
  }
}

const bob = new Person('Bob');
```

If we looked at the protoype chain for this instance of `bob`, we would see:

```
bob: {
  name: 'Bob'
  strength: true
  speed: true
  flight: true
  [[Prototype]] => Person: {
}                    getName()
                     hasSuperpower()
                     [[Prototype]] => Object
                   }
```

### `MethodDecorator`

Accepts a decorator implementation function and returns a decorator that may be applied to class methods. The decorator implementation function is passed a single object with the following shape:

```ts
{
  // Prototype object that owns the decorated method.
  prototype: object;
  // Name of the decorated method.
  methodName: string;
  // Property descriptor of the decorated method.
  descriptor: PropertyDescriptor;
}
```

If the decorator implementation function returns a function, the returned function will act as a proxy for the original method. The proxy will be invoked each time the original method is called, and is passed a single object with the following shape:

```ts
{
  // Any arguments passed to the method call.
  args: Array<any>;
  // Original method, pre-bound to the class instance.
  method: Function;
}
```

**Example:**

```ts
import {MethodDecorator} from '@darkobits/class-decorators';

const AddSalutation = MethodDecorator(({prototype, methodName}) => {
  // Optionally manipulate prototype here.

  // Return a function which will serve as a delegate for the original method.
  return ({args, method}) => `Hello, my name is ${method()}.`;
});

class Person {
  name: string;

  constructor(name: string): void {
    this.name = name;
  }

  @AddSalutation
  getName(): string {
    return this.name;
  }
}

const bob = new Person('Bob');
bob.getName() //=> 'Hello, my name is Bob.'
```

## &nbsp;
<p align="center">
  <br>
  <img width="22" height="22" src="https://cloud.githubusercontent.com/assets/441546/25318539/db2f4cf2-2845-11e7-8e10-ef97d91cd538.png">
</p>

[travis-img]: https://img.shields.io/travis/darkobits/class-decorators.svg?style=flat-square
[travis-url]: https://travis-ci.org/darkobits/class-decorators

[npm-img]: https://img.shields.io/npm/v/@darkobits/class-decorators.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/@darkobits/class-decorators

[codacy-img]: https://img.shields.io/codacy/coverage/bd23f052d0ec42b0ada5e46b006e6511.svg?style=flat-square
[codacy-url]: https://www.codacy.com/app/darkobits/class-decorators

[xo-img]: https://img.shields.io/badge/code_style-XO-e271a5.svg?style=flat-square
[xo-url]: https://github.com/sindresorhus/xo

[cc-img]: https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?style=flat-square
[cc-url]: https://conventionalcommits.org/
