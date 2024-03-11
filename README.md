// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract FakeBank {
    address owner;
    uint256 balance;

    constructor() {
        owner = msg.sender;
        balance = 500; // Initial balance set to 500 rs
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can perform this action");
        _;
    }

    function deposit(uint256 amount) public payable {
        balance += amount;
    }

    function withdraw(uint256 amount) public {
        require(amount <= balance, "Insufficient balance");
        balance -= amount;
        payable(msg.sender).transfer(amount);
    }

    function getBalance() public view returns (uint256) {
        return balance;
    }
}
