# About
This project is simple blockchain based comment managment based on Mumbai Test Polygon network.
It was created along with tutorial from [@pointer.gg](https://www.pointer.gg/tutorials/create-a-web3-forum-with-polygon/1cb8f005-08f4-48a2-9d82-cd963e16f7f1)

I encourage you to go throught this tutorial yourself. It's fun and in the end you can get something as a reward for your time :) 


# Demo
Contract is deployed in Mumbai Test Polygon network under adress: 

```shell
0x57e3d09f763d9cab1d4cd8cb2b309c42531c5252
```

You can check contract and it's transaction on [Mumbai Polygonscan](https://mumbai.polygonscan.com/address/0x57e3d09f763d9cab1d4cd8cb2b309c42531c5252)

Frontend is deployed in Vercel: https://blokchain-dev-polygon-forum.vercel.app/


If you need founds for testing use one of the [Polygon Faucets](https://faucet.polygon.technology/)


# Build

# Dependencies
Install all dependencies with command:

```shell
npm install
```

## Smartcontract
Smartcontract is written in [Solidity](https://docs.soliditylang.org)

I use [hardhat](https://hardhat.org/) to compile and deploy.

In order to compile just run:

```shell
npx hardhat compile
```

## Frontend
Source code contains frontend written in Next.js along with some other React usefull libraires such as: 

* [chakra-ui](https://chakra-ui.com/getting-started) - a component library that makes it quick and easy to build apps

* [react-query](https://react-query.tanstack.com/) - a popular async state management library

* [wagmi](https://github.com/tmm/wagmi) - a collection of React hooks to help us do web3 things

* [davatar](https://www.npmjs.com/package/@davatar/react) - an avatar component for web3


To start development server just run
```shell
npx hardhat compile
```

# Deployment
In order to deploy this smartcontract either to Polygon mainnet or Mumbain Test Polygon network you need to follow few steps:

1. Compile your contract with commands above. After succesfull compilation you shoult have ``artifacts`` folder in your project which contains ABI and JSONRPC files.

2. Open ``hardhat.config.js`` in root direcotry of this project and uncomment lines:

```js
    // matic: {
    //   url: "https://rpc-mumbai.maticvigil.com",
    //   accounts: [process.env.PRIVATE_KEY],
    // },
```
3. Create file ``.env`` in root directory and add single line:

```js
    PRIVATE_KEY={YOUR_WALLET_PRIVATE_KEY}
```

> **DO NOT COMMIT THIS FILE TO REPO. YOUR PRIVATE KE SHOULD REMAIN ON YOUR MACHINE.EXPOSING PRIVATE KEY OF YOUR WALLET MAY CAUSE TO STELL FROM YOUR WALLET**

4. Run command: 
```shell
npx hardhat run --network matic scripts/deploy.js
```

``scripts/deploy.js`` will deploy your previously compilled contract to the Mumbai network. 

**If you want to change network just edit ``hardhat.congig.js`` file. See [hardhat](https://hardhat.org/) documentation**

5. You will see contract adress in console. You can check your contaract in [Mumbai Polygonscan](https://mumbai.polygonscan.com)

6. Your frontend need to know adress of your contract. Navigate to ``hooks/useCommentsContract.tx`` and replace your contract address in line

```js
...
 const contract = wagmi.useContract({
    addressOrName: "YOUR_CONTRACT_DDRESS",
    contractInterface: CommentsContract.abi,
    signerOrProvider: signer.data || provider,
  });
...
```

7. You are done! Enjoy !
