// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleETHStaking {
    // Mapping to store staked amount for each address
    mapping(address => uint256) public stakedAmounts;

    // Event emitted when ETH is staked
    event Staked(address indexed user, uint256 amount);

    // Event emitted when ETH is unstaked
    event Unstaked(address indexed user, uint256 amount);

    /**
     * @dev Allows users to stake ETH.
     * The amount sent with the transaction is recorded as staked.
     */
    function stake() public payable {
        require(msg.value > 0, "Stake amount must be greater than zero");
        stakedAmounts[msg.sender] += msg.value;
        emit Staked(msg.sender, msg.value);
    }

    /**
     * @dev Allows users to unstake their ETH.
     * @param amount The amount of ETH to unstake.
     */
    function unstake(uint256 amount) public {
        require(amount > 0, "Unstake amount must be greater than zero");
        require(stakedAmounts[msg.sender] >= amount, "Insufficient staked amount");

        stakedAmounts[msg.sender] -= amount;

        // Transfer the ETH back to the user
        (bool success, ) = payable(msg.sender).call{value: amount}("");
        require(success, "Failed to unstake ETH");

        emit Unstaked(msg.sender, amount);
    }

    /**
     * @dev Returns the total amount of ETH staked in the contract.
     */
    function getTotalStaked() public view returns (uint256) {
        return address(this).balance;
    }
}
