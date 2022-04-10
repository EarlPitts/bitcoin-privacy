---
title:
- Bitcoin Privacy Concerns
author:
- Imre Molnar
- Bendeguz Seres
theme:
- Copenhagen
date:
- April 11, 2022
---

# Main Problems

- Ovnership is anonymous, flow of money is not

# Bitcoin Protocol

- A bitcoint is a **chain of transactions**
- Owners are identified by **public keys**:
    - ECDSA signature scheme
    - Serves as a *pseudonym*
    - Users can use any number of public keys

---

## Transaction

- The previous owner signs the hash of the transaction (in which he got the bitcoin) and the public key of the next owner
- In practice, SHA256 is used
- This signature is added to the set of transactions (that represent the coin itself)
- These transactions **reference the previous one** and form a **chain**
- To check the *validity*, each transaction can be checked in the chain

## Blocks

- Contains transactions
- Serves as a *timestamp*
- They are linked to form a *chain*, each referencing the previous block
- The **block chain** is pulicly available to every user

---

## Coin Creation

- Happens while blocks are created
- *Each block begins with a certain amount of zeroes*
- The block contains a *nonce*
- When this nonce is found, the block is broadcasted
- Only **21 million** coin can be generated in total
- Finding the nonce gives a reward of some BTC, which gets progressively lower

# Bitcoin Network

- Each user generates one or more keypairs
- The user makes their public key (also called **address**) publicly accessible
- If the user wants to send bitcoins, they *broadcast a transaction* to peers
- Peers propagate to other peers
- Eventually it reaches a miner, who collects transactions into blocks, then finds the nonce
- The miner also adds a **coin generation transaction**, specifying his address for the reward
- The miner broadcasts the block, which propagates

# Participants

- Individuals generally don't attempt mining on their own:
    - They join mining pools, that distributes the computation, and gives miners a franction of the reward
- Most users avoid mining and buy coins from **exchanges** (using other currencies)
- They keep bitcoins in their digital **wallet**, or they use **wallet services**
- Bitcoin can be used to transact with online vendors

# Statistics

- Transactions per day: 264.000
- Blockchain size: 400GB
- Total number of transactions: 725.000
- Most bitcoin belongs to early "hoarders":
    - These "sink" addresses never spent their coins (2013)
- In the early stages, there was only hoarding
- Later most bitcoins were spent almost immediately

# Anonimity

- Identity:
    - Who they pay
    - Who pays them
- Amounts:
    - How much they pay
    - How much they receive
    - Patterns

## Anonimity Types

- Weak: consistent pseudonym (reputation)
- Strong: no reputation

# Clustering Heuristics

- Unique addresses can be linked to a single entity
- Two main heuristics:
    - Different public keys used for transaction from same entity are considered linked
    - *Change addresses*:
        - Exploits a use pattern, not an inherent vulnerability

## Account control

- The entity that controls the account
- It's not enough to know the private key:
    - Services also know you private key, but they don't transact with it (hopefully)
- In case of wallet services, the entity that's responsible for forming transactions is the service provider itself

---

## Change address

- When you want to spend the value of a transaction you received before, you have to *spend all of it*
- The only way to send the fraction of a previous transaction is to use a *change address*, in which the excess is sent back to the sender
- *An address can only send as many times as it has already received*
- *Bitcoins can be divided only by being spent*

# Heuristic 1

- If a transaction uses two or more public keys as input, they belong to the same entity
- This effect is transitive:
    - If we have a transaction with A and B, and an other with B and C, then A, B and C all belong to the same entity

# Heuristic 2

- Focuses on change addresses
- Much less robust
- A common pattern of clients is to create a change address at each transaction, and never reuse it
- By identifying change addresses, not only the receiver, but also the input user can be clustered

# Heuristic 2

- Identifying change addresses:
    - Assumption: they only have 1 input
    - If the output of some transaction has a single address with only 1 input, then it's a change address
    - Exception: coin generation
    - It's also possible to set the change address to the input address itself, so these are avoided as well
- So the one-time change addresses are controlled by the same user as the input address
- The major advantage of this heuristic is that we can **eliminate self-churn**:
    - This way we can get a more accurate picture about how much bitcoin each user receives

# Service Centrality

- The centrality of services makes it difficult to stay anonymous, if you want to cash out into fiat money

# Exchanges

- Using an exchange is *almost unavoidable* for buying in or cashing out
- There are sites where you can find local buyers or sellers, but not really scaleable
- Exchanges are basically *checkpoints*, where users can be deanonimized (in response to e.g.: a subpoena)

# Theft

- The address of the thief is known
- Exchanges usually refuse these addresses (and sometimes send back the money)
- Laundry services are pretty unreliable
- If the thieves are lacking in smarts, we can easily follow the chain of transactions to an exchange

## Peeling chain

- A chain starts with a relatively large amount of coins
- At each transaction, a smaller amount is "peeled" off:
    - One part is transferred to an other address
    - One part is transferred to a one-time change address
- If we follow the change addresses of these hops, we get the chain of this particular transaction
- We also get the recipients by noting the other address (the "peel")

# Mixing Strategies

## CoinJoin

- Doesn't require the modification of the protocol
- Common control is not required for transactions using multiple input addresses
- Multiple users agree on a set of inputs to spend and a set out outputs to pay to
- All participants has to sign for the transaction to be valid
- The sources and destinations are obscured, transaction graph is obfuscated
- A stronger variant has all the change outputs be the same amount
- These are the most blockchain space efficient strategies

---

## Blind Signature

- The message is disguised (blinded) before it's signed
- The blinding can be removed while leaving the signature intact
- The sender's privacy is preserved
- When the signer verifies the unblinded signature, it will be unable to link the two messages together

## Chaumian CoinJoin

- Additionally uses chaum blind signatures:
    1. User provides input and *blinded* output
    2. Mixer signs the *blinded* output
    3. User unblinds the *signed blinded* output, and gives the server a *signed* output, with a new identity
    4. Mixer verifies the signature and creates the CoinJoin transaction
