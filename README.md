# css-in-javascript-2name: 'Tests: pretest/posttest'

on: [pull_request, push]

jobs:
  pretest:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        package:
          - '..'
          - eslint-config-airbnb
          - eslint-config-airbnb-base

    defaults:
      run:
        working-directory: "packages/${{ matrix.package }}"

    steps:
      - uses: actions/checkout@v2
      - uses: ljharb/actions/node/install@main
        name: 'nvm install lts/* && npm install'
        with:
          node-version: 'lts/*'
      - run: npm run pretest
