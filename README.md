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
