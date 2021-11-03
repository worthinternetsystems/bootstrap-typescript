# Bootstrap a Typescript Project

## tl;dr

Create git repository and clone

    cd ~/projects/my
    git clone git@github.com:ianhomer/my-repository.git
    cd my-repository
    touch README.md

Review `package.json` and clean out entries not needed.

Copy `.gitignore` into place.

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

And copy `.eslintrc.js` into place.

Install format-package

    yarn add -D format-package

Add the following scripts to `package.json`

    "scripts": {
      "eslint": "eslint src --ext .ts",
      "eslint:fix": "eslint src --ext .ts --fix",
      "lint": "yarn prettier && yarn eslint",
      "lint:fix": "yarn package:fix && yarn prettier:fix && yarn eslint:fix",
      "package:fix": "format-package -w",
      "prettier": "npx prettier --check .",
      "prettier:fix": "npx prettier --write .",
      "update": "yarn upgrade"
    },

Create an empty `src/index.ts`.

Lint fix with

    yarn lint:fix

Add pipelines, e.g. `.github/workflows/build.yaml` and
`.github/workflows/update.yaml`
