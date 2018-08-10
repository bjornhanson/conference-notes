# Hello Real World Of Legacy Code: Story of Yelp's Migration to React
- Speaker: [Tanvi](https://tanvip.github.io) (Yelp)

## Notes

As projects progress, the "legacy code jungle" grows. Things may be duplicated without knowing, etc.

Why is legacy code a problem?

- Architectual decisions
  - Scalability
  - Reusability
  - TIght coupling
  - Ownership
- Maintenance
  - Ease of making changes and complexity of code
  - Development time
- Testing
  - Testability of code defines how reliable it is to depend on
- Performance
  - How many layers of entangled code does a request have to go through to get a response?
  - Measurement of time budget

How do you introduce modern code to the old, legacy code jungle?

- Recognize the problem
  - Tight coupling of *unlike* componenets
  - Difficult in supporting user growth
  - Your devs are frustarted
  - Managers complain
- Foresee the future
  - Don't fall for immediate gratification
  - With more experience comes better judgement
  - Put your foot down if you have to
- Control adding new code to the legacy code base
  - Tell developers to not add new code
  - Invest in training devs to not add new code
  - Will that work?
  - Use coding guards, let builds fail, let the code cry

Reactive measures
- Big rewrite vs iterative fixes
  - Depends on your situation (can you shut down part of or the whole app and write a new one)
- Smaller refactors
  - Break into smaller refactors (easier to track and monitor)
  - Smaller, reliable modules are better than one giant flaky codebase
- Broadcast
  - Let developers know about refactor in progress, report unwanted activity
- Monitor with metrics
  - "If you can't measure impact, it's already a failure"
  - Code reliability => tests
  - Schedule time for writing tests and metrics to monitor perforamnce
  - Pretty dashboards: [SignalFX](https://signalfx.com/)
  - Bugsnap
- Dark launching
  - Run experiments
  - Roll out the refactored code only to smaller cohort of users first
  - Monitor
  - Roll out to 100% of production traffic
- Automated code refactoring
  - Yelp engineers wrote a tool called [Undebt](https://github.com/yelp/undebt)

## Migration to React

Yelp uses React with Cheeta templating engine

Some Yelp stats
- 148M Reviews
- 77M Monthly unique users on desktop web
- 500+ engineers
- 1000+ unique routes

Old stack
- Python web server (Pyramid/UWSGI)
- Python templates (Cheetah)
- jQuery + Closure Library
- SCSS (BEM)
- Closure compiler

A Yelp page is composed of many different components that come from different, smaller services

Using React was much simpler for using UI elements from their componenet library. Much less code for a dev to use means less problems.

They swapped Cheetah partials for React componenets.

They made a `render_react_component` function devs could import into existing Python code to swap new React modules in existing Python code.

React was way faster than their old infrastructure. They rewrote most heavily trafficked pages in it first.

They had a Google Doc with all issues listed and anyone could comment on them, so they didn't go to production unti all comments were addressed.

To help convince the business of needing a rewrite, show them the numbers of things will be better, or try giving estimates and telling them how much sooner things would be done with new code vs legacy code.

[Yelp Engineering Blog](https://engineeringblog.yelp.com/)
