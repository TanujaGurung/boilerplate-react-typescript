**latest ESLint + Prettier + Typescript and React Project ready boilerplate.**

This is the boilerplate for ESLint + Prettier + Typescript and React Project with husky hook.

Can directly clone it and use it for your upcoming project to build from scratch or if you need step by step procedure to build it and install it from scratch then here are the steps below:

Usually, the problem is that every time you have to set up ESLint and Prettier you go to the web search for an article, and this article is probably not updated. Usually, they use a lot of plugins and non-default configurations.

We are going to use the basic configuration of ESLint and Prettier to have fewer headaches.

**step 1 : Create react app**

➜ yarn create react-app boilerplate-react-typescript --template typescript or ➜ npx create-react-app boilerplate-react-typescript --template typescript ➜ cd boilerplate-react-typescript

--template typescript: used to create a ReactJS TypeScript project instead of JavaScript.

What is ESLint? ESLint is a JavaScript linting open source project and is used to find problems and syntax issues in your code, it will help us find broken logic that would be found only in run time.

**step 2 : To install ESLint:**

➜ yarn add -D eslint or ➜ npm install eslint --save-dev

After installing the ESLint we have to initialize the config file: npx eslint --init

Here we are going to answer some questions about our project:

? How would you like to use ESLint? … To check syntax only ▸ To check syntax and find problems To check syntax, find problems, and enforce code style

Choose ‘To check syntax and find problems’ because later we are going to use Prettier to enforce code style as well.

? What type of modules does your project use? … ▸ JavaScript modules (import/export) CommonJS (require/exports) None of these

Choose JavaScript modules mainly because ReactJS uses them.

? Which framework does your project use? … ▸ React Vue.js None of these

Choose ‘React’ as our framework.

? Does your project use TypeScript? ‣ No / Yes

Choose ‘Yes’ for TypeScript.

? Where does your code run? … (Press to select, to toggle all, to invert selection) ✔ Browser ✔ Node

Choose ‘Browser’ because ReactJS runs on the Browser.

? What format do you want your config file to be in? … JavaScript YAML ▸ JSON

Here you are free to choose any of the options, but I am going to use JSON as my format

The config that you've selected requires the following dependencies: eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest ? Would you like to install them now with npm? ‣ No / Yes

If you are using NPM then just select ‘Yes’, if not select ‘No’ then copy the packages and:

➜ yarn add -D eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest or ➜ npm i eslint-plugin-react ➜ npm i @typescript-eslint/eslint-plugin ➜ npm i @typescript-eslint/parser

Right now the ESLint package created a .eslintrc file with the format you choose:

Before continuing we have to install TypeScript plugins related to ESLint and to do so:

➜ yarn add -D eslint-plugin-import @typescript-eslint/parser eslint-import-resolver-typescript or ➜ npm i eslint-import-resolver-typescript ➜ npm i eslint-import-resolver-typescript

If everything went well your eslintrc file should look something like this:

                                {
                        "env": {
                            "browser": true,
                            "es2021": true
                        },
                        "extends": [
                            "eslint:recommended",
                            "plugin:react/recommended",
                            "plugin:@typescript-eslint/recommended"
                        ],
                        "parser": "@typescript-eslint/parser",
                        "parserOptions": {
                            "ecmaFeatures": {
                                "jsx": true
                            },
                            "ecmaVersion": "latest",
                            "sourceType": "module"
                        },
                        "plugins": [
                            "react",
                            "@typescript-eslint"
                        ],
                        "rules": {
                        }
                    }
Let’s install prettier and then edit the eslint and prettier configuration files.

Before all, what is Prettier?

Prettier is a code style formatter, different from ESLint, Prettier only format the code style, and does not look for syntax problems.

Rules like max-len, no-mixed-spaces-and-tabs, keyword-spacing, comma-style are some popular formatting rules in Prettier.

And rules like no-unused-vars, no-extra-bind, no-implicit-globals, prefer-promise-reject-errors are common rules in ESLint.

In this case, I prefer ESLint to search for problems and syntax errors and let the code style for prettier.

step 3: To install Prettier:

➜ yarn add -D prettier eslint-config-prettier eslint-plugin-prettier eslint-plugin-react-hooks or ➜ npm i eslint-config-prettier ➜ npm i eslint-plugin-prettier ➜ npm i eslint-plugin-react-hooks

After installing you have to create the prettierc file:

➜ touch .prettierrc

At this point you have a blank .prettierrc file and a default eslintrc file, so the next step is to configure the eslintrc file.

Open your eslintrc file.

If you are going to use or you intend to use Jest in your project add the next lines to your ‘env’:

                        {
                            "env": {
                                "browser": true,
                                "es2021": true,
                            "jest": true // Add this line!
                            },
                            ...
                        }
To use prettier alongside with eslint you need to change the extends object:

                    {
                        ...
                        "extends": [
                        "eslint:recommended",
                        "plugin:react/recommended",
                        "plugin:@typescript-eslint/recommended",
                        "prettier" // Add this line!
                        ],
                        ...
                    }
The main part of ESLint is the rules objects. Here you can put any rule you think is good for your project and team.

My basic configuration is this:

                    {
                        ...
                        "rules": {
                            "react/react-in-jsx-scope": "off",
                            "camelcase": "error",
                            "spaced-comment": "error",
                            "quotes": ["error", "single"],
                            "no-duplicate-imports": "error"
                    },
                        ...
                    }
If you want to learn more about ESLint rules you can check out rules page.(https://eslint.org/docs/rules/)

To use the plugins we have installed, update the plugins object in the eslintrc file:

"plugins": ["react", "react-hooks", "@typescript-eslint", "prettier"],

The last thing to set up in ESLint is the eslint-import-resolver-typescript. Just add the settings key in the eslint configuration file.

                {
                    ...
                    "settings": {
                    "import/resolver": {
                    "typescript": {}
                    }
                }
                }
Lastly, we are going to set up the .prettierrc file

My basic configuration for prettierrc file is:

                {
                "semi": false,
                "tabWidth": 2,
                "printWidth": 100,
                "singleQuote": true,
                "trailingComma": "all",
                "jsxSingleQuote": true,
                "bracketSpacing": true
                }
But if you want to learn more check out the options page.(https://prettier.io/docs/en/options.html)

Finally, we have to add the scripts in the package.json:

            {
                ...
                "scripts": {
                ...
                "lint": "eslint src/**/*.{js,jsx,ts,tsx,json}",
                    "lint:fix": "eslint --fix src/**/*.{js,jsx,ts,tsx,json}",
                    "format": "prettier --write 'src/**/*.{js,jsx,ts,tsx,css,md,json}' --config ./.prettierrc"
                    },
            ...
            }
Basically: lint: will search for problems, but will not fix lint fix: will search and try to fix the problems. format: will call prettier to fix the code style.

What are Git Hooks? Git hooks are scripts that you can set up to run at certain events in the Git lifecycle. These events include different stages of a commit, like before a commit (pre-commit) and after a commit (post-commit).

These are useful in that they allow developers to run custom code tasks or even enforce standards by automating other scripts to run those tasks.

What is Husky? Husky is a tool that allows us to easily wrangle Git hooks and run the scripts we want at those stages.

It works by including an object right within our package.json file that configures Husky to run the scripts we specify. After that, Husky handles managing at which point in the Git lifecycle our scripts will run.

**step 4: install husky**

yarn add husky or npm install husky

next after installing edit your package.json file

            "script": {
                ....
                "prepare": "husky install",
                "pre-commit": "lint-staged"
            }
Your project must be having .husky folder in the root folder.

under husky folder add file pre-commit and add the following line of code #!/usr/bin/env sh . "$(dirname -- "$0")/_/husky.sh" npm run lint:fix

make one more file with name commit-msg and add the following line of code #!/bin/sh . "$(dirname "$0")/_/husky.sh"

                    MSG_FILE=$1
                    FILE_CONTENT="$(cat $MSG_FILE)"
                    RED='\033[0;31m'
                    GREEN='\033[0;32m'
                    NO_COLOR='\033[0m'

                    # Initialize constants here
                    export REGEX='^\[.*\] .+|^Merge branch'
                    export ERROR_MSG="Commit message format must match regex \"${REGEX}\""

                    echo $MSG_FILE
                    echo $FILE_CONTENT

                    if [[ $FILE_CONTENT =~ $REGEX ]]; then
                        echo -e "${GREEN} Good commit! ${NO_COLOR}"
                    else
                    echo -e "${RED} Bad commit \"$FILE_CONTENT\" ${NO_COLOR}"
                        echo $ERROR_MSG
                        exit 1
                    fi

                    exit 0
The above commit pattern is "git commit -m "[./folder/filename] add your commit here"

If the pattern for commit is not followed then you will get an error Bad commit "added commit-msg"

If the pattern is followed then you get message like Good commit!

Anything I missed out then feel free to raise an issue.

resources I followed:

https://www.freecodecamp.org/news/how-to-add-commit-hooks-to-git-with-husky-to-automate-code-tasks/
https://blog.devgenius.io/eslint-prettier-typescript-and-react-in-2022-e5021ebca2b1
https://blog.logrocket.com/build-robust-react-app-husky-pre-commit-hooks-github-actions/
https://typicode.github.io/husky/#/?id=features
https://dev.to/monfernape/enforce-husky-pre-commit-with-eslint-prettier-in-monorepo-55jc#:~:text=Go%20to%20your%20frontend%20project%20and%20install%20eslint%2C,eslint-plugin-prettier%20eslint-config-prettier%20--save-dev%20npm%20install%20--save-dev%20--save-exact%20prettier
