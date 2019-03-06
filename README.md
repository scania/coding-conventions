# Corporate Coding Conventions (WORKING COPY)

Coding practices are a source of a lot of arguments among programmers. Coding standards, to some degree, help us to put certain questions to bed and resolve stylistic debates. No coding standard makes everyone happy and even their existence is sure to make some unhappy. What follows are the standards we put together within the developer community, which have become the general coding standard for all programming teams on new code development. We’ve tried to balance the need for creating a common, recognizable and readable code base with not unduly burdening the programmer with minor code formatting concerns.

## Table Of Contents

- [Why we need Coding Standards](#why-we-need-coding-standards)
- [Context is important](#context-is-important)
- [Stylistic Standards](#stylistic-standards)
- [JavaScript Style Guide](#javascript-style-guide)
- [CSS Style Guide](#css-style-guide)
- [Custom Elements Style Guide](#custom-elements-style-guide)
- [Sharable Linters](#sharable-linters)
- [Contribute](#contribute)
 
# Why we need Coding Standards

Conformity in the code is important to help the user develop an intuition for how to use it. Although every programmer is encouraged to bring their own insight and wisdom to the project, we must also ensure that there is enough consistency so that we can read, use, debug, and maintain each others code. Also, we must consider our direct customers, the users of the engine, i.e. the gameplay and tools programmers, and present them with a consistent and easy to understand interface.

Write your code as if you are writing it for someone else. Which, in fact, you are.

## Code Portability

The more teams, projects and subsidiaries that shares a common code standard, the easier it will be for them to share code and components in between them. The need for future code sharing and re-use is very hard for a team to predict, so following a standard from day 1 will eliminate a lot of unnecessary risk factors. 

# Context is Important

The rules and guidelines here derive from the tools we use, the architectures we work on, and the kind of problems we have to solve. There are situations where doing things the standard way may not be easy. If a rule or guideline makes it substantially more difficult to solve something, use your best discretion about how to resolve it, and let it be known so that this standard can reflect the experience.

# Stylistic Standards

Issues of style are in essence a matter of taste, and as such, are both arbitrary and subject to fruitless debate. That said a consistent set of aesthetic conventions helps readers – especially unfamiliar readers – read and understand code.  So some style elements are included, and are not subject for debate.  In general these reflect current practice.

# JavaScript Style Guide

We are currently evalutaing if we can re-use standards maintained by others. Our [latest survey](https://scania.github.io/corporate-ui-docs/surveys/js-coding-standards/standards-results.html) shows that both Airbnb and Google coding standards are poplular. Since Google seem to be somewhat limitied when it comes to React and Vue projects, we are currently looking into if we can use the Airbnb JavaScript Style Guide.

[Have a look at the Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

# CSS Style Guide

[Have a look at the working copy of our CSS / Sass Styleguide](css-style-guide.md)

# Custom Elements Style Guide

Since we've not found any good guide for creating Custom Elements, we're working on a standard of our own.

# Sharable Linters

We are currently evaluating both the linter and the config from Airbnb:
[Airbnb eslint with config files](https://github.com/airbnb/javascript/tree/master/packages)

# Contribute

We are more than happy to onboard anyone who cares for coding standards to join our work. Currently our Slack channel is the place to go:
[https://corporate-ui.slack.com/app_redirect?channel=coding-standards](https://corporate-ui.slack.com/app_redirect?channel=coding-standards)
