# Using Hardhat

This article will show you how to compile, deploy, and interact with smart contracts using Hardhat on ICE testnode.

* Continue until you reach step 7 of the process from [Hardhat tutorial](https://hardhat.org/tutorial/)
* Modifying hardhat configuration file, add ICE testnet entries to _<mark style="color:blue;">hardhat.config.js</mark>_ file in the url parameter.

```
require("@nomiclabs/hardhat-waffle");
const ICE_PRIVATE_KEY = "your private key";
module.exports = {
  solidity: "0.7.3",
  networks: {
    testnet: {
      url: `http://51.158.117.160:9933`,
      accounts: [`0x${ICE_PRIVATE_KEY}`]
    }
  }
};

```









*
