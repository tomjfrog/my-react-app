# Artifactory Component Dependency Demo
Component and application build instructions taken from [here](https://dev.to/alexeagleson/how-to-create-and-publish-a-react-component-library-2oe)

# Creating the React App and Installing the Component
```bash
npx create-react-app my-app --template typescript
npm install react-component --registry https://tomjfrog.jfrog.io/artifactory/api/npm/reactcomponent-npm-dev-local/
```
# Publishing the application to Artifactory without JFrog CLI
## Create a local `.npmrc` file in the root of the project with contents similar to:
```
//<artifactory-server-name>>/artifactory/api/npm/<artifactory repo name>/:_auth = <hashed password from Artifactory UI "Set Me Up" helper>
email = <artifactory user email>
always-auth = true
```
> Note: The .npmrc file is not checked into source control.  It will contain credentials to your Artifactory instance.
## Build with local NPM client
```bash
npm run build
npm publish --registry https://tomjfrog.jfrog.io/artifactory/api/npm/myreactapp-npm-dev-local/
```
# Publishing with Local NPM and JFrog CLI
```bash
jf c use  tomjfrog.jfrog.io
jf rt npm-config --server-id-resolve tomjfrog.jfrog.io --server-id-deploy tomjfrog.jfrog.io --repo-resolve myreactapp-npm-dev-virtual --repo-deploy myreactapp-npm-dev-virtual
jf npm ci --build-name myreactapp --build-number 1
jf npm publish --build-name=myreactapp --build-number=1
jf rt bp myreactapp 1
```

# Publishing with JFrog Pipelines

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
