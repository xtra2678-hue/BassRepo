name: Run Source Code Tests

# Trigger the workflow every time code is pushed or a pull request is made to the main branch
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  run-tests:
    # Run the tests on the latest Ubuntu Linux environment provided by GitHub
    runs-on: ubuntu-latest

    steps:
    # Step 1: Check out the repository source code onto the runner
    - name: Check out repository code
      uses: actions/checkout@v4

    # Step 2: Set up the correct version of Node.js
    - name: Set up Node.js
      uses: actions/setup-node@v4
      with:
        node-node-version: '20'
        cache: 'npm' # Caches dependencies to make future runs faster

    # Step 3: Install the project's dependencies
    - name: Install dependencies
      run: npm ci

    # Step 4: Execute the test suite
    - name: Run test script
      run: npm test
