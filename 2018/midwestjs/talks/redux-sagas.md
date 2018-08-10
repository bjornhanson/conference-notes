# Taming Redux with Sagas
- Speaker: Mike Plummer (Object Partners)
- [Slides](https://mike-plummer.github.io/redux-sagas-presentation)
- [Demo repo](https://github.com/mike-plummer/hangman)

## Intro

What's the problem? Managing complex/async flows in Redux is hard.

What are the hard parts?
- Ensuring happens-before relationships
- Error handling
- Readability, maintainability
- Testing!

What about `redux-thunk`? It made things easier, but not easy.

Awesomeness in `redux-saga`:
- Uses ES2015 to abstract away async complexity
- Readable and maintainable
- Trivial to handle errors
- Easy to test

What is a Saga?
> A flow of logic & interactions executed in response to a Redux action

A Saga can:
- Read redux state
- Call functions
- Generate actions
- Wait for actions
- ...and many other interactions

A Saga is a generator function
1. Each step of the Saga is a `yield` within the generator
2. The Saga runs (and waits) for each `yield` in turn
3. THe farmework runs generators in a promise-aware way
4. Multiple instances of the same Saga can run concurrently

## Helpers & Effects

Sagas use helper functions for each possible interaction

    const currentReduxState = yield select();

    yield put({
      type: 'SAVE',
      value: valueToSave
    })

    const result = yield call(myFunction, 'arg1', 'arg2');

Helpers create 'effects'

An 'effect' is an object instructing redux-saga what to do

    yield call(Api.fetch, './products');
    {
      CALL: {
        fn: Api.fetch,
        args: ['./products']
      }
    }

## Structure

1. Watcher
    - Watches for conditions we care about and invokes the appropriate Saga. These are initialized at app startup.
2. Saga
    - Invoked by a Watcher and are responsible for business logic. They are initialized on-demand.

A couple helpers to build watcher:
- `takeEvery` - execute saga every time action occurs
- `takeLatest` - takeEvery & cancel any previous instances

Watcher examples:

    const watchers = [
      // Start 'save' saga every time "SAVE" action occurs
      takeEvery("SAVE", save),

      // Start 'refresh' saga every time "REFRESH" action occurs
      // Cancel any instances already running.
      takeLatest("REFRESH", refresh)

      // Every time any action is seen kick off the 'analytics' saga
      takeEvery("*", analytics)
    ];

    // Sagas
    function* save(saveAction) {
      // Logic here
    }
    function* refresh(refreshAction) {
      // Logic here
    }

Saga example (easier to read than `redux-thunk` as it's top to bottom):

    function* save(saveAction) {
      try {
        // Dispatch action for user to CONFIRM save
        yield put({ type: "CONFIRM" });

        // Wait for user to respond with CONFIRM or CANCEL
        const choice = yield take(["CANCELLED", "CONFIRMED"]);
        if (choice.type === "CANCELLED") {
          return;
        }

        // Kick off API call to save
        yield call(Api.save, action.value);

        // API call succeeded, dispatch SUCCESS action
        yield put({ type: "SUCCESS" });
      } catch (error) {
        // Any errors fall into here, dispatch FAILURE action
        yield put({ type: "FAILURE" });
      }
    }

Getting started with Sagas (setup & config):

    import { applyMiddleware, createStore } from 'redux';
    import createSagaMiddleware from 'redux-saga';
    import rootReducer from './reducers';
    import watchers from './watchers'; // Reference to your watchers

    export const buildStore = () => {
      // Build Saga middleware
      const sagaMiddleware = createSagaMiddleware();
      // Saga middleware can be combined with other middleware
      const enhancers = applyMiddleware(sagaMiddleware, ...others);
      // Build your Redux store
      const store = createStore(rootReducer, enhancers);
      // Kick off the watchers - can be delayed if needed
      // (wait until after app init, for example)
      sagaMiddleware.run(watchers);

      return store;
    };

## Testing

`redux-saga-test-plan`
- Separate library that makes testing Sagas so very easy
- http://redux-saga-test-plan.jeremyfairbank.com/

