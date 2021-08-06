# ⑂ forker

[![version](https://img.shields.io/badge/version-0.0.1-7f187f.svg)](https://github.com/lelia/forker/releases)
![license: MIT](https://img.shields.io/badge/license-MIT-0fa573.svg)
[![contributor covenant](https://img.shields.io/badge/contributor%20covenant-2.0-4baaaa.svg)](CODE_OF_CONDUCT.md)
[![tests](https://github.com/lelia/forker/actions/workflows/test.yml/badge.svg)](https://github.com/lelia/forker/actions/workflows/test.yml)

Github action to automate fork creation. This action uses [octokit.js](https://github.com/octokit/octokit.js) and the [GitHub API](https://docs.github.com/en/rest) to automatically create a repository fork, either in your personal namespace or an organization you administer.

Before forking a repository into an organization, `forker` will check membership and outside collaborator status for the user requesting the fork. When the `addUser` option is enabled, `forker` will automatically invite the specified `user` to become a member of the organization where the fork has been requested.

⚠️ Note that the invitation will be sent from whichever account is used to authenticate the Github action and fork the requested repository, meaning there must be sufficient permissions to invite outside users to the organization.

For legal and compliance reasons, organizations or individuals can choose to provide an optional `licenseWhitelist` to compare against the [license of the repository](https://docs.github.com/en/rest/reference/licenses) being forked. If the license key returned by the Github API is not found within the provided whitelist, `forker` will exit without forking the repository.

----

Use this template to bootstrap the creation of a TypeScript action. :rocket:

This template includes compilation support, tests, a validation workflow, publishing, and versioning guidance.  

If you are new, there's also a simpler introduction.  See the [Hello World JavaScript Action](https://github.com/actions/hello-world-javascript-action)

## Create an action from this template

Click the `Use this Template` and provide the new repo details for your action

## Code in Main

> First, you'll need to have a reasonably modern version of `node` handy. This won't work with versions older than 9, for instance.

Install the dependencies  
```bash
$ npm install
```

Build the typescript and package it for distribution
```bash
$ npm run build && npm run package
```

Run the tests :heavy_check_mark:  
```bash
$ npm test

 PASS  ./index.test.js
  ✓ throws invalid number (3ms)
  ✓ wait 500 ms (504ms)
  ✓ test runs (95ms)

...
```

## Change action.yml

The action.yml contains defines the inputs and output for your action.

Update the action.yml with your name, description, inputs and outputs for your action.

See the [documentation](https://help.github.com/en/articles/metadata-syntax-for-github-actions)

## Change the Code

Most toolkit and CI/CD operations involve async operations so the action is run in an async function.

```javascript
import * as core from '@actions/core';
...

async function run() {
  try { 
      ...
  } 
  catch (error) {
    core.setFailed(error.message);
  }
}

run()
```

See the [toolkit documentation](https://github.com/actions/toolkit/blob/master/README.md#packages) for the various packages.

## Publish to a distribution branch

Actions are run from GitHub repos so we will checkin the packed dist folder. 

Then run [ncc](https://github.com/zeit/ncc) and push the results:
```bash
$ npm run package
$ git add dist
$ git commit -a -m "prod dependencies"
$ git push origin releases/v1
```

Note: We recommend using the `--license` option for ncc, which will create a license file for all of the production node modules used in your project.

Your action is now published! :rocket: 

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

## Validate

You can now validate the action by referencing `./` in a workflow in your repo (see [test.yml](.github/workflows/test.yml))

```yaml
uses: ./
with:
  milliseconds: 1000
```

See the [actions tab](https://github.com/actions/typescript-action/actions) for runs of this action! :rocket:

## Usage:

After testing you can [create a v1 tag](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md) to reference the stable and latest V1 action
