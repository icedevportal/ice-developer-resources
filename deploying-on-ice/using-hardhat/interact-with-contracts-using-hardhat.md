---
description: >-
  This article will show you how to interact with recently deployed smart
  contract on ice using hardhat
---

# Interact with contracts using hardhat

* Launch hardhat console by running:

```
npx hardhat console --network testnet
```

* Then, one by one, add the following lines of code. To begin, we construct a local instance of Token.sol contract

```
const Token = await ethers.getContractFactory('Token')
```

Next, connect this instance to an existing one by passing in the address we obtained when deploying the contract

```
const token = Token.attach('0x1680F8C98136F8D4C470fe01c7487fe1051FA1A4')
```

* Let’s call the methods of the contract now First transfer some tokens to a address by calling transfer() from contract

```
await token.transfer('0x223fe7e9cA68fDB858cf8397870E61d4b58f3A0A', 10)
```

* Then check the balance of available tokens in the address by calling balanceOf() mehtod

```
await token.balanceOf('0x223fe7e9cA68fDB858cf8397870E61d4b58f3A0A')
```

This should output 10 in the cosole.
