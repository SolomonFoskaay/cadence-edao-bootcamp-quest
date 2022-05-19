## CHAPTER 4

### DAY 1


#### QUESTION 1: 
Explain what lives inside of an account.
#### ANSWER: 


 <hr>
  
#### QUESTION 2: 
What is the difference between the /storage/, /public/, and /private/ paths?
#### ANSWER:



<hr>
  
#### QUESTION 3: 
What does .save() do? What does .load() do? What does .borrow() do?
#### ANSWER: 



<hr>
  
#### QUESTION 4: 
Explain why we couldn't save something to our account storage inside of a script.
#### ANSWER: 


<hr>
  
#### QUESTION 5: 
Explain why I couldn't save something to your account.
#### ANSWER: 


<hr>


#### QUESTION 6: 
Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:

   i. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

   ii. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
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



