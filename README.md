- https://github.com/nopara73/ZeroLink/blob/master/README.md
- https://cryptography.fandom.com/wiki/Blind_signature

[demo](demo.md)

---

- Ovnership is anonymous, flow of money is not
- Vulnerable to re-identification attacks:
    - Heuristic clustering to group based on shared characteristics
    - Can be used to identify major institutions and the transactions between them
    - Protecting against this would be a significant effort, lowering usability
- *A transaction is a cryptographically signed transfer from one public key to another*
- Transactions are irreversible
- **Pseudo-anonimity**: all transactions are completely transparent
- As the block chain contains all of the transaction graph, it can be analyzed, searching for *patterns*
- **Re-identification attack**:
    - Public keys known to belong to some service are collected
    - Cluster keys based on shared spending authority, creating a graph, where nodes represent the user/service

# Bitcoin Protocol

- **A chain of transactions**
- Owners are identified by public keys:
    - ECDSA signature scheme
    - Serves as a *pseudonym*
    - Users can use any number of public keys
- **Transaction**:
    - The previous owner signs the hash of the transaction (in which he got the bitcoin) and the public key of the next owner
    - In practice, SHA256 is used
    - This signature is added to the set of transactions (that represent the coin itself)
    - These transactions **reference the previous one** and form a **chain**
    - To check the *validity*, each transaction can be checked in the chain
- **Double spending**: Transfer bitcoin that was already transferred
- **Blocks**:
    - Contains transactions
    - Serves as a *timestamp*
    - They are linked to form a *chain*, each referencing the previous block
    - The **block chain** is pulicly available to every user
- *Creation of coins*:
    - Happens while blocks are created
    - *Each block begins with a certain amount of zeroes*
    - The block contains a *nonce*
    - When this nonce is found, the block is broadcasted
    - Only **21 million** coin can be generated in total
    - Finding the nonce gives a reward of some BTC, which gets progressively lower

## Bitcoin network

- Each user generates one or more keypairs
- The user makes their public key (also called **address**) publicly accessible
- If the user wants to send bitcoins, they *broadcast a transaction* to peers
- Peers propagate to other peers
- Eventually it reaches a miner, who collects transactions into blocks, then finds the nonce
- The miner also adds a **coin generation transaction**, specifying his address for the reward
- The miner broadcasts the block, which propagates

### Participants

- Individuals generally don't attempt mining on their own:
    - They join mining pools, that distributes the computation, and gives miners a franction of the reward
- Most users avoid mining and buy coins from **exchanges** (using other currencies)
- They keep bitcoins in their digital **wallet**, or they use **wallet services**
- Bitcoin can be used to transact with online vendors

### Statistics

- Average block size: 1.27
- Transactions per day: 264.000
- Blockchain size: 400GB
- Total number of transactions: 725.000
