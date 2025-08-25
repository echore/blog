---
share: true
---
2025-08-24  20:00
Tags:[[Web3|Web3]]

## What are bridges?

Blockchain bridges work just like the bridges we know in the physical world. Just as a physical bridge connects two physical locations, a blockchain bridge connects two blockchain ecosystems. **Bridges facilitate communication between blockchains through the transfer of information and assets**.

## Types of Blockchain Bridges:

1. **Token Bridges**:
    
    - Allow tokens (like ETH or USDT) to move between two blockchains (e.g., Bitcoin to Ethereum).
        
2. **Data Bridges**:
    
    - Facilitate the transfer of data or information between blockchains, not just assets.
        
3. **Cross-chain Bridges**:
    
    - Enable full interoperability between different blockchain ecosystems.

## How Does It Work?
### 1. Locking on Blockchain A

- **What happens**: Imagine you have some tokens (say **ETH**) on **Ethereum** (Blockchain A) and you want to use them on a different blockchain, like **Binance Smart Chain (BSC)** (Blockchain B).
    
- **How it works**: To transfer ETH from Ethereum to BSC, you send the ETH to a **bridge smart contract** on Ethereum. This contract **locks** your ETH. It **holds your ETH** temporarily so that it can't be used on Ethereum while it's being transferred to BSC.
    
    **Example**:
    
    - You send **1 ETH** to the bridge contract on Ethereum.
        
    - The **1 ETH** is now locked and cannot be used or spent on Ethereum.
        

### 2. Minting/Issuance on Blockchain B

- **What happens**: Once your ETH is locked on Ethereum, the bridge protocol then **creates an equivalent asset** on Binance Smart Chain (BSC).
    
- **How it works**: The bridge creates a new token on BSC, say **1 Wrapped ETH (wETH)**. This **wETH** is now the same value as the ETH that is locked on Ethereum, but it's now available for use on BSC.
    
    **Example**:
    
    - For every 1 ETH locked on Ethereum, the bridge **mints** **1 wETH** on BSC.
        
    - This **wETH** can now be used on BSC-based apps or DeFi platforms.
        

### 3. Unwinding (Returning the Asset)

- **What happens**: If you want to return your ETH from BSC back to Ethereum, the **wETH** you minted on BSC is sent to the bridge contract, and it is **burned** (destroyed).
    
- **How it works**: When you send your wETH back to the bridge on BSC, the bridge **burns** the wETH (removes it permanently). This ensures that the supply of wETH doesn’t increase and the system stays balanced. After burning the wETH, the bridge will **unlock** your original **ETH** on Ethereum, making it available for you to use again.
    
    **Example**:
    
    - You send your **1 wETH** from BSC to the bridge.
        
    - The bridge **burns** the **1 wETH** on BSC.
        
    - It then **releases** the **1 ETH** on Ethereum back to your wallet.

## Summary:

A blockchain bridge is like a **bridge** connecting different blockchains, helping you safely transfer assets between them. It ensures that during the transfer process, **no assets are created or lost, and the total supply remains balanced.**