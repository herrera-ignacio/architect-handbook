# E2E Anti-Patterns

- [E2E Anti-Patterns](#e2e-anti-patterns)
  - [Don't use your UI to build up state](#dont-use-your-ui-to-build-up-state)

## Don't use your UI to build up state

It's enormously slow, cumbersome, and unnecessary.

For example, __logging in__ is a prerequisite of state that comes before most of your tests. Do not use your UI to log in.

If you are using tools like Cypress instead of Selenium, you can skip needing to use the UI by using `cy.request()` to build up state without using your browser's UI.
