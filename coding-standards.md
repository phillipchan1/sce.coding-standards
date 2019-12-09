---
description: Coding Standards for SCE
---

# Coding Standards

Digital Accelerator's set of coding rules, programming styles, guidelines, and best practices that developers adhere to when writing source code for a project.

## Table of Contents

1. [Introduction](#introduction)
2. [The Actual Standards](#the-actual-standards)
    - [Coding Standards](#coding-standards)
    - [Application-Level Standards](#application-level-standards)
        - [General Application Recommendations](#general-application-recommendations)
        - [Project Organization Standards](#project-organization-standards)
        - [Testing Standards](#testing-standards)
        - [React / React-Native Standards](#react-/-react-native-standards)
    - [Operational Standards](#operational-standards)

## Introduction

This document describes the operational plan for ensuring consistent and quality code standards for projects undertaken by the Digital Accelerator Group at SCE.

In order for this to be successful, we see this happening at several hierarchical levels (concentric circles represents micro → macro):

![diagram](./assets/Code_Standards_Diagram.png)

### The hierarchy of standards

-   Coding Standards - coding styles, logic rules, linting
-   Application Standards - practices relevant to the application
-   Operational - practices related to team resources

### The implementation of standards

To carry about these standards in the most efficient and sustainable way, we require the convergence 1) tooling 2) procedure 3) and leadership to make it possible across every level that we are seeking to standardize.

### The strategy for implementation

> In reference to the concentric circles of standards, there is a direct relationship with the level of automation as it moves outward away from the circle.

We prefer automation at coding standards at the coding standards level, but as we move outwards the process inherently require more human resources to implement and enforce. This is because application-level concerns are largely application-specific and it is difficult to have cross-application principles.

# The Actual Standards

## Coding Styling

#### Use [prettier](https://prettier.io/) and [eslint](https://eslint.org/)

Use prettier to automate code styling and eslint to ensure micrologic quality

_.prettierrc config_

```
tabWidth: 2
semi: false
singleQuote: true
parser: "babylon"
bracketSpacing: true
```

_.eslint.js config_

```
module.exports = {
  extends: ['sonarqube', 'plugin:react/recommended'],
  plugins: ['babel', 'no-loops'],
  parser: 'babel-eslint',
  env: {
    node: true
  }
}
```

_Pre-Commit Checks_

To enforce linting and styling standards, use [lint-staged](https://github.com/okonet/lint-staged) and [husky](https://www.npmjs.com/package/husky)

_husky and lint-staged config in package.json_

    "husky": {
        "hooks": {
          "pre-commit": "lint-staged"
        }
      },
      "lint-staged": {
        "*.{js,css}": [
          "prettier --write",
          "eslint",
          "git add"
        ],
        "*.{js,json,css}": [
          "prettier --write",
          "git add"
        ]
      }

#### Use [Typescript](https://www.typescriptlang.org/) and tsx

Projects should use typescript to have strict typing and provide more assumable coding experience for developers

#### Other Coding Standards

-   No unused code in code base
-   No unused files in code base
-   Prefer no comments in code

## Application-Level Standards

### General Application Recommendations

Unlike coding standards whose standards have more rigidity, application-level concerns vary from application to application and will require a human resource to discern correctly about the right way to go about things. However these are suggestions about application-level concerns

#### Prefer offline first architecture when appropriate

#### Prefer Graphql over REST when appropriate

#### Prefer UI libraries; if making our own, leverage atomic design

#### Prefer no side effects and have immutable state and use sagas to handle asyncronous application state management

### Project Organization Standards

#### Use kebab case for file/folder nomenclature

```
// bad

/AzureLogin
  AzureLogin.ts
  Lib/
    AzureLoginUtils.ts
```

```
// good

/azure-login
  azure-login.ts
  lib/
    azure-login.utils.ts
```

#### Organize folders/files by domains not functionality

```
// bad

/components
  dashboard.ts
  login.js
/types
  dashboard.types.ts
  login.types.ts
```

```
// good

/login
  login.ts
  login.types.ts
/dashboard
  dashboard.ts
  dashboard.types.ts
```

#### Prefer a root level `app/` folder for core application-wide functionality

### Testing Standards

#### To have high quality unit tests for components (70%+)

See:

-   [Rethinking Unit Test Assertions](https://medium.com/javascript-scene/tdd-changed-my-life-5af0ce099f80)
-   [TDD Changed My Life](https://medium.com/javascript-scene/rethinking-unit-test-assertions-55f59358253f)

#### To have integration tests for every important integration

-   100% coverage for core services (authentication, authorization, first screen, etc)
-   Important integrations are anything critical for the main features of the application to work.

#### Testing Tools

-   [Jest](https://jestjs.io/)
-   [Appium](http://appium.io/) (react-native)
-   [Cypress](https://www.cypress.io/) (react)

### React / React Native Standards

#### Typescript Prop Types

Prefer it over react's prop types as it 1) catches errors on build time vs runtime and 2) provides autofill in the IDE

#### Prefer functional and pure components

All components should start as functional components unless it is guaranteed it needs to be a class component

#### Prefer application state to component state when applicable

There should be almost no state stored in components. Observe state management best practices

#### Prefer not using snapshot testing but valuable and readable component testing

## Operational Standards

#### Peer/Team Leader review for code

All code should be at least peer reviewed.

#### Use Feature branches then merge in

Branch and commit names should be readable. When developers look at code and are tracing its history, they should be able to reference a ticket number to gain contextual information regarding its feature

_Branch Nomenclature_

```
[type]/[ticket-number]-[branch-name]

// bad
my-branch-name

// good
feature/2911-add-offline-support
```

_Commit Name Nomenclature_

```
[ticket-number] - [feature-name]

//bad
use redux

// good
2911 - use redux for dashboard component
```

#### Every feature to have QA

#### Prefer low config Dev setup and automation as possible

#### Acceptance criteria

#### Test driven development

#### Consultation for DA UX to inform UX decisions

#### Need real time team chat

#### Need comments on ticket for every update for visibility

#### Commitment to disciplined agile practice

#### Microcommits

Tooling

#### VSTS / Jira

#### Teams / Slack
