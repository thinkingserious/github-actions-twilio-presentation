# Github Actions Demo Workshop

## Objective

To learn & understand deployment pipelines, what problems they solve, and how they can be integrated at a small scale, using CI/CD tools with Github Actions.

[Click here to access Presentation Slides](https://docs.google.com/presentation/d/1Jz0vqQQwX5S2_Xosug1_-kiCCa7irOdfnS53xQZCkks/edit?usp=sharing)

## Instructions

1. Fork the repository.

   - _Note: If you have your own Node.js project with several npm/yarn scripts already, you may use that instead._

2. Clone your fork to local. You can run `npm i` and `npm run build` optionally.
3. Go to "Actions" tab on your forked repository
4. Look for "Node.js" when searching for a Workflow template
5. You can click "Start Commit" on the right side, or copy the contents of the .yml file and proceed with the following steps:

   1. Create a folder in the **root** directory of your fork called `.github`.
   2. Inside the `.github` folder, create a folder called `workflows`. This is where you will create any workflow files.
   3. Create a `.yml` file, name it whatever you want, and paste the contents you copied from earlier on the remote repository.

6. Your `.github/workflows/<name>.yml` file should look very close to this:

```yaml
name: Node.js CI

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
```

7. Stage, commit, and push the changes to your remote repository (or the fork) and click on "Actions" on the remote repository again and see the job running live.
