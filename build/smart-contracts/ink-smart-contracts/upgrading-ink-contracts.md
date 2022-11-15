# Upgrading Ink! contracts

### Upgrading Ink Contracts&#x20;

Smart contracts are by default immutable in nature. Once uploaded to the chain, we cannot change its runtime logic or storage structure. This is an inconvenience since upgrades are common in software development. Even though the original contract is immutable, we can perform an upgrade of the contract by alternative means. Currently, there are three separate mechanisms to upgrade a contract that can be used according to the suitable use case.

#### 1. Forwarding Calls (Proxy Pattern)&#x20;

In this upgrade mechanism, we upload a new proxy contract with a mechanism to forward calls that are not implemented in the proxy contract to the actual contract. For this, we would need to set the actual contract account ID as `Proxy.forward_to`, for the call forwarding. Since we are setting the Contract Address to forward calls in the proxy contract, the actual contract must be deployed first.

If we deploy V2 of the contract with new methods, we can set the `Proxy.forward_to` parameter in the Proxy contract, with the address of the V2 contract. After that, all the calls to the Proxy contract would be directed to V2.&#x20;

Migrating the storage V1 to V2 falls under the responsibility of the V1/V2 contract developers.

**Example Code:** [Forward Call](https://github.com/paritytech/ink/tree/master/examples/upgradeable-contracts/forward-calls)

<figure><img src="../../../.gitbook/assets/image (2) (3).png" alt=""><figcaption><p>Forwarding Calls (Proxy Pattern)</p></figcaption></figure>

#### 2. Delegate Calls&#x20;

This is similar to forward calls pattern. The only difference is that the unmatched calls are delegated using the upgraded contracts code hash. Since code hash can also be updated, the smart contract can be upgraded any number of times. The V1/V2 contracts does not need to be deployed (call the constructor) after uploading, since the proxy contract calls the V1/V2 contract using the code hash. The storage is lazy initialized using the `Upgradeable` wrapper trait.

**Example Code**: [Delegate Call](https://github.com/paritytech/ink/tree/master/examples/upgradeable-contracts/delegate-calls)

<figure><img src="../../../.gitbook/assets/image (6) (2).png" alt=""><figcaption><p>Delegate Calls</p></figcaption></figure>

#### 3. Update Runtime&#x20;

This is the simplest approach to upgrading an Ink! contract. In this approach, we change the runtime execution code of a contract by changing its code hash to that of a new contract. It is basically replacing the old contract with new runtime logic. **Example Code**: [Set Code Hash](https://github.com/paritytech/ink/tree/master/examples/upgradeable-contracts/set-code-hash)

<figure><img src="../../../.gitbook/assets/image (1) (3).png" alt=""><figcaption><p>Update Runtime</p></figcaption></figure>

### Upgrading Storage&#x20;

There is no straightforward way to upgrade existing storage in case of a change in the storage existing layout of a contract. If we need to upgrade a contract with changes in layout data structure, then the most accessible path would be to use a forward-calls pattern in which the upgraded contract initializes its own storage and imports old records from previous contract storage. Developers would need to write their own data migration procedure for this.
