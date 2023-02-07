---
sidebar_position: 1
---

# Overview


[Darwinia.js](https://github.com/darwinia-network/darwinia.js) API library allows application developers to query Darwinia and Pangoro chain and interact with the chain's substrate interfaces using JavaScript. In this docs, we will look into how we can use some common code examples to interact with Darwinia node using Darwinia.js API library.

### Dependencies

The library sample mainly depends on the following libraries:

- **@polkadot/api** The _polkadot api_ library provides a Promise-style interface for performing related operations on the Darwinia chain.

- **ethers.js** The _ethers.js_ library aims to be a complete and compact library for interacting with the Ethereum blockchain and its ecosystem.

### Usage

Install library

```nodejs

yarn add @darwinia/api-options

```

Darwinia.js include Darwinia, Pangoro chain interfaces for developer to interact with one of them. With this, you can query and interact Darwinia node. Here is a config sample for using those node interfaces. we must configure **tsconfig.json** at compilerOptions section to apply type augmentation explicitly.



1. Applying Darwinia Chain type augmentation in tsconfig.json

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@polkadot/api-augment": ["./node_modules/@darwinia/api-augment/index.d.ts"],
      "@polkadot/types-augment": ["./node_modules/@darwinia/types/interfaces/augment-types.d.ts"],
      "@polkadot/rpc-augment": ["./node_modules/@darwinia/rpc-augment/index.d.ts"],
      "@polkadot/types/lookup": ["./node_modules/@darwinia/types-augment/index.d.ts"]
    }
  }
}
```


2. Applying Pangoro Chain type augmentation in tsconfig.json



``` json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@polkadot/api-augment": ["./node_modules/@darwinia/api-augment/pangoro/index.d.ts"],
      "@polkadot/types-augment": ["./node_modules/@darwinia/types/interfaces/augment-types.d.ts"],
      "@polkadot/rpc-augment": ["./node_modules/@darwinia/rpc-augment/pangoro/index.d.ts"],
      "@polkadot/types/lookup": ["./node_modules/@darwinia/types-augment/lookup/pangoro/index.d.ts"]
    }
  }
}

```


####  Create API Instance

You must first instantiate an API instance of the darwinia.js api. Create the wsProvider using the websocket endpoint of the Darwinia node.

```typescript
// Import
import { ApiPromise, WsProvider } from '@polkadot/api';
...
// Construct with darwinia node endpoint
const wsProvider = new WsProvider('wss://rpc.darwinia.network');
const api = await ApiPromise.create({ provider: wsProvider });

// Do something
console.log(api.genesisHash.toHex());

```

Due to darwinia has own substrate module and types, this mean developers are adding sepcific types for implementation as well. To close the gap, we have defined types for different node spec versions. You could inject types by our **typesBundle** . Let's change instantiate api instance to let Api know our types.

```typescript
// Import
import { ApiPromise, WsProvider } from '@polkadot/api';
import { typesBundle } from "@darwinia/types/mix";
...
// Construct
const wsProvider = new WsProvider('wss://rpc.darwinia.network');
const api = await ApiPromise.create({ provider: wsProvider, typesBundle: typesBundle.spec.darwinia });

// Do something
console.log(api.genesisHash.toHex());

```




####  Metadata and API Decoration

It's useful to understand some basic workings of the library.
When the API connects to a node, one of the first things it does is to retrieve the metadata and decorate the API based on the metadata information. The metadata effectively provides data in the form of api.`<type>`.`<module>`.`<section>` that fits into one of the following `<type>` categories: consts, query and tx.

None of the information contained within the api.{consts, query, tx}.`<module>`.`<method>` endpoints are hard coded in the API. Rather everything is fully decorated by what the metadata exposes and is therefore completely dynamic. This means that when you connect to different chains, the metadata and API decoration will change and the API interfaces will reflect what is available on the chain you are connected to.

#### API Example

We take some common examples on ApiPromise version of API. They are same with Polkadot.js API  allow application developers to interact with node's interface 
including "runtime constants", "state queries", "RPC queries" and so on. You can check the [Polkadot Docs](https://polkadot.js.org/docs/api/start) for more detailed usage description.
