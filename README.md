# React Native Hybrid Typescript App

Let's build a hybrid app using Typescript!

This experiment sets up separate frontend & native packages, with some simple copy scripts to move code back and forth for now.

The idea is that by isolating the projects, top-level configurations can live separately.

## Key branches in this repo

`a-starter`

`b-redux`

`c-glamorous`

## frontend (Web)

React Native for Web:

https://github.com/necolas/react-native-web

react-native-typescript-transformer:

https://github.com/ds300/react-native-typescript-transformer

#### Dependencies:

(on top of an ejected Create-React-App)

`yarn remove babel-eslint eslint eslint-config-react-app eslint-loader eslint-plugin-flowtype eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react`

`yarn add react-native-web typescript tslint awesome-typescript-loader babel-plugin-react-native-web babel-jest babel-preset-env babel-preset-react babel-preset-react-native react-test-renderer ts-jest babel-jest canvas-prebuilt prettier @types/node @types/jest @types/react-native @types/react`

#### Configs:

- rn-ts-transfomer packager config: [rn-cli.config.js](packages/frontend/rn-cli.config.js)
- Load typescript in [webpack.config.dev.js](packages/frontend/webpack.config.dev.js) in `module > rules`
- [tsconfig.json](packages/frontend/tsconfig.json) - note "skipLibCheck" fix
- custom jest config in [package.json](packages/frontend/package.json)

#### Jest - issues!

- needed to remove the match `|(\\.|/)(test|spec)` because it was matching the file scripts/test.js (provided by the ejected CRA)
- needs [special mocks](https://facebook.github.io/jest/docs/en/webpack.html) to handle inline svg
- had to add dependency `canvas-prebuilt` to avoid error during test
- was erroring out on Animated code, had to work around by setting style in state

## native

#### Dependencies:

(on top of react-native init)

`yarn add -D react-native-typescript-transformer typescript tslint ts-jest prettier @types/node @types/react-native @types/react @types/jest fs-extra`

#### Configs:

- [Extra package.json declaring "src"](packages/native/src/package.json) at top of `src` directory - don't skip this step, it's necessary!
- [tsconfig.json](packages/native/tsconfig.json)
- [rn-cli.config.js](packages/native/rn-cli.config.js)
- custom jest config in [package.json](packages/native/package.json)


#### Jest: issues here too!

- Difficult to get images to work, resolved using the assetsTransformer solution from [this thread](https://github.com/facebook/jest/issues/2663)
