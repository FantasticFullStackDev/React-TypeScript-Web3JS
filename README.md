## Getting Started

- `yarn`
- `yarn bootstrap`
- `yarn start`

In addition to compiling each package in watch mode, this will also spin up [packages/example-next](packages/example-next) on [localhost:3000](http://localhost:3000/). (It will also spin up [packages/example-cra](packages/example-cra) on [localhost:3001](http://localhost:3001/), but this is just a skeleton app for testing compatibility.)

## Running Tests

- `yarn test --watch`

## Documentation

This version of web3-react is still in beta, so unfortunately documentation is pretty sparse at the moment. [packages/example-next](packages/example-next), TSDoc comments, and the source code itself are the best ways to get an idea of what's going on. More thorough documentation is a priority as development continues!

## Upgrading Connector Dependencies

Some connectors have one or more dependencies that are specific to the connection method in question. For example, the walletconnect connector relies on `@walletconnect/ethereum-provider` package to handle a lot of the connection logic. Often, you may wish to upgrade to the latest version of a client package, to take advantage of the latest features. web3-react makes the process of upgrading client packages fairly painless by specifying them as [`peerDependencies`](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#peerdependencies). This means that you have to explicitly install client packages, and therefore may transparently switch between any version that agrees with the semver specified in the connector (usually any matching major).

## Adding Connectors

If you're interested in using web3-react with a wallet that doesn't have an "official" connector package, you're in luck! This library was designed to be highly modular, and you should be able to draw inspiration from the existing connectors to write your own! That code can live inside your codebase, or even be published as a standalone package. From time to time, if there's sufficient interest and desire, PRs adding new connectors may be accepted, but this should be brought up in an issue or discussion beforehand.

## Upgrading from v6

While the internals of web3-react have changed fairly dramatically between v6 and v8, the hope is that usage don't have to change too much when upgrading. Once you've migrated to the new connectors and state management patterns, you should be able to use the hooks defined in @web3-react/core, in particular `useWeb3React` (or `usePriorityWeb3React`), as more or less drop-in replacements for the v6 hooks. The big benefit in v8 is that hooks are now per-connector, as opposed to global, so no more juggling between connectors/multiple roots!

## Useful Commands

### Add a dependency

- `yarn lerna add <DEPENDENCY> --scope <PACKAGE>`

### Remove a dependency

- Delete the relevant `package.json` entry

Because of a [lerna bug](https://github.com/lerna/lerna/issues/1883), it's not possible to prune `yarn.lock` programmatically, so regenerate it manually:

- `yarn lerna exec "rm -f yarn.lock" --scope <SUBPACKAGE>`
- `yarn clean --scope <SUBPACKAGE>`
- `yarn bootstrap`
