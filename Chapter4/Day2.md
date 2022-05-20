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
A. Deploy a contract that contains a resource that implements a resource interface. DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day2-Quests-3a-ContractCapabilities.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //resource interface
    pub resource interface IPet {
        pub let petType: String
    }

    //resource type @Pet
    pub resource Pet: IPet {
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


Then,:


B. In a transaction, save the resource to storage and link it to the public with the restrictive interface. 
DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day2-Quests-3b-TransactionCapabilities.png" width="75%" height="75%">

```cadence
import PetCenter from 0x02

transaction() {

  prepare(acct: AuthAccount) {
    
    //SolomonFoskaayQuestsSubmission
    //STEP1of2: save the resource to account storage
    acct.save(<- PetCenter.createPet(), to: /storage/TestPet) 

    //STEP2of2: link it to the public with the restrictive interface
acct.link<&PetCenter.Pet{PetCenter.IPet}>(/public/TestPetPublic, target: /storage/TestPet)
    
  }

  execute {
    log("Stored Pet Resource & Linked Part Of It To Public")
  }
}
```

,

C. Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up..
DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day2-Quests-3c-Script1ErrorCapabilities.png" width="75%" height="75%">

```cadence
import PetCenter from 0x02

pub fun main(address: Address): String {
    
    //SolomonFoskaayQuestsSubmission
    let publicCapability: Capability<&PetCenter.Pet{PetCenter.IPet}> =
    getAccount(address).getCapability<&PetCenter.Pet{PetCenter.IPet}>(/public/TestPetPublic)

    let testPet: &PetCenter.Pet{PetCenter.IPet} = publicCapability.borrow() 
    ?? panic("The capability doesn't exist or you did not specify the right type when you got the capability.")

    return testPet.petName //ERROR: Member of restricted type not accessible: petName
}
```


,

D. Run the script and access something you CAN read from. Return it from the script.
DONE BELOW:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter4-Day2-Quests-3d-Script2FixedErrorCapabilities.png" width="75%" height="75%">

```cadence
import PetCenter from 0x02

pub fun main(address: Address): String {
    
    //SolomonFoskaayQuestsSubmission
    let publicCapability: Capability<&PetCenter.Pet{PetCenter.IPet}> =
    getAccount(address).getCapability<&PetCenter.Pet{PetCenter.IPet}>(/public/TestPetPublic)

    let testPet: &PetCenter.Pet{PetCenter.IPet} = publicCapability.borrow() 
    ?? panic("The capability doesn't exist or you did not specify the right type when you got the capability.")

    //and access something you CAN read from. Return it from the script
    return testPet.petType //Fixed The ERROR: Member of restricted type not accessible: petName
}
```


