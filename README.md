# Prettier Setup Guide for React, Next.js, and Node.js Projects

This guide provides step-by-step instructions for setting up Prettier in your React, Next.js, and Node.js projects. Prettier is an opinionated code formatter that ensures consistent code style across your project.

## Table of Contents

- [Common Setup](#common-setup)
- [React Setup](#react-setup)
- [Next.js Setup](#nextjs-setup)
- [Node.js Setup](#nodejs-setup)

## Common Setup

These steps are common for all project types:

1. Install Prettier as a dev dependency:
   ```bash
   npm install --save-dev prettier
   ```

2. Create a `.prettierignore` file in the project root:
   ```
   node_modules
   build
   dist
   .next
   coverage
   ```

3. Create an `.editorconfig` file in the project root:
   ```ini
   root = true

   [*]
   charset = utf-8
   indent_style = space
   indent_size = 2
   end_of_line = lf
   insert_final_newline = true
   trim_trailing_whitespace = true

   [*.md]
   trim_trailing_whitespace = false
   ```

4. Add a format script to your `package.json`:
   ```json
   "scripts": {
     "format": "prettier --write \"**/*.{js,jsx,ts,tsx,json,md}\""
   }
   ```

5. (Optional) Install the Prettier extension for your code editor.

6. (Optional) Set up a pre-commit hook using Husky and lint-staged (instructions below).

## React Setup

For React projects, follow these additional steps:

1. Create a `.prettierrc` file in the project root:
   ```json
   {
     "semi": true,
     "singleQuote": true,
     "trailingComma": "es5",
     "tabWidth": 2,
     "printWidth": 100,
     "jsxSingleQuote": false,
     "bracketSpacing": true,
     "jsxBracketSameLine": false,
     "arrowParens": "avoid"
   }
   ```

2. If using TypeScript, ensure your `tsconfig.json` includes:
   ```json
   {
     "include": ["src/**/*"],
     "compilerOptions": {
       "jsx": "react"
     }
   }
   ```

3. To run Prettier:
   ```bash
   npm run format
   ```

## Next.js Setup

For Next.js projects, follow these steps:

1. Create a `.prettierrc` file in the project root:
   ```json
   {
     "semi": true,
     "singleQuote": true,
     "trailingComma": "es5",
     "tabWidth": 2,
     "printWidth": 100,
     "jsxSingleQuote": false,
     "bracketSpacing": true,
     "jsxBracketSameLine": false,
     "arrowParens": "avoid"
   }
   ```

2. Update your `next.config.js` to ignore Prettier files:
   ```javascript
   module.exports = {
     webpack: (config, { isServer }) => {
       // Fixes npm packages that depend on `fs` module
       if (!isServer) {
         config.node = {
           fs: 'empty'
         }
       }
       return config
     },
     // Ignore Prettier files
     reactStrictMode: true,
     pageExtensions: ['js', 'jsx', 'ts', 'tsx'],
   }
   ```

3. To run Prettier:
   ```bash
   npm run format
   ```

## Node.js Setup

For Node.js projects, follow these additional steps:

1. Create a `.prettierrc` file in the project root:
   ```json
   {
     "semi": true,
     "singleQuote": true,
     "trailingComma": "es5",
     "tabWidth": 2,
     "printWidth": 100,
     "endOfLine": "lf",
     "arrowParens": "always",
     "bracketSpacing": true,
     "quoteProps": "as-needed",
     "proseWrap": "preserve",
     "overrides": [
       {
         "files": "*.js",
         "options": {
           "parser": "babel"
         }
       },
       {
         "files": "*.ts",
         "options": {
           "parser": "typescript"
         }
       }
     ]
   }
   ```

2. If using TypeScript, ensure your `tsconfig.json` includes:
   ```json
   {
     "compilerOptions": {
       "target": "es6",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     },
     "include": ["src/**/*"],
     "exclude": ["node_modules"]
   }
   ```

3. To run Prettier:
   ```bash
   npm run format
   ```

## Setting Up Pre-commit Hook (Optional)

To automatically format your code before each commit:

1. Install Husky and lint-staged:
   ```bash
   npm install --save-dev husky lint-staged
   ```

2. Add the following to your `package.json`:
   ```json
   {
     "husky": {
       "hooks": {
         "pre-commit": "lint-staged"
       }
     },
     "lint-staged": {
       "*.{js,jsx,ts,tsx,json,md}": ["prettier --write"]
     }
   }
   ```

3. Initialize Husky:
   ```bash
   npx husky install
   ```

4. Create a pre-commit hook:
   ```bash
   npx husky add .husky/pre-commit "npx lint-staged"
   ```

Now, Prettier will automatically format your code before each commit.

## Formatting on Save

To format your code automatically each time you save, you can configure your code editor. Here are instructions for some popular editors:

### Visual Studio Code

1. Install the Prettier extension for VS Code.
2. Open your VS Code settings (File > Preferences > Settings).
3. Search for "Format On Save" and check the box to enable it.
4. Also search for "Default Formatter" and select "Prettier - Code formatter" from the dropdown.

### WebStorm / IntelliJ IDEA

1. Go to Preferences/Settings > Languages & Frameworks > JavaScript > Prettier.
2. Check the box next to "On code reformat" and "On save".
3. Select Prettier package: choose your project's node_modules/prettier.

### Sublime Text

1. Install Package Control if you haven't already.
2. Install the JsPrettier package via Package Control.
3. Go to Preferences > Package Settings > JsPrettier > Settings.
4. Add `"auto_format_on_save": true` to your settings.

### Atom

1. Install the prettier-atom package.
2. In the package settings, check the box next to "Format on Save".

Remember to have the `.prettierrc` file in your project root so that your editor uses your project-specific Prettier configuration.

## Conclusion

With these setups, you'll have Prettier configured for your React, Next.js, or Node.js projects. This ensures consistent code styling across your project and team. Remember to commit the `.prettierrc`, `.prettierignore`, and `.editorconfig` files to your repository so that all developers use the same configuration.

For any updates or changes to Prettier, always refer to the [official Prettier documentation](https://prettier.io/docs/en/index.html).
