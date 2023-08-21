# Module-1-polygon
This is my NFT Project, in which I was tasked to deploy an NFT collection on the Ethereum blockchain, 
Map the collection to Polygon, and Transfer assets over via the Polygon Bridge.
# Description
This program is a simple contract written in Solidity, In which we have apple.sol (ERC721A Token) and 5 apple to build a polymer transfer and mint In this we will deploy in goeril network. To successfully complete the Final Challenge, your project should:

```
Generate a 5-item collection using DALLE 2 or Midjourney
Store items on IPFS using pinata.cloud
Deploy an ERC721 or ERC1155 to the Goerli Ethereum Testnet

You should have a promptDescription function on the contract that returns the prompt you used to generate the images

Map Your NFT Collection using Polygon network token mapper. Note: this isn’t necessary but helpful for visualization.
Write a hardhat script to batch mint all NFTs. Hint: ERC721A is optimal here.
Write a hardhat script to batch transfer all NFTs from Ethereum to Polygon Mumbai using the FxPortal Bridge

Approve the NFTs to be transferred
Deposit the NFTs to the Bridge
Test balanceOf on Mumbai
```
# Executing program
First Clone this repo , then write the following commands one by one :

npx hardhat run scripts/deploy.js --network goerli

--> then copy that address and paste in batchMint.js and approveDeposit.js

Run - npx hardhat run scripts/batchMint.js --network goerli

Run - npx hardhat run scripts/approveDeposit.js --network goerli

Copy that address in Goeril Testnet (Etherscan) for checking the transaction
```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;

import "erc721a/contracts/ERC721A.sol";

contract apple is ERC721A{

    address public owner;

    // Maximum number of tokens that can be minted
    uint256 public maxQuantity = 5;

    // Base url for the nfts
    string baseUrl = "https://gateway.pinata.cloud/ipfs/QmSZtSgSmP2t7wnKXSJYcZq96JeSFWkGtj86SgwgDkipyE/";

    // URL for the prompt description
    string public prompt =
        "an apple";

    constructor() ERC721A("apple", "APP") {
        owner = msg.sender;
    }

    // Modifier that only allows the owner to execute a action
    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can perform this action");
        _;
    }

    // Function to mint NFT which only owner can perform
    function mint(uint256 quantity) external payable onlyOwner{
        require(totalSupply() + quantity <= maxQuantity ,"You can not mint more than 5");
        _mint(msg.sender, quantity);
    }

    // Override the baseURI function to return the base URL for the NFTs
    function _baseURI() internal view override returns (string memory){
        return baseUrl;
    }

    // Return the URL for the prompt description
    function promptDescription() external view returns (string memory) {
        return prompt;
    }
}
```
# Authors
Akanksha Teja

# License
This project is licensed under the MIT License - see the LICENSE.md file for details
