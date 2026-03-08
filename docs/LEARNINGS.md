# Node and NPM

`which node` or `node -v` to find current version of Node.

`nvm ls` to view installed Node versions.

`npm` installs and manages packages.

`npx` executes Node packages. It can download them if not locally available.

`npm run dev` runs the `dev` script from `package.json`. In this case, `vite dev`. Could also be run with `npx vite dev`.

# Default files

1. `.npmrc` is an npm configuration file. It has one setting as created, `engine-strict:true`. This ensures that packages incompatible with the engines specificied in `package.json` will not be installed.
2. `.prettierignnore` specifies folders and files for Prettier to ignore.
3. `.prettierrc` sets options for Prettier. Plan to use all the defaults.
4. `AGENTS.md` contains instructions for GitHub Copilot (or other agents used)
5. `eslint.config.js` has config settings for ESLint. Prettier is configured as the project formatter here, to prevent ESLint and Prettier from fighting
6. `package-log.json` lists specific versions of each dependence for consistency and performance. This file is never edited by hand.
7. `package.json` lists metadata, dependencies (development and runtime), and scripts. Scripts are run via npm run. 
8. `svelte.config.js` is the configuration file for SvelteKit. It's currently using `adapter-auto` which detects deployment environment automatically.
9. `tsconfig.json` sets TypeScript compiler options for the project.
10. `vite.config.ts` defines settings for Vite, a local development server and build too. It also configured Vitest (test framework)

# Prettier and ESLint

* Prettier focuses on code formatting. 
* ESLint focuses on code quality and code style (e.g. naming conventions, import ordering). ESLint is configured in this project to leave code formatting to Prettier.
* Enable *Format On Save* in Visual Studio code to automatically format when saving.
* Run `npm run lint` to check formatting. This is mapped in `package.json` and runs both Prettier and ESLint. 

# Visual Studio Code Extensions

1. GitHub Copilot Chat
2. Prettier - Code formatter
3. Svelte for VS Code

# Copilot

* Plan mode. Work with Copilot to research and create a implemtation plan.
* Reference files with the `#` command.

# Testing

* Right now, there's one Vite test in `demo.spec.ts`.
* Vite tests can be run with `npm test`.