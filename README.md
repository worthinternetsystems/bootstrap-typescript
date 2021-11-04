# Bootstrap a Typescript Project

Explicit steps to bootstrap a typescript project with no hidden magic. Be aware
of each step. Only do it if you want it. Expand on these steps as you desire.

## tl;dr

Either create git repository and clone

    cd ~/projects/my
    git clone git@github.com:ianhomer/my-repository.git
    cd my-repository

or **(OPT1)** initialise git repository locally and push

    cd ~/projects/my/my-repository
    git init --initial-branch=main

Copy the following files into your repository as baseline files

- `.github/workflows/build.yaml`
- `.eslintc.js`
- `.gitignore`
- `.lintstagedrc`
- `src/index.ts` - simple typescript file to get rolling

Use the command line to copy files into place if you like

    export BRANCH_URI=ianhomer/bootstrap-typescript/main
    export RAW_URI=https://raw.githubusercontent.com/$BRANCH_URI
    mkdir -p .github/workflows src
    curl $RAW_URI/.github/workflows/build.yaml -sS \
      -o .github/workflows/build.yaml
    curl $RAW_URI/.eslintrc.js -sSO
    curl $RAW_URI/.gitignore -sSO
    curl $RAW_URI/.lintstagedrc -sSO
    curl $RAW_URI/src/index.ts -sS -o src/index.ts

Initialise yarn with typescript

    yarn init
    yarn add -D typescript ts-node

Review `package.json` and clean out entries not needed.

Add prettier, eslint and format-package for linting

    yarn add -D                        \
      prettier format-package          \
      eslint                           \
      eslint-plugin-simple-import-sort \
      eslint-config-prettier           \
      @typescript-eslint/eslint-plugin \
      @typescript-eslint/parser

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

Kick off `README.md` and add `## tl;dr` section guiding user what to do once
they've cloned the repository, start it off with something like

    touch README.md
    echo -e "# title\n\n## tl;dr\n\n    yarn" >> README.md

and add to this README as the repository evolves.

If **(OPT2)** it's a public repository add a LICENSE file, e.g. BSD

    curl $RAW_URI/LICENSE -sSO

Commit and push

    git add .
    git commit -am "Start"

If **(OPT1)** you initialised git repository repository then add the remote
origin

    git remote add origin git@github.com:ianhomer/boot1.git

And push

    git push
