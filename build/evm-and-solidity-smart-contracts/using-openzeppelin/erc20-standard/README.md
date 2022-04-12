---
description: In this article, we will learn to create different ERC20 standard tokens
---

# ERC20 standard

ERC20 is the technical standard underlying smart contracts that allow tokens to be implemented on the Ethereum based blockchains. A token hosted on the Ethereum based blockchain can be transferred, received, its overall supply checked, and the quantity available on an individual address checked. So, an ERC20 token contract keeps track of fungible tokens, which means that every one token is precisely equivalent to any other token i.e. no tokens have unique rights or behavior. As a result, ERC20 tokens may be used as a medium of exchange for money, voting rights, staking, and other purposes.

OpenZeppelin contracts provides a standard to build ERC20 tokens on EVM-based blockchains such as ICE.

You can find detailed information on property and its usage regarding the ERC20 token in [api reference](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20) page of the ERC20 token provided by openZeppelin contracts

The functions `balanceOf`, `totalSupply`, `transfer`, `transferFrom`, `approve`, and `allowance` are defined in ERC20. Apart from these, there are other getters functions like `name` and `symbol.`

Below is a brief description of a standard ERC20 contract:

```
contract ERC20 {
   function totalSupply() constant returns (uint theTotalSupply);
   function balanceOf(address _owner) constant returns (uint balance);
   function transfer(address _to, uint _value) returns (bool success);
   function transferFrom(address _from, address _to, uint _value) returns (bool success);
   function approve(address _spender, uint _value) returns (bool success);
   function allowance(address _owner, address _spender) constant returns (uint remaining);
   event Transfer(address indexed _from, address indexed _to, uint _value);
   event Approval(address indexed _owner, address indexed _spender, uint _value);
}
```

* **totalSupply:** It returns the total amount of token supplied
* **balanceOf:** It returns balance of account with address `_owner`
* **transfer:** It transfers `_value` amount from contract owner address to address `_to.`
* **transferFrom:** It enables a smart contract to automate the transfer procedure and transmit a specified quantity of the token on the owner's behalf. It returns a failed transaction unless the `_from` account has deliberately authorized the sender of the message.
* **approve:** It allows `_spender` to withdraw from your account, multiple times, up to the `_value` amount. If this function is called again it overwrites the current allowance with `_value`.
* **allowance:** It returns the amount which `_spender` is still allowed to withdraw from `_owner.`
* **event Transfer:** It is triggered when tokens are transferred.
* **event Approval:** It is triggered whenever `approve(address _spender, uint256 _value)` is called.

In this article, we will be using [OpenZeppelin Wizard](https://wizard.openzeppelin.com) to create **mintable**, **burnable** and **pausable** ERC20 standard smart contract.

{% hint style="info" %}
_Learn about components of OpenZeppelin wizard from_ [_here_](../#openzeppelin-contract-wizard)__
{% endhint %}

{% content-ref url="mintable-erc20.md" %}
[mintable-erc20.md](mintable-erc20.md)
{% endcontent-ref %}

{% content-ref url="burnable-erc20.md" %}
[burnable-erc20.md](burnable-erc20.md)
{% endcontent-ref %}

{% content-ref url="pausable-erc20.md" %}
[pausable-erc20.md](pausable-erc20.md)
{% endcontent-ref %}
