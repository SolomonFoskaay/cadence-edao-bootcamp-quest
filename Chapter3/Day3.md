## CHAPTER 3

### DAY 3


#### QUESTION 1: 
Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.
#### ANSWER: 
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day3-Quests-1-ReferenceDictionaryOfResource.png" width="75%" height="75%">

```cadence
pub contract Test {

    //SolomonFoskaayQuestsSubmission

    //dictionary of resources type @Pet
    pub var dictionaryOfPets: @{String: Pet}

    //resource type @Pet
    pub resource Pet {
        pub let petType: String
        init(_petType: String) {
            self.petType = _petType
        }
    }


    //reference get resource from the dictionary
    pub fun getRef(key: String): &Pet {
      return &self.dictionaryOfPets[key] as &Pet
    }


    //initialize variable "dictionaryOfPets"
    init() {
        self.dictionaryOfPets <- {
          "Puppy": <- create Pet(_petType: "Dog"),
          "Parot": <- create Pet(_petType: "Bird")
        }
    }

}
```

 <hr>
  
#### QUESTION 2: 
Create a script that reads information from that resource using the reference from the function you defined in part 1.
#### ANSWER:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day3-Quests-2-ScriptForReferenceDictionaryOfResource.png" width="75%" height="75%">

```cadence
import Test from 0x03

pub fun main(): String {
    let ref = Test.getRef(key: "Puppy")
    return ref.petType

}
```

<hr>
  
#### QUESTION 3: 
Explain, in your own words, why references can be useful in Cadence.
#### ANSWER: 
Reference can be useful in Cadence because it allows to easily access and interact with data like resource without moving the actual data around. Just like having an ATM card linked to huge amount of money in your bank account, you can easily move around and spend/withdraw your money anytime without the risk of carrying the actual huge amount of money as cash in your bag/wallet all around (thats too risky -lol)

  

