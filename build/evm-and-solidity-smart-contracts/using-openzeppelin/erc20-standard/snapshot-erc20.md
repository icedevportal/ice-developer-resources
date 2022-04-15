# Snapshot ERC20

Snapshot ERC20 contract adds a snapshot mechanism to an ERC20 token. When a snapshot is taken, the current balances and total supply are saved for future use. Now, these tokens can be queried at any point in time.

Snapshots are frequently utilized before each cycle of airdrop events. Tokens are given during an airdrop based on the balance of each blockchain address. In this situation, snapshots are taken to record each token holder's balance at a certain point in time (i.e., block height)

Let's look at a simple Snapshot ERC20 token smart contract created using [OpenZeppelin Wizard](https://wizard.openzeppelin.com)

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Snapshot.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, ERC20Snapshot, Ownable {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 10000 * 10 ** decimals());
    }

    function snapshot() public onlyOwner {
        _snapshot();
    }

    // The following functions are overrides required by Solidity.

    function _beforeTokenTransfer(address from, address to, uint256 amount)
        internal
        override(ERC20, ERC20Snapshot)
    {
        super._beforeTokenTransfer(from, to, amount);
    }
}
```

Here, we have created a Snapshot ERC20 token initialized with the token name 'MyToken', symbol 'MTK', and a pre-mint value of 10000 tokens.

### Methods

**snapshot()**

It creates a new snapshot by calling the internal function `_snapshot` and returns its **snapshot id.**

**\_**`snapshot` function emits a **Snapshot** event that contains the same id.

**totalSupplyAt(snapshotId)**

It returns the total supply at the time of a snapshot with **snapshotId**

**balanceOfAt(account, snapshotId)**

It returns the balance of an account at the time of a snapshot with **account address** and **snapshotId.**

Now, you can also go on and compile, deploy and interact with the above smart contract code in Remix IDE by following the steps shown [here](../../using-remix/)

### Reference

[https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20Snapshot](https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20Snapshot)
