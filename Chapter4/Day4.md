## CHAPTER 4

### DAY 4


#### QUESTION 1: 
Because we had a LOT to talk about during this Chapter, I want you to do the following:

Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words. Something like this:
#### ANSWER: 
```cadence
pub contract CryptoPoops {

  //SolomonFoskaayQuestsSubmission

  pub var totalSupply: UInt64

  // This is an NFT resource that contains a name,
  // favouriteFood, and luckyNumber
  pub resource NFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  /*
  This is a resource interface that allows us to control what data is exposed to the /public/ path 
  from the /storage/ path of "CollectionPublic" resource.
  */
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

/*
This is an NFT collection resources containing deposit, withdraw, getid and borrow NFT
functions with trackable id (dictionary) mapping each ID to its actual NFT in the collection
*/
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}

    //deposit NFT to this collection
    pub fun deposit(token: @NFT) {
      self.ownedNFTs[token.id] <-! token
    }

    //withdraw NFT from this collection
    pub fun withdraw(withdrawID: UInt64): @NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.")
      return <- nft
    }

    //get NFTs by ID in this collection
    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    //borrow NFT used to give public access to the NFT
    pub fun borrowNFT(id: UInt64): &NFT {
      return &self.ownedNFTs[id] as &NFT
    }

    init() {
      self.ownedNFTs <- {}
    }

  //nested resources in a resource needed to be destroyed - that is achieved with this function 
    destroy() {
      destroy self.ownedNFTs
    }
  }

//This is a function to create a new collection
  pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
  }

//This is a resource which ensures only role with the @Minter access is allowed to mint NFT 
  pub resource Minter {
    //create NFT with it unique details
    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }
    //create minter role
    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

/*
This initialize the NFT total supply and also save the @Minter resource role in storage
which ensures only the deployer of this smart contract get assigned the @Minter role and able to mint new NFT
*/
  init() {
    self.totalSupply = 0
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```

  
