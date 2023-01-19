---
sidebar_position: 3
---

# Execute Remote Smart Contract Call

This Dapp allows you to call Pangolin Smart Chain's `add(2)` function from Pangoro Smart Chain.

Pangoro Smart Chain is the testnet of Darwinia Smart Chain. [Pangolin Smart Chain](https://docs.crab.network/evm-compatible-crab-smart-chain/get-started/darwinia-pangolin) is the testnet of Crab Smart Chain. 

## Create a hardhat empty project

Follow the [instructions](https://hardhat.org/hardhat-runner/docs/getting-started) to create an empty hardhat project.

In this example, we have named the project `demo`.

## Install deps

```bash
cd demo
npm install --save-dev @darwinia/contracts-periphery @darwinia/contracts-utils
```

## Prepare cross-chain endpoints

In this example, we need two endpoints. One is for Pangoro Smart Chain, and the other one is for Pangolin Smart Chain. 
1. For convenience, the endpoints can be downloaded directly. 

    ```bash
    cd contracts
    wget https://raw.githubusercontent.com/darwinia-network/darwinia-s2s-template/main/contracts/PangoroToPangolinEndpoint.sol
    wget https://raw.githubusercontent.com/darwinia-network/darwinia-s2s-template/main/contracts/PangolinToPangoroEndpoint.sol
    ```
    Please Note: If you want to use endpoints in a production environment, you need to add access control.

2. Deploy `PangoroToPangolinEndpoint` to Pangoro Smart Chain.
   ```bash
   npx hardhat flatten ./PangoroToPangolinEndpoint.sol > ~/PangoroToPangolinEndpoint.sol
   ```
   Copy the flattened PangoroToPangolinEndpoint.sol to [Remix](https://remix.ethereum.org/) and deploy it to Pangoro Smart Chain.  
   > How to use Remix to deploy a contract? here are some useful articles.  
   [Creating and Deploying a Contract in Remix](https://remix-ide.readthedocs.io/en/latest/create_deploy.html)  
   [Pangoro Smart Chain Info](../../networks/darwinia)


3. Deploy `PangolinToPangoroEndpoint` to Pangolin Smart Chain. 
   ```bash
   npx hardhat flatten ./PangolinToPangoroEndpoint.sol > ~/PangolinToPangoroEndpoint.sol
   ```
   Copy the flattened PangolinToPangoroEndpoint.sol to Remix and deploy it to Pangolin Smart Chain.

   > [Pangolin Smart Chain Info](https://docs.crab.network/evm-compatible-crab-smart-chain/crab-faqs-network-rpc#pangolin-test-network-configuration-parameters)

4. Call the `setRemoteEndpoint(_remoteChainId, _remoteEndpoint)` on the two endpoints so they point to each other. 

   The chain id of Pangoro Smart Chain is `0x70616772`. The chain id of Pangolin Smart Chain is `0x7061676c`.  

   > You can get the full chain id list from [constants](../constants).

## Deploy the callee contract on the Pangolin Smart Chain

In the `demo/contracts` folder, create a file `Callee.sol`.

```javascript
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;

contract Callee {
    uint256 public sum;

    function add(uint256 _value) external {
        sum = sum + _value;
    }
}
```

Copy it to Remix and deploy it to Pangolin Smart Chain.

## Deploy the caller contract on the Pangoro Smart Chain

In the `demo/contracts` folder, create a file `Caller.sol`.

```javascript
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;

import "./PangoroToPangolinEndpoint.sol";

// Call Pangolin.callee.add(2) from Pangoro
contract Caller {
    address public endpoint;

    constructor(address _endpoint) {
        endpoint = _endpoint;
    }

    function remoteAdd(address callee) external payable returns (uint256) {
        uint256 messageId = ToPangolinEndpoint(endpoint).remoteExecute(
            28140, // latest spec version of pangolin
            callee,
            hex"1003e2d20000000000000000000000000000000000000000000000000000000000000002", // add(2)
            120000 // gas limit
        );

        return messageId;
    }
}
```

Make sure that the latest spec version of Pangolin is correct. You can get it from https://pangolin.subscan.io/runtime.

```bash
npx hardhat flatten ./Caller.sol > ~/Caller.sol
```
Copy the flattened Caller.sol to Remix and deploy it to Pangoro Smart Chain. Make sure that the constructor param `_endpoint` is correct when deploying, it must be the PangoroToPangolinEndpoint's address.

## Run

1. You can get a estimated market fee by calling the `fee` function of the PangoroToPangolinEndpoint contract.
2. Call the `remoteAdd(callee)`. 

   * The param `callee` is the `Callee` contract address.   
   * The value input should be set to a market fee >= the estimated market fee.  
   ![Untitled](/img/guide-03-0.png)