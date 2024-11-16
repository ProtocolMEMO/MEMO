# MEMO

Here’s THE open-source code of how Protocol Memo could create and manage messages on Solscan, leveraging AI and showcasing its capabilities.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @title ProtocolMemo
 * @dev Creates, stores, and integrates memos using AI-like logic .
 */
contract ProtocolMemo {
    string public protocolName = "Protocol Memo";
    address public owner;
    uint256 public memoCount;

    struct Memo {
        uint256 id;
        string message;
        string aiResponse;
        uint256 timestamp;
        address creator;
    }

    mapping(uint256 => Memo) public memos;

    event MemoCreated(
        uint256 id,
        string message,
        string aiResponse,
        uint256 timestamp,
        address creator
    );

    constructor() {
        owner = msg.sender;
        memoCount = 0;
    }

    /**
     * @dev Generates an AI-driven response for a given message.
     * @param message The message input to "AI."
     * @return response AI-generated response (fictional for this contract).
     */
    function generateAIResponse(string memory message) internal pure returns (string memory) {
        // Fake AI response logic
        return string(abi.encodePacked("AI Analysis: ", message, " [Decoded & Indexed]"));
    }

    /**
     * @dev Allows a user to create a memo and stores it on the blockchain.
     * @param message The message to attach to the memo.
     */
    function createMemo(string memory message) public {
        string memory aiResponse = generateAIResponse(message);
        memoCount++;

        memos[memoCount] = Memo({
            id: memoCount,
            message: message,
            aiResponse: aiResponse,
            timestamp: block.timestamp,
            creator: msg.sender
        });

        emit MemoCreated(memoCount, message, aiResponse, block.timestamp, msg.sender);
    }

    /**
     * @dev Fetches a memo by its ID.
     * @param id The ID of the memo to fetch.
     * @return The memo struct containing details.
     */
    function getMemo(uint256 id) public view returns (Memo memory) {
        return memos[id];
    }

    /**
     * @dev Returns the latest memo created in the protocol.
     */
    function latestMemo() public view returns (Memo memory) {
        require(memoCount > 0, "No memos have been created yet.");
        return memos[memoCount];
    }
}
