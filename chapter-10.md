# Minting and Managing Tokens for Fungible & Non-fungible Assets

## Tokens {#tokens}

A token in everyday life is something that stands in for, or represents, something else. A valet parking ticket represents your car. A subway token represents the right to take a ride. A concert wristband represents the right to enter a venue. In all these cases, the token is not the actual thing but is a claim or proof connected to it.

Tokens can be fungible or non-fungible. 

* A fungible token is interchangeable with any other token of the same type. A money order is an example. It represents a certain amount of money, and any money order for the same amount is equivalent to any other.   
    
* A non-fungible token represents something unique. Your car is an example of a non-fungible asset. Even if two cars begin identically, they become different over time because of how they are used and maintained. Therefore, a valet parking ticket that acts as a token for your car would therefore be non-fungible.

These ideas about tokens carry over to the blockchain world.

## Blockchain-based tokens {#blockchain-based-tokens}

Blockchain technology allows us to create digital tokens that represent claims, rights, or assets. Where does technology help?

* The technology helps  
    
  * keep track of who holds these tokens, and   
      
  * manage how they move  
      
    * Once created, these tokens can be transferred or used according to the rules built into their smart contracts.

Blockchain-based tokens can also be fungible or non-fungible. 

* Fungible blockchain tokens behave like identical units of value that can be exchanged on a one-to-one basis.   
    
* Non-fungible blockchain tokens represent unique items that cannot be substituted for one another.

The following sections help us better understand blockchain-based tokens. We will first focus on blockchain-based non-fungible tokens (NFTs). After that, we turn to fiat-backed stablecoins, which are an example of blockchain-based fungible tokens that are designed to maintain a stable value.

## NFTs {#nfts}

NFTs are blockchain-based non-fungible tokens. They represent unique digital items or claims to unique assets. 

* An NFT is not the actual asset but is a digital stand-in recorded on the blockchain for something unique.

* Each NFT represents a single copy of a digitized asset (e.g., a music file or digital art), even when multiple identical copies exist.

* The ownership of the asset is determined by whoever holds the private key to the token’s address. 

* NFTs are created using smart contracts, which (a) enable their issuance, transfer, and management, and (b) rely on blockchain technology to preserve the integrity and visibility of ownership.

### Why was there a craze for NFTs? {#why-was-there-a-craze-for-nfts?}

Since you now have a conceptual understanding of NFTs, you are likely to ask why there was a craze for NFTs. 

The craze was due to the ability of NFTs to convert a fungible asset into a non-fungible asset.

For that, let us consider digital art that you have created. Would you call this asset fungible or non-fungible? 

The digital art that you created can be argued to be fungible. You can make multiple copies of it. Each copy would be the same as the other. 

But it is now possible to make your digital art non-fungible. Why would we want to make them non-fungible? Non-fungible implies uniqueness. And uniqueness implies the price we pay for them. We pay a greater price for things that are scarce \-- provided we see them as inherently useful in our lives. 

So, how can we make something like digital art non-fungible?

First of all, we store the digital art in a place where it is immutable. 

Then, we represent it with one or more tokens and we put those tokens on a blockchain. The tokens (or their private keys) are given to the owners. 

We now take advantage of the authentication, immutability, and transparency aspects of the blockchain. 

* Authentication and immutability allow us to control ownership. You have the private key to the token and you are the only one who can operate it. And others would not be able to change the information in the token and transfer it to themselves because of immutability. 

* You can claim to the world that you have the only token that accompanies (or that you have one of the limited tokens that accompany) the digital art. Because the token is on the blockchain, others can verify (because of the transparency afforded by the blockchain) that you are the owner and that there are no more tokens or certificates of ownership of that digital art. 

And, voila, we have taken something that was fungible and transformed it into something non-fungible. 

### Plain english mechanics of creating an NFT  {#plain-english-mechanics-of-creating-an-nft}

Let us consider the case of us as creators of digital art. We want to sell it to others \-- typically only a few others in order to take advantage of the idea that scarce items are more valuable than freely available ones. 

* We don’t hand over the art to the person or entity we sell it to. We keep it in some ‘decentralized’ place where it can remain permanently. 

  * Permanent means that it stays there forever and unchanged. 

  * See it as storing a smart contract on the blockchain. Once you store it, it is there and it does not change.  We don’t store the digital art on blockchain, though, because storing information on blockchain is expensive. There is more later on where it is stored. 

* We can issue a token for the digital art that we created. It is not the digital art itself but a claim to its ownership.

* The token points to the location where the digital art is stored. 

* We can write our smart contract so that once a token is issued to a particular account or address on the blockchain, then only that account or address can change ownership. 

* Anyone can go to the smart contract that issued the token and see who is the owner of which token.

### Exercise: Hands-on learning  {#exercise:-hands-on-learning}

Before we get our hands dirty with the code, go to Google Docs. 

Create a doc and in that upload/paste a picture (if you don’t have a picture, use [this](https://u4d2z7k9.rocketcdn.me/wp-content/uploads/2021/04/rsz_ethereum-nfts-environment.jpg)). Then select File/Share/Publish to web. Select Publish and copy the URL (in a google doc or wherever you can retrieve it from). This is the URL of your digital art. This is not the ideal way to store your digital art but for now we will manage with this. 

Create two new docs, each with a new picture (if you don’t have pictures, use [this](https://www.dunster.co.za/wp-content/uploads/2022/04/NFT-Art-scaled-e1649403981704.jpg) and [this](https://i0.wp.com/gmbaker.net/wp-content/uploads/2021/12/396px-Mona_Lisa.jpg?w=396&ssl=1)). Publish them to the web and copy their URLs (in a google doc or wherever you can retrieve them from).

For our smart contract, we will borrow the code from [https://medium.com/geekculture/mint-an-nft-and-erc-721-smart-contract-easy-step-by-step-4fafff151fbe](https://medium.com/geekculture/mint-an-nft-and-erc-721-smart-contract-easy-step-by-step-4fafff151fbe). It is reproduced below. 

This code is based on open source code that allows us to create our own tokens. 

Copy the following into Remix.

// SPDX-License-Identifier: MIT  
pragma solidity \>=0.8.2 \<0.9.0;  
   
import "https://github.com/0xcert/ethereum-erc721/src/contracts/tokens/nf-token-metadata.sol";  
import "https://github.com/0xcert/ethereum-erc721/src/contracts/ownership/ownable.sol";  
   
contract newNFT is NFTokenMetadata, Ownable {  
   
  constructor() {  
    nftName \= "Synth NFT";  
    nftSymbol \= "SYN";  
  }  
   
  function mint(address \_to, uint256 \_tokenId, string calldata \_uri) external onlyOwner {  
    super.\_mint(\_to, \_tokenId);  
    super.\_setTokenUri(\_tokenId, \_uri);  
  }  
   
}

You will notice that we are importing code into our contract. Instead of writing it ourselves, we leverage the code written by someone else and vetted by the community.

Instead of the nftName and nftSymbol provided in the contract, we can use our own (e.g., “Synth Kahai” and “SK” or “Cryptokitties” and “CK”). nftSymbol is a shorthand for the name. 

1. Compile the code and deploy it. 

* Specifically, use the first EOA in the Remix VM to deploy the contract. That address becomes the one who controls many aspects of the contract. Since it is the one that controls many aspects of the contract, the contract refers to it as the owner (though, strictly speaking, it is the code that owns it). 


2. Confirm that the first EOA is the owner (as per the language of the contract). 

* Click on the owner variable to see who owns the contract. Is that the address of the deployer?  
    
3. Create three tokens using the owner EOA. Give them to different addresses or accounts. 

* Use the mint function to mint three new tokens. Give them to the 2nd, 3rd, and 4th address in the Remix VM. Use 2, 3, 4 as token ids (we are keeping token id equal to 1 for the creator – this is not a strict requirement, though). Use the urls of the three different digital art pieces that you created, one for each address. 

  For example, for the first token, you should enter something like the following (you may also use the following by copying and pasting it into the mint function) for the different fields (make sure you don’t copy and paste the labels which are given in bold):

  **Address:** 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2

  **Token ID:** 2

  **URL:** https://docs.google.com/document/d/e/2PACX-1vTmvjfLs5tZI1pA2ntKx7F-9LtkbWUvjzLsjVOEzT8ClLVOg4c5okdqRLh7ONJh6uc3YmtkfqzDXTP4/pub


  

  For the second token, you could use the following:

  **Address:** 0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db

  **Token ID:** 3

  **URL:** https://docs.google.com/document/d/e/2PACX-1vR-WIgPkD1siHAfHU4s-TrXru4topRxee8E-eGYU413bRMmRkLU1ZWWBEM6lrQC3H2HpaMG99\_oNk6k/pub


  

  For the third token, you could use the following:

  **Address:** 0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB

  **Token ID:** 4

  **URL:** https://docs.google.com/document/d/e/2PACX-1vRBgpc9aqAxTrDaUbe5wcq93BxP6dEAUrftViQ97z1aro4ook4eRkyfTARHLybW6ErzYzEmtGUhhXpt/pub


4. Check out the balance (use balanceOf variable) for each address that was given a token. This gives you the number of tokens of each of the addresses. To confirm, check out the balance of any address to which you have not given any token.

5. Use the ownerOf variable to see who owns the tokens with ids 2, 3, & 4\. Use different EOAs to check ownership of the different tokens. Are you able to use an EOA different from that of the creator? Why?

6. Make sure you are using the first EOA – i.e., the creator’s EOA. Use the transferFrom function to transfer the token whose id is 2 from the second to the third address. What do you observe? Now use the third EOA and see if you can transfer. What do you observe? You will see that you are unable to transfer. That is because only the second address – which owns the token whose id is 2 – should be able to transfer ownership. No other EOA is able to do the transfer.  

7. Change the ACCOUNT that you are using to the 2nd address. Now try to transfer the token. What do you observe? You are able to transfer. 

8. Now check the balances for each address again.

9. Also check the ownership of each token. 

10. Try minting the following new token but AFTER changing to EOA (the address under ACCOUNT) to the second address or any address but the first one (which is of the deployer of the contract).

    **Address:** 0x617F2E2fD72FD9D5503197092aC168c91465E7f2

    **Token ID:** 5

    **URL:** [https://docs.google.com/document/d/e/2PACX-1vSc7H25h90KEAa-Ql1LSinVvOdVsqXFBrSK5Qvak7ZTajUHl9Y9ggzoPK-4-wpYCKb0oPKGrDord8wQ/pub](https://docs.google.com/document/d/e/2PACX-1vSc7H25h90KEAa-Ql1LSinVvOdVsqXFBrSK5Qvak7ZTajUHl9Y9ggzoPK-4-wpYCKb0oPKGrDord8wQ/pub)

    What do you observe? Who do you think will be able to mint the art for which token ID is 5?

11. Could you (as the creator of digital art that you are selling) not change the content at any of the URLs? After all, you created an art and published it. You can also unpublish it or delete it, thereby leaving the entity you have sold to high and dry?

    For that, read about IPFS or interplanetary file systems. Google this term or you can use the following link to learn more: [https://www.ledger.com/academy/what-is-ipfs](https://www.ledger.com/academy/what-is-ipfs). You can also ask ChatGPT about IPFS.

    The following is a brief paragraph about IPFS from ChatGPT:

    

    IPFS (InterPlanetary File System) is a decentralized, peer-to-peer network for storing and sharing files using content-addressing, where files are identified by cryptographic hashes instead of locations. This ensures data integrity and enables efficient retrieval from multiple peers, much like BitTorrent. IPFS is resilient, decentralized, and immutable, making it ideal for hosting websites, archiving data, and integrating with blockchain systems. By distributing data across the network, it reduces reliance on central servers, enhances speed, and ensures censorship resistance, paving the way for a faster, safer, and more open web.

    With content stored on IPFS, it cannot be changed\!  In other words, we have immutable storage and the creator cannot play any tricks. 

    Also, since the file is addressed by its cryptographic hash rather than by its location, the same content can be hosted by many independent nodes without breaking the link. On the traditional web, by contrast, a URL points to a specific server, so if the creator deletes the file or takes down the server, the content simply disappears. With IPFS, even if the original creator deletes their local copy, the content can remain accessible elsewhere on the network as long as at least one node continues to store it. As a result, IPFS shifts trust away from the individual creator and toward a decentralized infrastructure that is designed to preserve both the integrity and the long-term accessibility of digital content.

12. Check out more functions of the NFT smart contract. To learn more about these functions visit [https://docs.openzeppelin.com/contracts/2.x/api/token/erc721](https://docs.openzeppelin.com/contracts/2.x/api/token/erc721). 

### Uses of NFTs {#uses-of-nfts}

Are NFTs useful only for digital art? Are there other uses? What are they?

Essentially, you can use NFTs to enable claim to ownership for any kind of digital asset or an asset that can be digitized. What are examples of that?

* Music  
* Games  
* Software  
* Certificate of ownership of a piece of land, stock, automobile, digital artifacts in the metaverse  
* Your degree or transcripts from a university – the university would mint your degree certification or transcripts and only you can do things like make them accessible to certain addresses. 

## Minting & managing fungible tokens – Simulating fiat-backed stablecoins  {#minting-&-managing-fungible-tokens-–-simulating-fiat-backed-stablecoins}

This section, which was created with assistance from ChatGPT,  takes us through the exercise of minting and managing fiat-backed stablecoins. We will simulate the role of:

* A user, who deposits and redeems U.S. dollars off-chain, and  
* An issuer, who mints and burns tokens on-chain.

But, first, let us get a sense of how fiat-backed stablecoins, such as those provided by Circle and Tether work. 

### How do fiat-backed stablecoins provided by Circle & Tether work? {#how-do-fiat-backed-stablecoins-provided-by-circle-&-tether-work?}

Fiat-backed stablecoins work as follows:

1. A user sends USD to the issuer (Circle, Tether).  
     
2. The issuer mints 1 stablecoin token for each $1 deposited.  
     
3. These tokens live on a blockchain (Ethereum, Solana, etc.).  
     
4. The issuer uses the blockchain’s native currency (ETH, SOL) only to pay gas.  
     
5. When a user returns the stablecoins to the issuer,  
     
   * the issuer burns the tokens, and  
       
   * sends USD back to the user.

### Exercise: Simulating fiat-backed stablecoins {#exercise:-simulating-fiat-backed-stablecoins}

In this exercise, “USD deposits” and “USD withdrawals” will be simulated by pretending that they have happened. The minting and burning, however, will take place in the virtual Ethereum platform provided within Remix.

Copy the following into Remix:

| `// SPDX-License-Identifier: MIT pragma solidity ^0.8.0; import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.9.0/contracts/token/ERC20/ERC20.sol"; import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.9.0/contracts/access/Ownable.sol"; contract USDStablecoin is ERC20, Ownable {     constructor() ERC20("Simulated US Dollar Coin", "sUSDC") {}     // Issuer mints tokens after verifying real USD deposits off-chain     function mintForUSDDeposit(address to, uint amountInUSD) external onlyOwner {         // 1 token per 1 USD         _mint(to, amountInUSD * 1e18);     }     // Issuer burns tokens after receiving USD back off-chain     function burnForUSDWithdrawal(uint amountInTokens) external {         _burn(msg.sender, amountInTokens);     } }`  |
| :---- |

This contract models a fiat-backed stablecoin like USDC:

* Only the issuer (owner) can mint (because only the issuer can verify USD deposits).  
* Users can burn their own tokens (the smart contract does not handle USD withdrawal; that is off-chain).

Compile using Remix. Deploy using the first account (the issuer) as owner and carry out the following steps:

| Step 1: “USD Deposit” and On-Chain Minting (Issuer → User)  In this step, Account 1 (0x5B38Da6a701c568545dCfcB03FcB875f56beddC4) acts as the issuer. Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2) acts as the customer who sends USD. We will begin by pretending that Account 2 has sent $200 to the issuer via traditional means. Assume that has already been done. Account 1 (the issuer) mints tokens on-chain. Carry out those actions as described below. Keep Account 1 selected (issuer). Call the function mintForUSDDeposit with: to: Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2) amountInUSD: `200` This creates 200 sUSDC for Account 2\. sUSDC is simulated stablecoin pegged to the US dollar.  Check the balance Call: `balanceOf(Account 2)` (Account 2: 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2)  You should see: `200000000000000000000`  Note that each sUSDC is broken up into 10\*18 units, which is why you are seeing a balance of 200 \* 10^18 units for Account 2\.  Step 2: User Transfers sUSDC On-Chain   Now Account 2 uses the stablecoin. Switch to Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2). Call the transfer function with: recipient: Account 3 (0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db) amount: `50000000000000000000` (50 sUSDC) Check balances: Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2) now has 150 sUSDC Account 3 (0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db) now has 50 sUSDC This illustrates how users can freely use stablecoins.  Step 3: User Returns sUSDC to Issuer and Redeems USD  Account 3 wants to redeem 30 sUSDC for real USD. Account 3 (sends 30 tokens back to the issuer (Account 1). Switch to Account 3 (0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db) Call the transfer function with: recipient: Account 1 (i.e., 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4) amount: `30000000000000000000` (30 sUSDC) User requests a USD withdrawal from the issuer via traditional means (we just pretend here).  Now Account 1 checks its wallet and sees that Account 3 returned 30 tokens (Account 1 is able to see it has received 30 tokens but determining where they have come from is a somewhat complex off-chain process, which we do not need to get into. However, if you remember what we had done when introducing Ethereum – specifically Part 2, we had seen one or more internal transactions with descriptions of who had sent the ETH to whom. All of that was done using an off-chain process). Issuer burns the tokens Switch to Account 1 (0x5B38Da6a701c568545dCfcB03FcB875f56beddC4) Call burnForUSDWithdrawal with: amountInTokens: `30000000000000000000` This removes 30 sUSDC from circulation.  Off-chain settlement The issuer (Account 1\) would now send $30 USD back to Account 3 (we just pretend here). Step 4: Delegated Spending  This simulates a situation where a parent approves spending of a certain amount by their kid. We will simulate Account 2 approving Account 4 to spend 20 sUSDC. Account 2 approves Account 4  Switch to Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2) Call the approve function with: spender: Account 4 (0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB) amount: `20000000000000000000` Account 4 transfers sUSDC from Account 2 → Account 5 Switch to Account 4 Call the transferFrom function with: sender: Account 2 (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2) recipient: Account 5 (0x617F2E2fD72FD9D5503197092aC168c91465E7f2) amount: `20000000000000000000`  Balances will update accordingly.  |
| :---- |

