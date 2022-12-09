# XCM Integration Guide

ICE Network has recently added support for XCM to the Arctic Testnet. XCM is an essential layer of the Polkadot technology stack which enables Cross-Consensus Messaging with other parachains. As part of this development, we will gradually roll out integration plans with partner parachains on Kusama, and eventually Polkadot.

In this first article, we will provide a walkthrough of the steps required to integrate XCM and test messaging transfer scenarios. In the following series of articles, we will explain XCM in some more detail and do a deep dive into XCM runtime implementation.

### Integration Instructions <a href="#_li753nkt27qd" id="_li753nkt27qd"></a>

A key point to be aware of is that XCM itself is a messaging format, not a protocol; this is a distinction between VMP (Vertical Message Passing) and XCMP (Cross-Chain Message Passing).

Currently, parachain to parachain communication is enabled by opening a unidirectional connection known as the HRMP channel.

### Add HRMP Channels <a href="#_j2o4uub8lqsx" id="_j2o4uub8lqsx"></a>

The following instructions apply to [Arctic Testnet](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Farctic-rococo-rpc.icenetwork.io#/explorer) on Rococo; it's also recommended that both teams test the integration locally first with the arctic-dev setup using a copy of the [arctic-karura](https://github.com/web3labs/ice-substrate/blob/main/resources/arctic-karura.json) polkadot-launch configuration and replace karura-dev with the target parachain.

1. Calculate and fund your parachain's sovereign account on Rococo
2. Open an HRMP channel
3. Accept the HRMP channel

As stated earlier, HRMP are unidirectional channels; each parachain is required to repeat the above 3 steps to complete a single channel registration.

Using [this](https://github.com/web3labs/ice-substrate/blob/main/scripts/xcm-utils/hrmp.js) hrmp utility script, we perform all 3 steps after modifying these parameters:

* relayWS: relay chain WebSocket endpoint
* sender paraId
* recipient paraId
* sender endpoint
* recipient endpoint

#### Calculate and fund your parachain's sovereign account <a href="#_b3twf4kjdura" id="_b3twf4kjdura"></a>

The following JavaScript snippet calculates and funds paraId 2000

```
let soverign_account_2000 = get_parachain_soveriegn_account(2000)

await fund(api,soverign_account_2000, new BN(9*1e15))
```

**Note**: On the official Rocco Sovereign Account’s address, please fund your sovereign account using the [Rococo faucet](https://wiki.polkadot.network/docs/build-pdk#obtaining-roc).

#### Open an HRMP channel <a href="#_dpgfr76gy0px" id="_dpgfr76gy0px"></a>

Initiate an open HRMP request between sender, paraId 2000, and recipient, paraId 2001

```
await open(2000, 2001, senderWsEndpoint)
```

This function performs 3 actions as explained in this [tutorial](https://docs.substrate.io/reference/how-to-guides/parachains/add-hrmp-channels/):

1. Prepares _**** hrmpInitOpenChannel_ call for the recipient, and encodes it on the relay chain.
2. Executes the encoded call with _polkadotXcm.send_ on the **sender** parachain via sudo, which in turn sends an upward message to the relay chain.

#### Accept HRMP channel request <a href="#_9c8ykco8bxki" id="_9c8ykco8bxki"></a>

To accept an HRMP channel request on the recipient, the following JavaScript snippet performs the required steps:

```
await accept(2000, 2001, recipientWsEndpoint)
```

1. Prepares _hrmpAcceptOpenChannel_ call for the sender, and encodes it on the relay chain.
2. Executes the encoded call with _polkadotXcm.send_ on the **recipient** parachain via sudo, which in turn sends an upward message to the relay chain

To verify that channel registration is successful, look at Developer -> ChainState -> hrmp -> hrmp.hrmpChannels

![](../.gitbook/assets/0)

### Asset Transfer Example <a href="#_dfe93kwrwppk" id="_dfe93kwrwppk"></a>

To have a fully realistic Asset Transfer setup between two parachains it must have bidirectional communication, meaning channels two should be open, one from 2000 to 2001 and the other from 2001 to 2000.

The setup described above should then be made one additional time, para 2001 being the source. After doing this, the relay chain can be used to check to see if both the channels have been opened.

![](../.gitbook/assets/1)

For two parachains to be able to send assets from one to another, they must know how assets are represented to be able to correctly handle and interpret messages from one another.

In this example, we will use the native token of the relay chain to demonstrate how transfers can be made from all relay to para, para to para, and para to relay flows.

First, we will transfer some tokens from the relay chain to para 2000. Transferring tokens from relay to para do not the require manually opening of a hrmp channel, since this happens automatically, so we just need to use xcmPallet (vanilla version) to send the tokens.

![](../.gitbook/assets/2)

<figure><img src="../.gitbook/assets/3" alt=""><figcaption></figcaption></figure>

Checking on the destination para 2000, we should be able to see that the transfer succeeded. This type of transfer, from the relay chain to the parachain is generically called a **DownwardMessage**. We can see that Alice’s account has been funded with KSM tokens. Another interesting thing is that another account has been also funded with a small amount of KSM tokens from the initial chunk sent. That account is the treasury account and has been funded with the transaction fee, which has also been paid in KSM. The amount of KSM tokens considered as fees as well as the destination account that will be funded with the fees are configurable and each parachain can do its own configuration.

![](../.gitbook/assets/4)

Now that Alice on para 2000 has some KSM tokens, we can go ahead and send some of them to Alice on para 2001. To do this, we are going to be using xTokens instead of xcmPallet. xTokens is a wrapper over the vanilla xcm and is meant to ease the interaction with the confusing generic Junctions parameters of the original xcm interface.

![](../.gitbook/assets/5)

Keep in mind that we are able to send KSM because both sender and receiver parachains know how to represent, handle, and interpret messages representing KSM transfers. Later, when we get to Asset Registration, we will see how we can dynamically register tokens without having to hardcode them into the runtime code.

Checking para 2001, swe should be able to see the transfer succeeded.

![](../.gitbook/assets/6)

Sending them back to Alice on para 2000 should also bring no problems:

![](../.gitbook/assets/7)

![](../.gitbook/assets/8)

And lastly, we should be able to send them back to Alice on the relay chain.

![](../.gitbook/assets/9)

Checking Alice’s balance on the relay chain we could see that it increased with \~10 (minus the fees) KSM.

![](../.gitbook/assets/10)

This type of transfer is called generically an Upward Message.

![](../.gitbook/assets/11)

Later, when we get to the implementation details, we will see why the relay chain interprets the tokens as UNITS and why the two parachains as KSM.
