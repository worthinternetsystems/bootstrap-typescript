# Bootstrap a Typescript Project

## tl;dr

Create git repository and clone

    cd ~/projects/my
    git clone git@github.com:ianhomer/my-repository.git
    cd my-repository
    touch README.md

Review `package.json` and clean out entries not needed.

Copy the following files into place as baseline

- `.github/workflows/build.yaml`
- `.eslintc.js`
- `.gitignore`
- `.lintstagedrc`

Initialise yarn with typescript

    yarn init
    yarn add -D typescript ts-node

Install prettier

    yarn add -D prettier

Install eslint

    yarn add -D                        \
      eslint                           \
      eslint-plugin-simple-import-sort \
      eslint-config-prettier           \
      @typescript-eslint/eslint-plugin \
      @typescript-eslint/parser

Install format-package

    yarn add -D format-package

Add the following scripts to `package.json`

    "scripts": {
      "eslint": "eslint src --ext .ts",
      "eslint:fix": "eslint src --ext .ts --fix",
      "lint": "yarn prettier && yarn eslint",
      "lint:fix": "yarn package:fix && yarn prettier:fix && yarn eslint:fix",
      "package:fix": "format-package -w",
      "prepare": "husky install",
      "prettier": "npx prettier --check .",
      "prettier:fix": "npx prettier --write ."
    },

Create an empty `src/index.ts`.

Lint fix with

    yarn lint:fix

Add husky and lint-staged

    yarn add -D husky lint-staged
    yarn prepare
    npx husky add .husky/pre-commit "npx lint-staged"

Add `## tl;dr` section to `README.md` guiding user what to do once they've
cloned the repository, start it off with something like

    yarn

and build on this as the repository evolves.
