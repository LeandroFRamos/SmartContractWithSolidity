# LeaVoting Smart Contract

This is the repository for **LeaVoting**, a smart contract written in Solidity that implements a basic voting system. The goal of this project is to provide a practical introduction to smart contract development on the Ethereum blockchain.

## Overview

The **LeaVoting** contract allows users to vote for a predefined list of candidates. It records and counts votes, ensuring that only valid candidates can receive votes. This contract is developed for educational purposes to demonstrate fundamental Solidity concepts such as mappings, arrays, and functions.

## Features

- **Candidate Storage**: The contract maintains a list of candidates who can receive votes.
- **Voting**: Users can vote for candidates using the `voteForCandidate` function.
- **Candidate Validation**: Before any voting operation, the contract checks if the candidate is valid.
- **Vote Counting**: The contract allows checking the number of votes received by each candidate.

## Contract Structure

### Variables

- `votesReceived`: A mapping that associates a candidate's name (`string`) with the number of votes received (`uint256`).
- `candidateList`: An array that stores the list of candidates available for voting.

### Constructor

```solidity
constructor (string[] memory candidateName) {
    candidateList = candidateName;
}
function totalVotesFor(string memory candidate) view public returns (uint256) {
    require(validCandidate(candidate));
    return votesReceived[candidate];
}
function voteForCandidate (string memory candidate) public {
    require(validCandidate(candidate));
    votesReceived[candidate] += 1;
}
function validCandidate (string memory candidate) view public returns (bool) {
    for(uint i = 0; i < candidateList.length; i++){
        if (keccak256(abi.encodePacked(candidateList[i])) == keccak256(abi.encodePacked(candidate))){
            return true;
        }
    }
    return false;
}
