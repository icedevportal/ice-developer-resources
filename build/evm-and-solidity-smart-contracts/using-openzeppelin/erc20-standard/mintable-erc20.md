# Mintable ERC20

Mintable ERC20 tokens are those that follow the ERC20 standard completely. As a result, they have an additional property that distinguishes them from other tokens i.e. mintable tokens enable us to issue additional tokens at any moment, thereby, expanding the supply.

Only contract deployer can mint new tokens

Let's look at a simple mintable ERC20 token smart contract created using [OpenZeppelin Wizard](https://wizard.openzeppelin.com/)

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 10000 * 10 ** decimals());
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

Here we have created a mintable ERC20 token by initializing the token name as 'MyToken' , the symbol as 'MTK', and a pre-mint value of 10000 tokens through the constructor.

### Methods

**mint(to, amount)**

This function creates `amount` of token assigned to the address `to` by calling `_mint` function. Here only contract deployer is the minter.

Now you also compile, deploy and interact with the above smart contract using Remix IDE as shown [here](../../using-remix/).

### Reference

[https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Mintable](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Mintable)
