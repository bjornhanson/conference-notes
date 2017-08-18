# A Math-free Introduction to Neural Networks

Speaker
- [Randall Koutnik](https://github.com/SomeKittens), Senior Software Engineer, Netflix


## Neural Networks
- A type of machine learning
- Used to solve problems we can't easily write programs to solve the problem, but where we can have the computer learn how to solve the problem
- Are only as good as they data that is used to train them (bad data --> bad results)
- Are commonly used for classification problems (which one, `a` or `b`)
- Always have an output between `1` and `0`
- Nowdays usually use what's called the [sigmoid function](https://en.wikipedia.org/wiki/Sigmoid_function)
- `Deep learning` just means the nearal network has hidden layers

Multiple inputs, reducing down to certain outputs
```
x1
  ->
    w1
       +b -> y
    w2
  ->
x2
```

Two outputs from neural network:
- `is zero:` percentage it thinks it's a zero
- `is one:` percentage it thinks it's a one

## Example - WarriorJS

Steps
  1. Data collection
  2. Format data (network can only talk in terms of values 0 and 1)
  3. What is good?
  4. (...missed this one...)
  5. Training (run many scenarios, train to do type of thing more or less depending on result)

# Resources
- [MNIST database of handwritten digits](http://yann.lecun.com/exdb/mnist/)
- [WarriorJS game written in JS, used for learning AI in JS](https://github.com/olistic/warriorjs)
- [Keras deep learning library for Python](https://github.com/fchollet/keras) (runs on Tensorflow, much easier to use)
- [Titanic passenger dataset](https://www.kaggle.com/c/titanic)
- [Netflix jobs](https://jobs.netflix.com/jobs) - they have freedom and responsibility (get to solve problems however they want, but have to be responsible for them, which is sweet)
