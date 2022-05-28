## CHAPTER 5

### DAY 3


#### QUESTION 1: 
What does "force casting" with as! do? Why is it useful in our Collection?
#### ANSWER: 
Force casting with as! is used to downcast data from generic type to a specific type needed.

It is useful in our Collection because it ensures and protect our Collection from been dilluted with other NFTs from other NFT collections. 
It downcast the recieved/deposited NFT to ensure it confirm only to the specific NFT type our collection was created for. And if its from another NFT collection, it panic and abort the deposite to our Collection.


 <hr>
  
#### QUESTION 2: 
What does auth do? When do we use it?
#### ANSWER:
auth is authorised reference used when dealing with a reference to make it possible to downcast data referenced from generic type to a specific type when used with "as!"

<hr>


#### QUESTION 3: 
This last quest will be your most difficult yet. Take this contract:

```cadence
import NonFungibleToken from 0x02
pub contract CryptoPoops: NonFungibleToken {
  pub var totalSupply: UInt64

  pub event ContractInitialized()
  pub event Withdraw(id: UInt64, from: Address?)
  pub event Deposit(id: UInt64, to: Address?)

  pub resource NFT: NonFungibleToken.INFT {
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

  pub resource Collection: NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic {
    pub var ownedNFTs: @{UInt64: NonFungibleToken.NFT}

    pub fun withdraw(withdrawID: UInt64): @NonFungibleToken.NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
            ?? panic("This NFT does not exist in this Collection.")
      emit Withdraw(id: nft.id, from: self.owner?.address)
      return <- nft
    }

    pub fun deposit(token: @NonFungibleToken.NFT) {
      let nft <- token as! @NFT
      emit Deposit(id: nft.id, to: self.owner?.address)
      self.ownedNFTs[nft.id] <-! nft
    }

    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT {
      return &self.ownedNFTs[id] as &NonFungibleToken.NFT
    }

    init() {
      self.ownedNFTs <- {}
    }

    destroy() {
      destroy self.ownedNFTs
    }
  }

  pub fun createEmptyCollection(): @NonFungibleToken.Collection {
    return <- create Collection()
  }

  pub resource Minter {

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  init() {
    self.totalSupply = 0
    emit ContractInitialized()
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}  
```

and add a function called borrowAuthNFT just like we did in the section called "The Problem" above. Then, find a way to make it publically accessible to other people so they can read our NFT's metadata. Then, run a script to display the NFTs metadata for a certain id.

You will have to write all the transactions to set up the accounts, mint the NFTs, and then the scripts to read the NFT's metadata. We have done most of this in the chapters up to this point, so you can look for help there :)

  
#### ANSWER:

The answer is subdivided into:

A. The NonFungibleToken standard Smart Contract DONE below:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day3-Quests-3a-NonFungibleTokenContract.png" width="75%" height="75%">

<br/> 

B. The CryptoPoops NFT Smart Contract DONE below:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day3-Quests-3b-CryptoPoopsNFTContract.png" width="75%" height="75%">

```cadence
import NonFungibleToken from 0x02

pub contract CryptoPoops: NonFungibleToken {
    
  pub var totalSupply: UInt64

  pub event ContractInitialized()
  pub event Withdraw(id: UInt64, from: Address?)
  pub event Deposit(id: UInt64, to: Address?)

  pub resource NFT: NonFungibleToken.INFT {
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


//SolomonFoskaayQuestsSubmission
    /*
    SOLUTION STEP 1:
    Add Interface that an account would commonly publish for their collection
    */
    pub resource interface ICollectionPublic {
        pub fun deposit(token: @NonFungibleToken.NFT)
        pub fun getIDs(): [UInt64]
        pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT

        //SOLUTION STEP 3B: - Add the borrowAuthNFT - to ensure public access to the NFT details via thi Interface
        pub fun borrowAuthNFT(id: UInt64): &NFT
    }


    /*
    SOLUTION STEP 2:
    Add ICollectionPublic Interface to ensure our Collection resource conform to it too
    */
  pub resource Collection: NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic, ICollectionPublic {
    pub var ownedNFTs: @{UInt64: NonFungibleToken.NFT}

    pub fun withdraw(withdrawID: UInt64): @NonFungibleToken.NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
            ?? panic("This NFT does not exist in this Collection.")
      emit Withdraw(id: nft.id, from: self.owner?.address)
      return <- nft
    }

    pub fun deposit(token: @NonFungibleToken.NFT) {
      let nft <- token as! @NFT
      emit Deposit(id: nft.id, to: self.owner?.address)
      self.ownedNFTs[nft.id] <-! nft
    }

    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT {
      return &self.ownedNFTs[id] as &NonFungibleToken.NFT
    }

    /*
    SOLUTION STEP 3A:
    Use authorised reference to make the NFT downcastable by as! operator 
    To display full details of the NFT based on it ID inputed by user search for the specific NFT details
    */
    pub fun borrowAuthNFT(id: UInt64): &NFT {
        let ref = &self.ownedNFTs[id] as auth &NonFungibleToken.NFT
        return ref as! &NFT
    }

    init() {
      self.ownedNFTs <- {}
    }

    destroy() {
      destroy self.ownedNFTs
    }
  }

  pub fun createEmptyCollection(): @NonFungibleToken.Collection {
    return <- create Collection()
  }

  pub resource Minter {

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  init() {
    self.totalSupply = 0
    emit ContractInitialized()
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
} 
```


C. The CreateNFTCollection Transaction used to create CryptoPoops Collection DONE below:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day3-Quests-3c-CreateNFTCollectionTransaction.png" width="75%" height="75%">

```cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

transaction() {

//SolomonFoskaayQuestsSubmission

    /*
    SOLUTION STEP 4:
    create collection to deposit and withdraw CryptoPoops NFTs
    */
    prepare(account: AuthAccount) {
        account.save(<- CryptoPoops.createEmptyCollection(), to: /storage/Collection)
        account.link<&CryptoPoops.Collection{NonFungibleToken.CollectionPublic, CryptoPoops.ICollectionPublic}>(/public/Collection, target: /storage/Collection)
    }

    execute {
        log("We SUCCESSFULLY Stored a Collection for our CryptoPoops")
    }

} 
```


D. The DepositNFT Transaction used to mint and deposit NFTs to the Collection DONE below:

Minted NFT ID = 0

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day3-Quests-3d1-DepositNFTTransaction.png" width="75%" height="75%">

Minted NFT ID = 1

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day3-Quests-3d1-DepositNFTTransaction.png" width="75%" height="75%">

```cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

transaction(recipient: Address, newName: String, newFavouriteFood: String, newLuckyNumber: Int) {

//SolomonFoskaayQuestsSubmission

    /* 
    SOLUTION STEP 5
    Minter role signs the transaction to allow minting to the new owner address
    */
    prepare(account: AuthAccount) {
       let nftMinter = account.borrow<&CryptoPoops.Minter>(from: /storage/Minter)!

       let publicReference = getAccount(recipient).getCapability(/public/Collection)
                            .borrow<&CryptoPoops.Collection{NonFungibleToken.CollectionPublic}>()                                
                            ?? panic("This account does not have a Collection Yet")

        publicReference.deposit(token: <- nftMinter.createNFT(name: newName, favouriteFood: newFavouriteFood, luckyNumber: newLuckyNumber))
    }

    execute {
        log("We SUCCESSFULLY Stored newly minted NFT in our CryptoPoops Collection")
    }

} 
```


E. The CheckNFT Script used to display the NFTs metadata for a certain id DONE below:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day2-Quests-2-Semo-and-Egusi-Soup-Images.jpg" width="75%" height="75%">

```cadence
 import CryptoPoops from 0x01
import NonFungibleToken from 0x02

pub fun main(account: Address, id: UInt64): String {   

//SolomonFoskaayQuestsSubmission

    /* 
    SOLUTION STEP 6
    Display the NFTs metadata for a certain id from CryptoPoops NFT Collection
    */
    let publicReference = getAccount(account).getCapability(/public/Collection)
                            .borrow<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>()
                            ?? panic("This account does not have a CryptoPoops Collection")

    return publicReference.borrowAuthNFT(id: id).name                       


}    
```




