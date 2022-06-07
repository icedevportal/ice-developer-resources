---
description: Swap between native blockchain token(ICZ) and ERC-20 token.
---

# Swap on ICE Blockchain

In this example, we will be creating a Dapp that will allow a user to swap tokens on the ICE network. For this example, we will be able to swap native ICZ token with a ERC-20 (USDC) token and vice versa.

### Implementation of contracts

#### **ERC-20 Contract**

For the implementation of swap we start by implementing a ERC-20 standard token. We can make use of [openzeppelin ](https://github.com/OpenZeppelin/openzeppelin-contracts)library to kickstart our custom ERC-20 contract, named `USD Coin` and symbol `USDC` that mints 1000\*10\*\*18 tokens at the deployer address.

```
pragma solidity >=0.8.0 <0.9.0;
//SPDX-License-Identifier: MIT

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract USDC is ERC20 {
  constructor() ERC20("USD Coin","USDC") {
      _mint(msg.sender,1000*10**18);
  }
}
```

#### **SwapContract**

SwapContract is the main contract that swaps the default blockchain token and our custom ERC-20 token, USDC. To keep things simple, we will swap 1 USDC for 1 ICZ.

We will be implementing two specific methods:

1. **Buy:** The user can buy USDC (ERC20 token) with ICZ.
2. **Sell:** The user can sell USDC and get ICZ in return.

For the implementation of SwapContract, we utilize the SafeMath library that helps to prevent overflow and underflow as well as by creating a ERC20 interface that has to be set during the creation of SwapContract.

```
pragma solidity >=0.8.0 <0.9.0;
//SPDX-License-Identifier: MIT

import "hardhat/console.sol";

import "@openzeppelin/contracts/utils/math/SafeMath.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract SwapContract{
    using SafeMath for uint256;
    IERC20 token;

    event Bought(address by, uint256 amount);
    event Sold(address by, uint256 amount);

    constructor(address token_addr) {
        token = IERC20(token_addr);
    }
}
```

#### **Implementing Buy**

In order to buy USDC, we first verify two things**:**

1. &#x20;**** Some ICZ is provided in order to buy USDC
2. There is enough USDC that can be bought for the provided ICZ

If the above condition matches, the user can buy USDC for ICZ.

```
function buy() public payable {
   uint256 amountToBuy = msg.value;
   uint256 swapcontractBalance = token.balanceOf(address(this));
   require(amountToBuy > 0, "You need to send some ICZ");
   require(amountToBuy <= swapcontractBalance, "Not enough tokens in the reserve");
   token.transfer(msg.sender, amountToBuy);
   emit Bought(amountToBuy);
}
```

#### **Implementing Sell**

The logic to implement sell is quite similar to that of buy. We verify that:

1. Some amount of USDC is provided.
2. There is enough ICZ in the reserve such that the provided amount of USDC can be sold.

Apart from the following, we also have to verify that the sender has approved the **SwapContract** for transferring the amount on its behalf.

```
function sell(uint256 amount) public {
   require(amount > 0, "You need to sell at least some tokens");
   uint256 allowance = token.allowance(msg.sender, address(this));
   require(allowance >= amount, "Check the total allowance");
   uint256 swapcontractBalance = address(this).balance;
   require(amount <= swapcontractBalance, "Not enough ICZ in the reserve");
   address payable user = payable(msg.sender);
   user.transfer(amount);
   token.transferFrom(msg.sender, address(this), amount);
   emit Sold(amount);
}
```

Finally, in order to receive ICZ for the contract, we have to implement a receive method. It can be implemented with a single line of code.

```
receive() external payable {}
```

#### &#x20;**SwapContract Implementation**

The full implementation of the code can be found in [Github](https://github.com/icondev99/DEX/).

### **Interacting with the contract**

#### **Deploying contracts**

We can deploy our contracts by following the instructions as provided in [**using hardhat**](../using-hardhat/)****

We can create a deploy script to deploy the contract.

```
async function main() {
    const [deployer] = await ethers.getSigners();
  
    console.log("Deploying contracts with the account:", deployer.address);
  
    console.log("Account balance:", (await deployer.getBalance()).toString());

    // Deploy necessary contracts
    const USDC = await ethers.getContractFactory("USDC");
    const usdc = await USDC.deploy();
    console.log(`Deployed USDC at ${usdc.address}`)
  
    const SwapContract= await ethers.getContractFactory("SwapContract")
    const swapcontract = await SwapContract.deploy(usdc.address);
    console.log(`Deployed SwapContract ${swapcontract.address}`)

}
  
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
});
```

We can save the addresses and then interact with them at a later time by attaching with the deployed address through the console.

```
npx hardhat console --network testnet
```

Now that we have our console opened, we can create a local instance of our ERC-20 contract, USDC with

```
const USDC = await ethers.getContractFactory('USDC')
```

We can connect this local instance to the USDC contract we have already created by passing the contract address that we have saved earlier.

```
const usdc = await USDC.attach('0x7E1874B97e4f7B1Caf5559eB3dd0f33b2A68B8b2')
```

To be sure that the connection is established, we can invoke the balanceOf method described for ERC-20.

```
await usdc.balanceOf(swapcontract.address)
```

In the similar way, we can connect the local instance of **SwapContract** with the one that has already been deployed.

```
const SwapContract= await ethers.getContractFactory('SwapContract')
const swapcontract = await SwapContract.attach('0x7513F77F645F2002f3477Dce9d3aF761E7d1d43B')
```

#### **Buying USDC**

Since all the tokens are minted to the deployer address, some of the tokens need to be sent to the **SwapContract** for the contract to function. This can be achieved by:

```
await usdc.transfer(swapcontract.address, 1000)
```

With some USDC in the **SwapContract**, any user can now buy USDC by sending ICZ.

```
await swapcontract.buy({value: 100})
```

#### **Selling USDC**

Now that we have some USDC, we can sell them to get ICZ back. It should be noted that sufficient ICZ must be in the SwapContract. ICZ can be supplied to the **SwapContract** through the console by:

```
let tx = {to: swapcontract.address, value: 1000}
myWallet = await ethers.getSigner()
await myWallet.sendTransaction(tx)
```

#### Using Metamask

Alternatively, we can use Metamask or other wallets to directly transfer some ICZ to the **SwapContract**.

1. You can configure your metamask to **Arctic** testnet network by following this [link](../../../ice-testnet-details/network-endpoints/interacting-with-arctic-using-metamask.md)
2. Send amount to contract - (use swapcontract.address)

![](<../../../.gitbook/assets/image (1) (2).png>)

After verifying there is some ICZ in the **SwapContract**, we can now sell our USDC. Before moving on with selling we must approve our **SwapContract** such that the transfer can be made on behalf of us.

```
await usdc.approve(swapcontract.address, 100)
```

After approving DEX in the USDC, we can now finally sell USDC.

```
await swapcontract.sell(100)
```
