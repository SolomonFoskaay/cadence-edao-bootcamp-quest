## CHAPTER 3

### DAY 2
For today's quest, you'll have 1 large quest instead of a few little ones.

#### QUESTION 1: 
Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.
#### ANSWER: 
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day2-Quests-1a-ArrayDictionaryOfResource.png" width="75%" height="75%">

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day2-Quests-1b-ArrayDictionaryOfResource.png" width="75%" height="75%">

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day2-Quests-1c-ArrayDictionaryOfResource.png" width="75%" height="75%">


~~~cadence
pub contract Test {

    //SolomonFoskaayQuestsSubmission

    //array of resources type @Pet
    pub var arrayOfPets: @[Pet]

    //dictionary of resources type @Pet
    pub var dictionaryOfPets: @{String: Pet}

    //resource type @Pet
    pub resource Pet {
        pub let petName: String
        init() {
            self.petName = "Dog"
        }
    }


    //add to array of resources type @Pet
    pub fun addToPet(pet: @Pet) {
        self.arrayOfPets.append(<- pet)
    }

    //remove from array of resources type @Pet
    pub fun removeFromPet(index: Int): @Pet {
        return <- self.arrayOfPets.remove(at: index)
    }


    //add to dictionary of resources type @Pet
    pub fun addPet(pet: @Pet) {
        let key = pet.petName     
        let oldPetName <- self.dictionaryOfPets[key] <- pet
        destroy oldPetName
    }

    //remove from dictionary of resources type @Pet
    pub fun removePet(key: String): @Pet {
        let pet <- self.dictionaryOfPets.remove(key: key)!
        return <- pet
    }

    init() {
        self.dictionaryOfPets <- {}
        self.arrayOfPets <- []
    }

}
~~~
