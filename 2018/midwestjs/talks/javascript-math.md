# How Does JavaScript Math?
- Speaker: Meara Charnetzki (@m34ra)

## Notes

JavaScript automatically does coercion (implicitly converting one type to another)

    2 + '2' = '22'    // Convert first number to string

What if we add other things?

    [1, 2, 3, 4] + [5, 6]     // '1,2,3,45,6'

    true + true               // 2

    undefined + null          // NaN

    null + null               // 0

    [] + {}                   // '[object Object]'

    {} + []                   // 0

`+` in front of anything casts it to a number


## Resources
- ["Wat" video](https://www.destroyallsoftware.com/talks/wat) by Gary Bernhardt
- https://www.ecma-international.org/ecma-262/5.1/
- https://medium.freecodecamp.org/js-type-coercion-explained-27ba3d9a2839
