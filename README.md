# Bootstrap a Typescript Project

Explicit steps to bootstrap a typescript project with no hidden magic. Be aware
of each step. Only do it if you want it. Expand on these steps as you desire.

## tl;dr

Create git repository and clone

    cd ~/projects/my
    git clone git@github.com:ianhomer/my-repository.git
    cd my-repository
    touch README.md

Review `package.json` and clean out entries not needed.

Copy the following files into your repository as baseline files

- `.github/workflows/build.yaml`
- `.eslintc.js`
- `.gitignore`
- `.lintstagedrc`
- `src/index.ts` - simple typescript file to get rolling

Use the command line if you like

    export BRANCH_URI=ianhomer/bootstrap-typescript/main
    export RAW_URI=https://raw.githubusercontent.com/$BRANCH_URI
    mkdir -p .github/workflows src
    curl $RAW_URI/.github/workflows/build.yaml -sS \
      -o .github/workflows/build.yaml
    curl $RAW_URI/.eslintc.js -sSO
    curl $RAW_URI/.gitignore -sSO
    curl $RAW_URI/.lintstagedrc -sSO
    curl $RAW_URI/src/index.ts -sS -o src/index.ts

Initialise yarn with typescript

    yarn init
    yarn add -D typescript ts-node

Add prettier

    yarn add -D prettier

Add eslint

    yarn add -D                        \
      eslint                           \
      eslint-plugin-simple-import-sort \
      eslint-config-prettier           \
      @typescript-eslint/eslint-plugin \
      @typescript-eslint/parser

Add format-package

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

Check linting added OK

    yarn lint:fix

Add husky and lint-staged

    yarn add -D husky lint-staged
    yarn prepare
    npx husky add .husky/pre-commit "npx lint-staged"

Add `## tl;dr` section to `README.md` guiding user what to do once they've
cloned the repository, start it off with something like

    yarn

and add to this README as the repository evolves.

If it's a public repository add a LICENSE file, e.g. BSD

    curl $RAW_URI/LICENSE -sSO
