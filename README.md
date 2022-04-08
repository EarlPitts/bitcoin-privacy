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
- **Double spending**:
    - Transfer bitcoin that was already transferred
