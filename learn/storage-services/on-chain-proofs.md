# On-Chain Proofs

First, please allow me to set some context about Solana itself… At the most basic fundamental level, blockchains are nothing more than ledgers. Ledgers record the history of how things have changed over time and all of those changes combined give you the current “state”. Solana is all about its “accounts” and the “state” of those accounts.

What do I mean by “state”? Let’s use computers as an example… Everything in a computer is 0’s and 1’s. The bit stores just a 0 or 1: it’s the smallest building block of storage. **If a bit is a 1 then its current state is 1. If a bit is 0 then its current state is 0.** That bit is either a 0 or a 1, the history of that bit is not relevant to whether that bit’s state is currently a 0 or a 1.

The next thing we need to know is that Solana is unique in the way it structures everything as an “account.” This is important terminology, so here’s the definition:

{% code overflow="wrap" %}
```
Accounts
Storing State between Transactions
If the program needs to store state between transactions, it does so using accounts. Accounts are similar to files in operating systems, such as Linux, in that they may hold arbitrary data that persists beyond the lifetime of a program. Also, like a file, an account includes metadata that tells the runtime who is allowed to access the data and how.

Unlike a file, the account includes metadata for the lifetime of the file. That lifetime is expressed by a number of fractional native tokens called lamports. Accounts are held in validator memory and pay "rent" to stay there. Each validator periodically scans all accounts and collects rent. Any account that drops to zero lamports is purged. Accounts can also be marked rent-exempt if they contain a sufficient number of lamports.

In the same way that a Linux user uses a path to look up a file, a Solana client uses an address to look up an account. The address is a 256-bit public key.
```
{% endcode %}

Thinking back to state, the history of the accounts on Solana is completely irrelevant to their current state. Why? Because all the events that took place in order to arrive at the current state were reviewed by the Proof of History consensus mechanism (i.e. the Solana Validator network) and deemed to be valid.

Tying everything together, what Solana is really built to achieve and maintain consensus on is the state of all accounts on the network. **It is a state machine.** In fact, **“the world’s most performant global state machine”** is exactly how Solana describes itself.

The current state of Solana is already hashed, but then it is shredded and decentralized across all the validators of the network. Effectively what this means is that Solana can recreate the current state of every piece of data on the blockchain… every wallet address, every program that’s been deployed, the location of every single token… at a moment’s notice… **without** needing to know anything about the historical transactions that led up to the current state.

Now, just because historical transactions are irrelevant to the current “in the moment” state of all accounts on Solana (because every event leading up to the present had to be passed through the Solana validator network and therefore was part of the consensus that led to the current state) doesn’t mean that historical transactions aren’t important to the **developers and users** performing actions on Solana.

This is where we circle back to ShdwDrive. The ShdwDrive utilizes the world’s most performant state machine to ensure the validity and integrity of the state of its storage network via on-chain change events.

It’s easiest to explain in real terms, so here’s an example… Let’s say you upload NFT metadata to ShdwDrive and want that data to be stored permanently and want it to be immutable.

1. An NFT project uploads their NFT metadata to ShdwDrive. The NFT project wishes for this metadata to be stored forever and wants it to be immutable.
2. These instructions from the NFT project creators are passed to the ShdwDrive smart contract and the smart contract sends a transaction request to the Solana validators which has been signed by the NFT project’s wallet.
3. An account hash is created on-chain that indicates which NFT project the metadata is associated with, that this metadata is immutable, and it is to be stored permanently.
4. Then the hash plus the actual NFT metadata itself are hashed again, sharded, and uploaded to ShdwDrive by the smart contract in the appropriate storage format and location to ensure that the data can never be edited (not even by the NFT founders who uploaded it) and never deleted.

Under this design, the ShdwDrive smart contract only recognizes signatures from the wallet associated with the stored data. In this example, any transaction request to change the data listed as immutable in ShdwDrive would fail to be validated by the Solana validators. This is because the smart contract would not pass through any instructions to edit or delete this data, due to the fact that the data is immutable and therefore cannot be edited or deleted.

In the [**ShdwDrive Smart Contract**](smart-contracts.md) section, we will go deeper into how the ShdwDrive smart contract interacts with the Solana validator network to ensure the current state (and thus the integrity of the data) remains intact.
