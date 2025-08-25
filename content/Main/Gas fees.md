---
share: true
---
2025-08-24  14:53
Tags:[[Web3|Web3]]

## What are gas fees?

Think of Ethereum as a large computer network where people can do tasks like sending messages or running programs. Just like in the real world, these tasks require energy to get done.

In Ethereum, each computational action has a set "gas" price. **Your gas fees are the total cost of the actions in your transaction**. When you send a transaction or run a smart contract, you pay in gas fees to process it.

## Why do we need gas?

- **Security**: Gas helps secure Ethereum by preventing **Sybil attacks**. This is when an attacker floods the network with fake accounts or transactions. If malicious actors want to spam Ethereum with transactions, they need to pay a cost (gas), which makes it expensive for them to attack the network.
    
- **Cost of Computation**: Every action on Ethereum (sending transactions, executing smart contracts) requires computation and storage. Gas acts as a way to pay for this computation. The more complex the operation (e.g., running a smart contract), the more gas it requires.
    
- **Preventing Network Overload**: Ethereum has a limit on how much computation (gas) can be done in a single block (i.e., per transaction). This hard limit helps ensure that the network is always accessible and doesn’t get overwhelmed by too many operations. Without gas, Ethereum could be flooded with transactions, making the network slow or unusable.

### Gas Fee Components:

1. **Base Fee**:
    
    - Set by the Ethereum network.
        
    - Changes depending on network congestion.
        
    - Ensures efficient transaction processing.
        
2. **Priority Fee (Tip)**:
    
    - Optional fee you pay to miners/validators.
        
    - Incentivizes them to prioritize your transaction.
        
    - Increases the speed of your transaction.
        
3. **Units of Gas Used**:
    
    - Measures how much computation is needed for your transaction.
        
    - Simple transactions (e.g., sending ETH) use fewer gas units (21,000 gas).
        
    - Complex actions (e.g., interacting with smart contracts) use more gas.
        

