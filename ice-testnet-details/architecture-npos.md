---
cover: ../.gitbook/assets/ICE-Cicles (2).gif
coverY: 0
---

# Architecture: NPoS

**Nominated Proof of Stake (NPoS)** is a blockchain consensus mechanisms. Consensus mechanisms, in simple terms, are algorithms that ensure all the nodes participating in a network are synchronized with same data and transactions.

Proof-of-stake minimizes the amount of computing labor required to validate blocks and transactions that ensure security of the blockchain . Proof-of-stake alters the way blocks are confirmed by native token owners' devices. The owners submit their currencies as collateral in exchange for the ability to validate blocks. Owners of staked coins are referred to as "validators”. A coin owner must "stake" a certain quantity of coins to become a validator.

**Nominated Proof of stake** is a type of scheme used to select validators who are allowed to participate in the consensus protocol. NPoS is a Proof-of-Stake variant that is utilized in Substrate-based Blockchains. The main actors involved in NPoS are: **Validators** and **Nominators**.

**Validators** are responsible for the network's infrastructure and operation. They are in charge of creating new blocks, validating blocks, ensuring finality, and ultimately ensuring the network's security. They must be responsive at all times and maintain a secure, dependable infrastructure. Furthermore, validators require tokens to back them up, which encourages them to follow the rules because a portion of these tokens may be taken away otherwise (called slashing). Validators are compensated for their services with incentives priced in the native token of the underlying network (e.g. ICY on ICE and ICZ on Snow).

**Nominators** are token holders who contribute to the network's security by supporting the validators of their choosing with their stakes (tokens). A nominator publishes a list of validator candidates in whom he/she has faith and stakes a certain amount of native tokens in order to endorse them. If some of these candidates are elected as validators, he/she divides the payouts or penalties on a per-staked-native token basis with them. Nominators, unlike validators, can have a limitless number of participants. As long as a nominator is careful in his/her selection and only supports validator candidates who follow solid security standards, his/her function is low risk and offers a steady source of funding.

This nominator-validator configuration provides high security assurances. It enables the system to choose validators with vast aggregate stakes far more than any single party's native token holdings and exclude candidates with little stake. In fact, it can be anticipated that a significant portion of total native token supply will be staked in NPoS at any one time. This makes it extremely difficult for a hostile entity to elect validators (since they must first establish a good reputation in order to obtain the necessary backing) and extremely expensive to attack the system (because any attack will result in large amounts of tokens being slashed).

### **NPoS on ICE and Arctic Network**

**The Arctic test network is POA(Proof Of Authority) at the moment (Later it will make transition to NPoS)**. It will use the NPoS to reach consensus among the network validators. This is achieved by using the consensus engine [Aura](https://docs.substrate.io/v3/advanced/consensus/#aura)  provided by the [Substrate](https://substrate.io/)  framework, along with [Cumulus extension pallet for Aura](https://paritytech.github.io/cumulus/cumulus\_pallet\_aura\_ext/index.html) which makes the Arctic network compatible with parachains.\
\
The same consensus mechanism will be adopted by Snow and ICE network.

{% hint style="info" %}
**References:**

****[**https://stakingfac.medium.com/what-is-nominated-proof-of-stake-889fc22bef8f**](https://stakingfac.medium.com/what-is-nominated-proof-of-stake-889fc22bef8f)****

****[**https://www.investopedia.com/terms/p/proof-stake-pos.asp**](https://www.investopedia.com/terms/p/proof-stake-pos.asp)****
{% endhint %}
