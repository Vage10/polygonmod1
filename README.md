# Sample Hardhat Project

Welcome to the project! This guide walks you through batch minting NFTs on the Sepolia network and bridging them to the Amoy network using the FX Portal. The project demonstrates the bridging capabilities for ERC721A NFTs.

## Project Overview 
This project showcases how to bridge NFTs between different networks. With the Goerli and Mumbai testnets deprecated, we utilize Sepolia and Amoy networks. The StreetNft.sol contract is optimized for batch minting NFTs in one transaction.

## Smart Contract Example
The StreetNft.sol contract includes a batch minting function for NFTs:
```
function batchMintNFT(string[] memory nftURLs, string[] memory prompts) public onlyOwner {
    require(nftURLs.length == prompts.length, "Mismatched arrays length");
    uint256 startTokenId = counter;
    uint256 numberOfTokens = nftURLs.length;

    _safeMint(owner(), numberOfTokens);

    for (uint256 i = 0; i < numberOfTokens; i++) {
        _tokenURIs[startTokenId + i] = nftURLs[i];
        _prompts[startTokenId + i] = prompts[i];
    }

    counter += numberOfTokens;
}
```
### Batch Minting NFTs 
Users can batch mint multiple NFTs on the Sepolia network in one transaction using the batchMintNFT() function. This allows for efficient and scalable NFT creation.

### Bridging NFTs 
After minting on Sepolia, NFTs can be bridged to the Amoy network using the FX Portal. You'll need to approve the deposit, then wait for the bridge to complete.

### Checking NFT Balances
Once the bridge process is finished, check the balance of NFTs on the Amoy network to confirm the successful transfer.

## How to Get Started 
### Installation
1. Clone the Repository: Fork or clone this project to your local environment.
2. Install Dependencies: Ensure Node.js is installed, then run:
```
npm install
```
3. Set Up Environment Variables: Create a .env file and configure your RPC URLs and wallet private key.
### Execution Steps
1. Compile the Contract:
```
npx hardhat compile
```
2. Deploy the Contract on Sepolia Network:
```
npx hardhat run scripts/deploy.js --network sepolia
```
3. Batch Mint NFTs on Sepolia Network:
```
npx hardhat run scripts/batchMint.js --network sepolia
```
4. Approve NFT Deposit for Bridging:
```
npx hardhat run scripts/approveDeposit.js --network sepolia
```
5. Wait for the Bridging Process: Allow 20-30 minutes for the bridge to complete. Once done, obtain the contract address on the Amoy network.
6. Check NFT Balance on Amoy Network:
```
npx hardhat run scripts/getBalance.js --network amoy
```

Need Help? 
Make sure to have faucet tokens for both networks:
* Sepolia Faucet: Sepolia Faucet
* Amoy Faucet: Amoy Faucet (requires joining the Polygon Discord)
If you run into issues with the Solidity compiler version, ensure you're using a compatible version.

## Author
Vageshwari Chaudhary
