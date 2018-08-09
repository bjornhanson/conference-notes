# A Practical Approach to the Component Library Challenge
- Speaker: [Amy Gebhardt](https://github.com/agebhardt) (@amlyhamm)
- [Presentation repo](https://github.com/lund0n/jscodeshift-midwestjs)

## Notes

1. Get to know your users
    - Who will be using this? Engineers? Designers? Product owners? What would make this successful from their perspective?
2. Take an inventory
    - Do you have an existing app? What's currently out there? Do this from both a code and design perspective.
3. **Determine the deal-breakers**
    - What has prevented this from being successful in the past? Framework? Versioning? Lack of interest?
4. Determine a tech stack
    - What's compatible with your app(s)? How is this going to limit you in the future? Where are things now and where do you see it going? Be prepared for this to keep changing!
5. Pay attention to terminology
    - What is a "component"? How about a "dual scrolly"? Or a "drop down"?
6. Decide and commit to a component lifecycle (difficult to actually do)
    - How does a component get designed? When is it ready for development? What are the technical expectations? (accessibility standards, testing, documentation, linters, versioning, internationalization, SEO, responsive, etc.)
    - Does a proposed change add value for the user? If not, it's not worth the time.
    - "No, I'm not slowing you down. I'm making things more efficient for the future."
7. Don't forget about your designers
    - What assets do they have available to them? How can you help them follow standards and component limitations?
8. Propose your plan and determine an owner for the project
    - Get your team excited and committed to the idea.
    - Focus on the *why*: who is this for? Why will it benefit them?
    - Don't allow this to become a "nice-to-have" in your workflow - determine an owner and let them own the project.
9. Be prepared to use those soft skills
    - You'll be wearing a lot of hats
    - Not everyone will be easy to please
    - Listen, adapt, educate
    - Buy-in is essential to the success of the project
10. Respect the creative process
    - Remove as many roadblocks as possible while still ensuring consistency
    - Keep adjusting

## SportsEngine Demo

- SportsEngine has their own web app that has components, how to use them, code and working examples, etc. (kinda like Bootstrap's website)
- Each component is in its own private npm package
- They made a custom ui json config file that is consumed by a custom node app that installs the necessary componenets (at their specific versions), what theme to use, etc. and the results are TypeScript compiled and dumped into a clean directory structure with just the JS and CSS files that engineers need
- Amy sends out an HTML email newsletter every month that show what was released, how many contributeors, how many people used things, etc. and examples of what's new and coming soon
