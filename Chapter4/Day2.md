## CHAPTER 4

### DAY 2


#### QUESTION 1: 
What does .link() do?
#### ANSWER: 
.link() helps to make data in /storage/ path available to anyone as a /public/ path. Simply makes what we have stored, accessible for others to access. It also, gives allows to limit what is been exposed to the public via interface restrictions.

 <hr>
  
#### QUESTION 2: 
In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.
#### ANSWER:
In summary, to use resource interfaces to only expose certain things to the /public/ path, we simply need to ensure only things we are confortable exposing are included in the resource interface while others things remain concealed in the interfaced resource itself. 

So, when the capability is given via the resource interface, it helps to limit and only expose certain things within it to the /public/ path while protecting other concealed things in the actual resources itself from the /public/ path access.


<hr>


#### QUESTION 3: 
Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

  i. In a transaction, save the resource to storage and link it to the public with the restrictive interface.

  ii. Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

  iii. Run the script and access something you CAN read from. Return it from the script.
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

