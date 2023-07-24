# AddingSenderAddressToContract
// SPDX-License-Identifier: MIT 
pragma solidity ^0.8.18;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract FundMe {
    AggregatorV3Interface internal priceFeed;

    constructor() {
        priceFeed = AggregatorV3Interface(0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419);
    }

    uint256 public minimumUSD = 5;
    

    address[] public funders;
    mapping(address funder => uint256 a ount funded) public addressToAmountFunded;

    function fund() public payable {
        uint256 conversionRate = getPrice();
        require(conversionRate >= minimumUSD, "didn't have enough ETH"); 
        funders.push(msg.sender);
        addressToAmountFunded[msg.sender] += addressToAmountFunded[msg.sender] + msg.value; 
    }

    function withdraw() public {
        for (uint256 funderIndex = 0; funderIndex < funders.length; funderIndex++) {
            // Add withdrawal logic here
        }
    }

    function getPrice() public view returns(uint256) {
        (,int256 answer,,,) = priceFeed.latestRoundData();
        return uint256(answer);

    function getConversionRate(uint256 ethAmount) public view returns(uint256){
      uint256 ethPrice = getPrice();
      uint256 ethAmountInUSD = (ethPrice * ethAmount) / 1e18;

    }

  }
