# How to "build your damn app already!" with Meteor
- Speaker: [Joshua Longanecker](https://github.com/notarypublic)
- [Todo app demo project repo](https://github.com/notarypublic/meteor-todo-final) that was built during the talk
- [Slides](https://docs.google.com/presentation/d/1GYGtSLL5f8DN9nQ3xaczv5EaGZOk-CMKgv8PeD9ldiY/edit)

## Why build an app as a business
- No inventory cost
- Cheap setup cost (just server hosting)
- No shipping or real estate
- Education is free
- Quick to get started...kind of

## What makes an app, an app?
A non-trivial app:
- User accounts
- Persistent public/private data stored in a database
- Routing

## MEAN Stack
- Setup database
- Setup Gulp
- Setup file structure
- Update Gulp
- ... etc., ...

## Meteor (under the hood)
- MongoDB
- Node
- Templating Language built-in (very similar to Handlebars)
- Client-side DB (minimongo)
- Real-time websockets (magic)
- Lots of magic
- No setup

## Let's build an app
- `meteor create todo-midwest-js`
- `cd todo-midwest-js`
- `meteor`
- That's it. Now can replace boilerplate code with your stuff.

## Files to start with
- `main.html`
- Loads every HTML file that exist in the `client` directory

## Two Major Building Blocks of Meteor
- Helpers
- Events (all the UI events)

## Installing additional packages
- `meteor add fourseven:scss` to add [fourseven's SCSS package](https://atmospherejs.com/fourseven/scss)
- `meteor add iron:router` to add [a router](https://atmospherejs.com/iron/router)

## Package As Phone App
- Single command using Ionic

## Resources
- [Atmosphere](https://atmospherejs.com) repository for Meteor modules (can also use NPM now, but it's more work)
- [Todo app demo project repo](https://github.com/notarypublic/meteor-todo-final) -- He needs to update this with .meteor stuff
- [Discover Meteor book](https://www.discovermeteor.com) (in-depth)
- [Meteortips.com](http://meteortips.com) (in-depth tutorials)

## Other Links I Found
- [Meteor TODO app tutorial with React](https://www.meteor.com/tutorials/react/creating-an-app)
- [How to use React with Meteor](https://guide.meteor.com/react.html)
