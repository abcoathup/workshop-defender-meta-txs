# Defender Meta-Transactions Workshop

Code for the workshop on Meta-Transactions using [OpenZeppelin Defender](https://openzeppelin.com/defender).

This project consists of a sample _names registry_ contract, that accepts registrations for names either directly or via a meta-transaction, along with a client dapp, plus the meta-transaction relayer implementation.

Live demo running at [defender-metatx-workshop-demo.openzeppelin.com](https://defender-metatx-workshop-demo.openzeppelin.com/).

## Structure

- `app`: React code for the client dapp, bootstrapped with create-react-app.
- `autotasks/relay`: Javascript code for the meta-transaction relay, to be run as a Defender Autotask, compiled using rollup.
- `contracts`: Solidity code for the Registry contract, compiled with [hardhat](https://hardhat.org/).
- `scripts`: Custom scripts for common tasks, such as uploading Autotask code, signing sample meta-txs, etc.
- `src`: Shared code for signing meta-txs and interacting with the Forwarder contract.
- `test`: Tests for contracts and autotask.

## Scripts

- `yarn deploy`: Compiles and deploys the Registry and Forwarder contracts to xDAI, and writes their addresses in `deploy.json`.
- `yarn sign`: Signs a meta-tx requesting the registration of `NAME`, using the private key defined in `PRIVATE_KEY`, and writes it to `tmp/request.json`.
- `yarn events`: Lists all the `Registered` events from the deployed contract on xDAI.
- `yarn invoke`: Invokes the relay Autotask via `WEBHOOK_URL` with the contents of `tmp/request.json` generated by `yarn sign`.
- `yarn upload`: Compiles and uploads the Autotask code to `AUTOTASK_ID`.
- `yarn relay`: Runs the relay Autotask script locally, using the Defender Relayer for `RELAY_API_KEY`.
- `yarn test`: Runs tests for contracts and Autotask using hardhat.

## Environment

Expected `.env` file in the project root:

- `PRIVATE_KEY`: Private key used for deploying contracts and signing meta-txs locally.
- `RELAYER_API_KEY`: Defender Relayer API key, used for sending txs with `yarn relay`.
- `RELAYER_API_SECRET`: Defender Relayer API secret.
- `AUTOTASK_ID`: Defender Autotask ID to update when running `yarn upload`.
- `TEAM_API_KEY`: Defender Team API key, used for uploading autotask code.
- `TEAM_API_SECRET`: Defender Team API secret.

Expected `.env` file in `/app`:

- `REACT_APP_WEBHOOK_URL`: Webhook of the Autotask to invoke for relaying meta-txs.
- `REACT_APP_QUICKNODE_URL`: Optional URL to Quicknode for connecting to the xDAI network from the dapp.