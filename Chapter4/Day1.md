## CHAPTER 4

### DAY 1


#### QUESTION 1: 
Explain what lives inside of an account.
#### ANSWER: 
Account owner's data lives inside of an account which can be in form of things like Smart contract code stored in Storage and can either acessible via Public path (for everyone) or Private path (for those allowed by the account owner)

 <hr>
  
#### QUESTION 2: 
What is the difference between the /storage/, /public/, and /private/ paths?
#### ANSWER:
The difference between the /storage/, /public/, and /private/ paths are:
 i. /storage/: stores data and only accessible to the account owner
 
 ii. /public/: data store in this path is accessible to everyone
 
 iii. /private/: data store in private path is accessible only to the account owner and any other people the account owner give the access to.


<hr>
  
#### QUESTION 3: 
What does .save() do? What does .load() do? What does .borrow() do?
#### ANSWER: 
i. .save() helps to save data inside the account "Storage"

ii. .load() helps to take out the stored data

iii. .borrow() help to give access to the stored data in storage without actually moving the data itself through the user of reference


<hr>
  
#### QUESTION 4: 
Explain why we couldn't save something to our account storage inside of a script.
#### ANSWER: 
We couldn't save something to our account storage inside of a script because script is only to read what is already stored on Blockchain and not to add, modify or delete it. Only transaction has such capability.

<hr>
  
#### QUESTION 5: 
Explain why I couldn't save something to your account.
#### ANSWER: 
You can't save something to my own account because you are not a coder (lol - just joking). Its because you need AuthAccount access to my account first, which requires I sign a transaction. Since you don't have my private key and have not sign transaction for you, there is no way to save in my account.

<hr>


#### QUESTION 6: 
Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:

   i. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

   ii. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
#### ANSWER: 
A. Define a contract that returns a resource that has at least 1 field in it done below:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day1-Quests-6a-ContractAccountStorage.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //resource type @Pet
    pub resource Pet {
        pub let petType: String
        pub let petName: String

        init() {
            self.petType = "Dog"
            self.petName = "Puppy"
        }
    }

    //create & return @Pet resource
    pub fun createPet(): @Pet {
        return <- create Pet()
    }

    //initialize variables
    init() {
    }

}    
```


Then, write 2 transactions:


B. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it. 
DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day1-Quests-6b-Transaction1AccountStorage.png" width="75%" height="75%">

```cadence
import PetCenter from 0x02

transaction() {

  prepare(acct: AuthAccount) {
    let addPet <- PetCenter.createPet()

    //STEP1of4: saves the resource to account storage
    acct.save(<- addPet, to: /storage/TestPet) 

    //STEP2of4: loads it out of account storage
    let removePet <- acct.load<@PetCenter.Pet>(from: /storage/TestPet)
                    ?? panic("A @PetCenter.Pet Resources Does Not Exist Here!!!")
    
    //STEP3of4: logs a field inside the resource
    log (removePet.petType) 

    //STEP4of4: destroys the removed resource
    destroy removePet 
  }

  execute {

  }
}
```

,

C. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day1-Quests-6c-Transaction2AccountStorage.png" width="75%" height="75%">

```cadence
import PetCenter from 0x02

transaction() {

  prepare(acct: AuthAccount) {
    let addPet <- PetCenter.createPet()
    //SolomonFoskaayQuestsSubmission
    //STEP1of4: saves the resource to account storage
    acct.save(<- addPet, to: /storage/TestPet) 

    //STEP2of4: then borrows a reference to it
    let borrowPet = acct.borrow<&PetCenter.Pet>(from: /storage/TestPet)
                    ?? panic("A @PetCenter.Pet Resources Does Not Exist Here!!!")
    
    //STEP3of4: logs a field inside the resource
    log (borrowPet.petType) 

    //STEP4of4: i tried to destroy the borrowed resource reference
    //destroy borrowPet //got ERROR - cannot destroy value: not a resources
  }

  execute {

  }
}
```

