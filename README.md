# React TypeScript Boilerplate

**Template React project with full TypeScript and SSR support.**

This project is a compilation of different approaches in React development that allows not only to start a new project quickly, but to learn how it works under the hood.

---

## What's Inside

Core:

- **React** 18+ (**Preact** 10+ as an option, see [comparison](#react-vs-preact) below)
- **webpack** 5+ (with optional **SWC** support and SSR or static build)
- **TypeScript** (with strict rules, including webpack configuration)

SSR:

- **Express** (with render to stream option including helmet data and initial state pushing)

State:

- **Redux** 4+

Router:

- **React Router**

Code Splitting:

- **Loadable Components** (SSR compatible)

API:

- **RTK Query**

i18n (Internationalization):

- **Lightweight custom solution** based on Redux (with async loading and SSR support; [why not any common i18n package?](#why-not-any-common-i18n-package))

Styles:

- **(S)CSS modules** (with TypeScript support)

Linters:

- **TS Standard** (TypeScript Style Guide, with linter and automatic code fixer based on [StandardJS](https://standardjs.com/))
- **Stylelint** (including rules order)
- **Prettier**

Tests:

- **Jest** 29+
- **React Testing Library**
- Utility for Redux Testing
- One example of integration test of a component with user event and Redux

Other:

- API request caching (powered by RTK Query)
- Data prefetching on server side
- Hot reload (including state, style and server code hot reloading)
- VSCode support with error highlight and on save fixes
- Script for fast component creation
- Optional Service worker and offline status detector
- Webpack Bundle Analyzer

## The App

This boilerplate includes a simple application with:

- Several screen/pages with their own routes
- Local counter
- Global counter
- One of the components is dynamically loaded
- API requests
- Loading spinner
- Theme switcher (light and dark)
- Offline detector

(due to free hosting, a cold start could be slow)

## How to Use

### Quick Start (SSR with hot reload)

1. Clone this repo:

   `git clone https://github.com/StopNGo/react-ssr-boilerplate`

2. Install all packages:

   `npm i`

3. Run project in a development mode:

   `npm start`

4. Open your browser with the next address:

   `http://localhost:8080/`

### Build and run a server (SSR)

1. Build the project (production bundle will be in the `"dist"` folder):

   `npm run build`

   or with Webpack Bundle Analyzer report server:

   `npm run build:report`

2. Run a server:

   `npm run run`

3. You can test the server locally:

   `http://localhost:3000/`

### Static development mode with hot reload

- Just run the next command and browser will open automatically:

  `npm run start:static`

### Static production

- Run the next command and get a production bundle in the `"dist"` folder:

  `npm run build:static`

  or with Webpack Bundle Analyzer report server:

  `npm run build:static:report`

### Updating packages

All packages in this project are pinned to latest versions at the time of publishing to exclude version-based conflicts and errors and to guarantee proper work of the code in this repository.

If you want to update packages, do next:

```
npm install -g npm-check-updates
ncu -u
npm i
```

## Basic App Configuration

All configuration is available in files with constants:

- `webpack\constants.ts` - contains working directories, SWC option and other related to bundling staff
- `src\constants` - a directory with app files with configuration constants
- `src\server\constants.ts` - contains a server port and render to stream options

### React vs Preact

In `webpack\constants.ts` you can choose to use [Preact](https://preactjs.com/) library instead React itself (`IS_PREACT` boolean constant).

Preact is a fast and compact React-compatible Virtual DOM library. But because its community is much smaller, you can face with some incompatibility with React API and functionality, especially with new ones. Also some tests show some frame drops during moving a lot of elements. Below you can see a bundle size comparison of no-SSR version of the sample application of this repository (according to Webpack Bundle Analyzer):

|         | React     | Preact   |
| ------- | --------- | -------- |
| Parsed  | 278.75 KB | 164.82 KB |
| Gzipped | 91.11 KB  | 55.59 KB |

### Why not any common i18n package?
You can freely integrate any React compatible i18n solution. But if this app already uses Redux and RTK, why just not use them for this task? Therefore, I have created a custom internationalization solution with a minimum additional code. It supports translations dynamic loading, server side rendering based on user acceptable languages, strict typing, etc. At the moment it just does not support string processing like pluralization, but it could easily be added later.
