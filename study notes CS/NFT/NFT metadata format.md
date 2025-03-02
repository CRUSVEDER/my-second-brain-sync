NFT metadata is typically formatted in JSON and follows standards like [ERC-721](https://eips.ethereum.org/EIPS/eip-721) or [ERC-1155](https://eips.ethereum.org/EIPS/eip-1155). The metadata is usually stored off-chain (IPFS, Arweave, etc.) and linked from the smart contract.

### **Basic NFT Metadata Format (ERC-721)**

```json
{
  "name": "Cool NFT",
  "description": "This is a unique digital asset.",
  "image": "ipfs://Qm...hash",
  "external_url": "https://yoursite.com/nft/1",
  "attributes": [
    {
      "trait_type": "Background",
      "value": "Blue"
    },
    {
      "trait_type": "Rarity",
      "value": "Legendary"
    }
  ]
}
```

### **Extended NFT Metadata (ERC-1155)**

```json
{
  "name": "Multi-token NFT",
  "description": "An NFT supporting multiple instances.",
  "image": "ipfs://Qm...hash",
  "animation_url": "ipfs://Qm...hash", 
  "external_url": "https://yourproject.com/nft/1",
  "attributes": [
    {
      "display_type": "boost_number",
      "trait_type": "Power",
      "value": 100
    },
    {
      "display_type": "date",
      "trait_type": "Minted",
      "value": 1704067200
    }
  ]
}
```

### **Key Fields Explained**

- **`name`**: Name of the NFT.
- **`description`**: A short description of the asset.
- **`image`**: A URL or IPFS hash linking to the NFT's image.
- **`external_url`**: A link to more details about the NFT.
- **`animation_url`** _(optional)_: Links to GIFs, videos, or 3D models.
- **`attributes`**: Key-value pairs defining the NFT's properties.
- **`display_type`** _(optional)_: Used for properties like dates, levels, or boosts.

