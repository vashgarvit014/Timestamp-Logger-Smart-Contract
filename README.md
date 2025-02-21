# ⏳ Timestamp Logger Smart Contract  

## 📜 Description  
The **Timestamp Logger Smart Contract** is a blockchain-based system designed to **log user interactions with timestamps** securely and transparently. Each recorded interaction includes the sender’s **wallet address** and **block timestamp**, ensuring **data integrity and immutability**.  

## 🚀 Features  
- **Decentralized Logging:** Stores interactions securely on-chain.  
- **Immutable Records:** Ensures permanent and tamper-proof logging.  
- **Event Emission:** Triggers real-time notifications on each interaction.  
- **Retrievable Data:** Fetch specific interactions and check total logs.  

## 📂 Smart Contract Code  
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract InteractionLogger {
    struct Interaction {
        address user;
        uint256 timestamp;
    }

    Interaction[] public interactions;

    event InteractionLogged(address indexed user, uint256 timestamp);

    function logInteraction() public {
        interactions.push(Interaction(msg.sender, block.timestamp));
        emit InteractionLogged(msg.sender, block.timestamp);
    }

    function getInteraction(uint256 index) public view returns (address, uint256) {
        require(index < interactions.length, "Invalid index");
        Interaction memory interaction = interactions[index];
        return (interaction.user, interaction.timestamp);
    }

    function getTotalInteractions() public view returns (uint256) {
        return interactions.length;
    }
}
