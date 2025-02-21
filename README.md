# ⏳ Timestamp Logger Smart Contract  

## 📜 Description  
The **Timestamp Logger Smart Contract** allows users to log interactions on the blockchain with a timestamp. Each interaction is recorded with the sender's address and the time of execution.  

## 🚀 Features  
- **Logs Interactions:** Stores each interaction with `msg.sender` and `block.timestamp`.  
- **Immutable Record:** Once logged, interactions are permanently stored on-chain.  
- **Event Emission:** Emits an event when an interaction is logged.  
- **Retrieve Logs:** Users can fetch specific interaction details and total interaction count.  

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
