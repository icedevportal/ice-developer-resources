# Using OpenZeppelin

OpenZeppelin is a open source framework built of reusable Ethereum smart contracts. The framework enables smart contract developers to limit the risk of vulnerabilities in their distributed applications (dapps) by utilizing standard, tested, community-reviewed code. It provides security tools to develop, automate, and run decentralized applications. All of OpenZeppelin's contracts and libraries may be deployed without any changes because of ICE's Ethereum compatibility.

Find more information about OpenZeppelin on their [documentation site](https://docs.openzeppelin.com/openzeppelin/).

Here we will look how to create ERC721 and ERC1115 standard NFT tokens using openZeppelin

You can also generate a basic smart contract code using [OpenZeppelin Contract Wizard](https://wizard.openzeppelin.com).

&#x20;[OpenZepplin Contracts Wizard](https://wizard.openzeppelin.com) is an online web-based interactive contract generating tool, which is arguably the simplest and quickest method to develop your smart contract using OpenZeppelin code.

### OpenZeppelin Contract Wizard

![OpenZeppelin Contract Wizard](https://lh4.googleusercontent.com/8rxyWY9FlwSU-b5AIoiuBGraGJRB-VgMhLa3i4dWlAS3ZRS-gN6O-dUBxfAJ\_BapAXXHCBoBBBTjs19xt6WkqqKsBiNxiz2gSQNQ3wubxezZeu5\_zsEk9nRHD6Cd7zfqS8QBJ9g2)

As we can see, openzeppelin contract wizard is divided into various parts:

1. **Token standard:** Shows different standards token provided by the wizard
2. **Settings:** Provides base setting for each standard like name, symbol,pre-mint value, base uri, etc.
3. **Features:** Provides list of features for every token standard
4. **Access Control:** a list of all the access control techniques available for each token standard
5. **Upgradability:** Provides contract upgradability features.
6. **Info:** Provides fields where people can contact the contract creator for any issue and another field for license
7. **Code display area:** displays the smart contract code with the user-specified parameters.

### Simple ERC721 token

NFTs are a new type of digital assets. They are non-fungible tokens which means that each token is unique, meaning that no two tokens are alike. The NFTs can represent ownership of in-game items, physical assets, or even just data. This special type of Token has amazing possibilities so it deserves a proper Standard, the ERC-721 came to solve that!

This unique sort of Token has incredible potential, and it demands a suitable standard; the ERC-721 was created to address this issue!

The ERC-721 sets a standard for NFT, which means that this type of Token is distinct and may have a different value than another Token from the same Smart Contract, maybe related to its age or rarity.



The ERC721 smart contract below is created using contract wizard:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC721, Ownable {
    constructor() ERC721("MyToken", "MTK") {}

    function _baseURI() internal pure override returns (string memory) {
        return "test";
    }

    function safeMint(address to, uint256 tokenId) public onlyOwner {
        _safeMint(to, tokenId);
    }
}
```

It is a simple ERC721 mintable token which provides a `mint` function that can only be called by the owner of the contract. By default, the owner is the contract's deployer address.

You can go on and deploy this contract on frost testnet using Remix IDE by following this [link](using-remix/).

### GameCard NFT

Now Let's use ERC721 standard to create a collectables called 'GameCard'. Each GameCard will be owned by someone. Here we will provide a 'GameCard' to a player. i.e. Each card will be minted and sent to the player's address. Players have the option of keeping their token or transferring it to other players.

Here's what contract looks like:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract GameCard is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    constructor() ERC721("GameItem", "GIT") {}

    function createItem(address player)
        public
        returns (uint256)
    {
        _tokenIds.increment();

        uint256 newItemId = _tokenIds.current();
        _safeMint(player, newItemId);

        return newItemId;
    }
}
```

Here the GameCard token is initialized with a token name **GameItem** and a symbol **GIT** through the constructor.

**Counter** is also imported from openZeppelin which is a simple way to get a counter that can only be incremented or decremented.

**CreateItem** function simply mints the token to the given adderess and returns the tokenId if the minted item



{% hint style="info" %}
&#x20;_Currently any account can call `createItem` to mint items. To restrict what accounts can mint items we can add_ [_Access Control_](https://docs.openzeppelin.com/contracts/4.x/access-control)_._
{% endhint %}

Now you go on and deploy above contract in frost testnet using Remix IDE in injected web3 environment as demonstrated [here](using-remix/).

### ERC1155 token standard

ERC1155 is a multi-token standard that enables the production of fungible, non-fungible, and semi-fungible tokens in a single contract. Prior to ERC1155, if a use case required both ERC20 (fungible) and ERC721 (non-fungible) tokens, two contracts were necessary. ERC1155 also enables the launch of several NFT collections in a single smart contract rather than developing a separate contract for each collection.

ERC1155 is commonly used in blockchain-based decentralized games, which require currencies and collectibles, hence it has become a standard there.

Here We will create 3 NFT collections (Shield, Arrow, and Hammer) with a single NFT in each one.

The smart contract code looks like:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";

contract Weapon is ERC1155 {
    uint256 public constant Shield = 1;
    uint256 public constant Arrow = 2;
    uint256 public constant Hammer = 3;

    constructor() ERC1155("test") {
        _mint(msg.sender, Shield, 1, "");
        _mint(msg.sender, Arrow, 1, "");
        _mint(msg.sender, Hammer, 1, "");
    }
}
```

In the above smart contract code:&#x20;

First ERC1115 is imported from openZeppelin.

Then we have created out contract named **Weapon** and also created three variables Shield, Arrow and Hammer assigning each with a unique id.

Then we have initialized the constructor by passing tokenUri(_in our case 'test'_) which mints the different NFTs by calling function `_mint` passing the following params in it:

* **msg.sender** is the address on which token will be minted. It is also the address of contract deployer.
* Second parameter is token id  which we have already assigned names, so using names here.
* Amount of each token, here we are minting 1 token each.
* The last parameter is the data field which is kept empty here.

Now lets head over to [**Remix IDE**](https://remix.ethereum.org) to compile and deploy our NFT.

In a workspace, create a file named **`Weapon.sol`**

![Create contract file](../../.gitbook/assets/weapon1.png)

Now navigate to Compile tab on from left navigation and click on **Compile Weapon.sol** button

![Compile smart contract](../../.gitbook/assets/weapon2.png)

**Deploy:**

1. Navigate to **Deploy and Run Transaction** tab
2. Select the environment as **Injected Web3**
3. Select **Weapon.sol** contract
4. Click on **Deploy**
5. Now it will pop up metamask to confirm the transaction, **Confirm** it.

![Deploy ERC1115 Token](../../.gitbook/assets/weapon3.png)

Now that the contract is deployed you can interact with it methods.
