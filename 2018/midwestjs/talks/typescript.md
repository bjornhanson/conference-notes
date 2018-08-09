# const name: Language = 'TypeScript';

Speakers
- [Abraham Williams](https://github.com/abraham) - experienced developer, start-up founder, international speaker, senior developer at Bendyworks, top 1% contributor at Stack Overflow and an active member of Google Developer
- [Pearl Latteier](https://github.com/pearlbea) - software engineer at Bendyworks (in Madison, WI), a Google Developer Expert in web technologies, and co-organizer of Madison's Google Developer Group

Resources
- [slides.today](https://slides.today/decks/-LH8wTBkC8kd7wpjCMiF)
- [Slides](https://docs.google.com/presentation/d/1HkGh_fBU6FXYYgDIbJl9h_w56dEUEXcPczpDHeSTyCk/edit)

## About TypeScript

Why use TypeScript?
- Helps you catch errors earlier
- Refactor more confidently
- Self-documenting
- Use modern JavaScript (TypeScript is a superset of JavaScript)


Elm has more runtime checks, whereas TypeScript is more development checks

Examples:

    const num1: number = 123;

    const multiply = (a: number, b: number): number => {
      return a * b;
    }

Can do both of these:

    let stuff: string[];

    let things: Array<number>;

Can "opt-out" of type-checking if the type is not known:

    let dunno: any;

Can make custom types:

    type HasVowels = (arg: string) => boolean;

    type Things = Person | Book;

"Generics" are like templates in C++:

    function randomItem<T>(arr: T[]): T {
      let randomIndex = Math.floor(Math.random() * arr.length);
      return arr[randomIndex];
    }

    randomItem<string>(['once', 'twice]);
    randomItem([1, 2, 3]);

Example with remote data:

    // lib.ts
    type RemoteData<E, D> = Initialized | Pending | Failure<E> | Success<D>;

    // app.ts
    type State = RemoteData<number, Tweet>;

## Setting Up TypeScript

How to install:

    npm install --save-dev typescript

    npx tsc --init

Creates a tsconfig.json:

    {
      "compilerOptions": {
        "target": "es5",          // Output JS version (ES5, ES2016, ESNext, etc.)
        "module: "commonjs",      // Output module type (commonjs, umd, ESNext, etc.)
        "strict": true,           // Enable all strict type-checking options
        "esModuleInterop": true
      }
    }

Look for types at [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)

    npm i --save-dev @types/lodash

## Tools

- tslint

        npm install --save-dev tslint
        npx tslint --init
        npx tslint --project tsconfig.json

- TypeDoc
- Visual Studio Code
- ts-node

        npm install ts-node

        npx tsc app.ts
        node app.js

        npx ts-node app.ts

## Resources
- https://www.typescriptlang.org/
- https://basarat.gitbooks.io/typescript/
- https://kangax.github.io/compat-table/es6/
- http://earlbarr.com/publications/typestudy.pdf
- https://github.com/DefinitelyTyped/DefinitelyTyped
- https://github.com/TypeStrong/ts-node
- https://github.com/TypeStrong/typedoc
- https://palantir.github.io/tslint/
- https://github.com/Microsoft/tsdoc
