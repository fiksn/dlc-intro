## Discreet Log Contracts

is a wordplay on the "discrete logarithm problem" and the fact that contracts are discreet. There is no sign of a smart contract on the blockchain. Also the oracle is not aware of who is using his data. The scheme was presented in the paper [Discreet Log Contracts](https://adiabat.github.io/dlc.pdf) by Thaddeus Dryja who is also one of the creators of Lightning network.

[Alternative expanation](https://atomic.finance/blog/a-laypersons-guide-to-discreet-log-contracts-atomic-yield-series-part-3/)

### Refresher (Schnorr signatures)

s = k - hash(message || R || P) * d

R = k*G

### Problem statement

Alice and Bob want to bet against each other. They could create 2-of-2 multisig, but what if loser is not cooperating?

In 2-of-3 multisig they need an oracle (Olivia). However how to make sure she doesn't collude with the loser?

You could use smart contracts (e.g., on Ethereum) but this is expensive and not very private. Enter DLCs on Bitcoin.

### Operations

Olivia just publishes one R for that particular bet (she commits to a R value). All possible outcomes need to be known and agreed upon in advance!

Else Olivia has no idea who will use her data.

Now anyone can calculate
si * G. 

Let's say the bet is "heads" vs. "tails".

so 
- sHEADS * G = R - hash("heads" || R)*O
- sTAILS * G = R - hash("tails" || R)*O

R is the published value, O is Olivias public key

this values (points on the eliptic curve) are called **encryptors**

### Channel

For Alice and Bob it is very similar to opening a lightning channel: they create a 2-of-2 multisig.

#### Bailout

Before that block is transmitted to the blokchain Alice and Bob make sure each peer signs a bailout transaction. So Alice can whitdraw her part after a timelock, and vice-versa for Bob.

#### Contract

Alice bets on "heads" and creates an output from that UTXO that can be spent using the private key for some public key Ai that is defined as A + sHEADS * G

That is her public key but skewed with an encryptor (sHEADS * G) which is publicly known (depending on R from Olivia). She signs the transaction, but without Bob's signature that can't be broadcasted to the network.

Bob verifies that the value is correct and signs the transaction Alice gave him (since he knows Alice can't possibly know the private key and will know it just if she won).

Then also Bob creates a spend from the multisig: he uses bi and in the tx you can see public key Bi which is B + sTAILS * G. Now Alice verifies the same way and eventually signs.

Those two transactions are never broadcasted on-chain (similar to bailout tx).
They are called **contract execution transactions (CETs)**.

#### Settlement

Olivia reveals either sHEADS or sTAILS. If she reveals both of them (or more than one in case there more than two options) her private key is compromised (can be factored out since same R and thus also k was used).

Only she can reveal them because o (her private key) must be used for signing.

Say Olivia publishes sHEADS.

Now Alice can compute private key ai which is just a + sHEADS.
Only she knows her private key a, so this value doesn't help anyone.
But she can now sweep the funds. 

In fact she has to, because if she waits time-lock could expire and Bob could
get his stake back (due to the presigned "bailout" transaction).

If Olivia just disappears after time-lock both Alice and Bob get their stake back.

#### Problems

Olivia has no incentive to publish the results, it is only her reputation that suffers.

She must use a random k each time. Using the same k twice - she loses her private key.

If must be possible to enumerate all possible outcomes in advance (for price this can get messy). You can then use a certain discretization.

Only one outcome can win (or none), if there are combinations you need to create a power-set. (User can still bet on multiple outcomes, but care has to be taken by peers if that creates a sure bet). 

E.g. Bob woudn't sign Alice a bet on "heads" and then also "tails", since he knows this way he will just lose his money.

#### Usages

- [Atomic.Finance](https://atomic.finance) uses DLCs to implement covered calls to earn income on your BTC without giving up custody
- [SuredBits](https://suredbits.com) - they also have [oracles](https://oracle.suredbits.com/) and presented something called [Discrete Log Contract for Difference - DLCFD](https://suredbits.com/settlement-of-dlcfd/)

[Previous - Schnorr](./schnorr.md) 