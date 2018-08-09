# Harnessing the Power of ASTs using jscodeshift
- Speaker: [Jeremy Lund](https://github.com/lund0n) (Twitter: @Jeremy_Lund)
- [Presentation repo](https://github.com/lund0n/jscodeshift-midwestjs)

## Notes

ASTs used by many tools (Babel, ESLint, Prettier, etc.).

We're looking at a codemod tool maintained by Facebook called [jscodeshift](https://github.com/facebook/jscodeshift)

Install

    npm install -g jscodeshift

On CLI, use `-t` to do transform. Need to make a [transform](https://github.com/facebook/jscodeshift#transform-module) file (written in JS)

    jscodeshift -t [transform] [file/dir]

Can also use jscodeshift right in [astexplorer.net](http://astexplorer.net)

Example 1 (can use this in [astexplorer.net](http://astexplorer.net), pick jscodeshift):

    // file.js
    const a = 'Hello, ';

    function showGreeting(name) {
      return a + name;
    }

    // transform.js
    function transformer(file, api) {
      const j = api.jscodeshift;

      return j(file.source)
        .find(j.Identifier, {
          name: 'a',
        })
        .replaceWith(j.identifier('greeting'))
        .toSource();
    }

    module.exports = transformer;

Can do more complex things with transformation:

    // transform.js
    function transformer2(file, api) {
    const j = api.jscodeshift;

    const toUpdate = {
      a: 'greeting',
      b: 'farewell',
    };

    return j(file.source)
      .find(j.Identifier)
      .filter(p => toUpdate[p.value.name])
      .replaceWith(p => j.identifier(toUpdate[p.value.name]))
      .toSource();
    }

    module.exports = transformer;

## Resources
- http://astexplorer.net
- https://github.com/facebook/jscodeshift
- https://github.com/sejoker/awesome-jscodeshift
- https://github.com/reactjs/react-codemod
