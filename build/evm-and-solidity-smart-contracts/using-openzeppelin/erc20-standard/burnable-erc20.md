# Burnable ERC20

Burnable ERC20 adds a new feature to standard ERC20 tokens that let people who have a lot of ERC20 coins destroy both their own coins and those they have an allowance for, in a way that can be seen off-chain. So burning the token implies a reduction of the total supply. But on the other hand, blockchains are immutable, so making an ERC20 burnable is achieved by sending the tokens to an address whose private keys aren't accessible to anyone and subtracting the number from the total supply in our contract.

Let's look at a burnable ERC20 token smart contract generated using [OpenZeppelin Wizard](https://wizard.openzeppelin.com).

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";

contract MyToken is ERC20, ERC20Burnable {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 10000 * 10 ** decimals());
    }
}
```

Here we have created a burnable ERC20 token by inheriting the properties of class **ERC20Buranable,** which provides some extra functions, which can be imported from [openzeppelin/contracts](https://openzeppelin.com/contracts/) library. We have initialized the token with the name 'MyToken', symbol 'MTK', and a pre-mint value of 10000 tokens issued in name of contract deployer's address.

### Methods

**burn(amount)**

It destroys the amount of tokens from the caller's account thus reducing the total supply.

**burnFrom(account, amount)**

It destroys `amount` tokens from `account`. `amount` is then deducted from the caller's allowance.

You can also compile, deploy, and interact with the above smart contract using Remix IDE as shown [here](../../using-remix/).

### Reference

[https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Burnable](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Burnable)



