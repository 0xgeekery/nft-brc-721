# nft-brc-721

nft-brc-721 (abbreviated as nbrc-721) is a set of NFT protocols specifically designed for the ordinals ecosystem, aiming to solve the following problems:

1. NFT data is stored entirely on-chain.
2. NFT data stored on-chain should be as small as possible.
3. NFTs should not only be images, but also have their own names and quantities, and more importantly, they should have randomness and uniqueness.

## Features of nft-brc-721

1. Fully on-chain storage.
2. Minting an NFT reduces the block space occupancy by more than 97% .
3. Randomness: We introduce the concept of DNA for NFTs, and the characteristics of NFTs are determined only after they are minted.
4. Unified interface for easy integration: Only 3 lines of code are needed for the frontend to display NFTs. Third-party platforms can easily integrate.
5. Stronger extensibility: We introduce the concept of a parser on-chain, and developers can implement their own parsers in the interface.

## Implementation

The implementation mainly consists of three main components: deploy, mint, and display layer.
![NFT-BRC-721](./images/nbrc-721.png "NFT-BRC-721")


### The design architecture of NFT-BRC-721
The NFT data on the chain is divided into three structural levels.
1. Base info, traits  
2. Parser
3. Mint inscription
![NFT-BRC-721](./images/structure.png "NFT-BRC-721")


### 1. Deploy

Deployment is a JSON file, mainly containing three parts:

   a. Basic information of the NFT.  
   b. Traits of the NFT, which exist in base64 format.  
   c. Parser: The parser is a function with a unified interface, stored on-chain in base64 format. The frontend can directly obtain images through the parser.  
   The main function of the parser is to generate the final NFT based on the tokenID and DNA of the NFT. Example code for the parser:  
    
    `(_tokenID, _dna, traits) => {  
      //code  
      ......  
      return svg;  
    }
    `

| Key         | Required | Description                                                  |
| ----------- | -------- | ------------------------------------------------------------ |
| p           | YES      | value: nft-brc-721 |
| op          | YES      | value: deploy |
| tick        | YES      | NFT collection of names, such as matches |
| supply      | YES      | NFT maximum quantity of supply |
| v           | YES      | Protocol version, backward compatible |
| traits      | YES      | NFT traits,string,base64 |
| parser      | YES      | NFT parser,string, base64 |



### 2. Mint

The mint file of nft-brc-721 is based on the implementation of the brc20 mint file, with the following format:

`{
"p": "nft-brc-721",
"op": "mint",
"tick": "matchstick",
"in": "",
"id": "0",
"d": "geek"
}`  

| Key         | Required | Description                                                  |
| ----------- | -------- | ------------------------------------------------------------ |
| p           | YES      | value: nft-brc-721 |
| op          | YES      | value: mint |
| tick        | YES      | NFT collection of names, such as matches |
| in          | YES      | The inscription deploy of NFT |
| id          | YES      | ID of NFT, reference tokenID of Ethereum. |
| d           | YES      | Represents a part of the DNA, the user input, the user is advised to enter their own name. "d" and "id" determines the NFT's DNA. |


### 3. Display

The display layer is mainly implemented through the parser. After the frontend obtains the NFT-related data, it passes it to the parser and displays the obtained image.  
Example code:  
{  
    //code  
}  
  
  
In summary, the nft-brc-721 protocol is a set of NFT protocols with features such as fully on-chain storage, block space occupancy reduced by more than 95%, randomness, unified interface, and stronger extensibility. The implementation mainly consists of deploy, mint, and display layer components. The parser is a function with a unified interface, stored on-chain in base64 format, and the frontend can directly obtain images through the parser.
