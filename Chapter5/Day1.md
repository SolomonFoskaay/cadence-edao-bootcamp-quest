## CHAPTER 5

### DAY 1


#### QUESTION 1: 
Describe what an event is, and why it might be useful to a client.
#### ANSWER: 
A. What an event is

Event is used to inform users what has happened in the Blockchain easily each time it happens.

B. Why it might be useful to a client

It might be useful to client (users of the contract) because it make it easier for the users to get informed what is going on with the contract and can hook up the event to their website to trigger an action or update specific information when a certain event is emited from the Blockchain



 <hr>
  
#### QUESTION 2: 
Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.
#### ANSWER:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day1-Quests-2-Event.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //create event
    pub event NewPetAdded (petType: String, petName: String)

    //resource interface
    pub resource interface IPet {
        pub var petType: String
    }

    //resource type @Pet
    pub resource Pet: IPet {
        pub var petType: String
        pub var petName: String

        init() {
            self.petType = "Dog"
            self.petName = "Puppy" 
        }
    }

    //create & return @Pet resource
    pub fun createPet(newPetType: String, newPetName: String): @Pet {
        let petAdded <- create Pet()

        //emit event details of newsly created pet to users
        emit NewPetAdded (petType: newPetType, petName: newPetName)
        
        return <- petAdded   
    }

    //initialize variables
    init() {
    }

}    
```


<hr>


#### QUESTION 3: 
Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
#### ANSWER: 
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day1-Quests-3-PrePostCondition.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //create event
    pub event NewPetAdded (petType: String, petName: String)

    //resource interface
    pub resource interface IPet {
        pub var petType: String
    }

    //resource type @Pet
    pub resource Pet: IPet {
        pub var petType: String
        pub var petName: String

        //Post condition to ensure pet type can not be Snake 
        pub fun checkPetType(newPetType: String): String {
            post {
            result == "Snake": "This pet type not allowed in this pet center"
            }
            return newPetType
        }        

        init() {
            self.petType = "Dog"
            self.petName = "Puppy" 
        }
    }

    //create & return @Pet resource
    pub fun createPet(newPetType: String, newPetName: String): @Pet {
    
        //Pre condition to ensure pet name not less than one character
        pre {
            newPetName.length > 1: "This pet name is too short."
        }

        let petAdded <- create Pet()

        //emit event details of newsly created pet to users
        emit NewPetAdded (petType: newPetType, petName: newPetName)

        return <- petAdded   
    }

    //initialize variables
    init() {
    }

}     
```

<hr>


#### QUESTION 4: 
For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.
```cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```
#### ANSWER: 

```cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  ///ANSWER
  /*
  NOOOOOOOO it will not log the name 
  WHY?
  because the input "Jacob" is equivalent to 5 and this pre condition does not just like Jacob
  and any other names of 5 lenght like Judes, Janet, Caden - lol! 
  Try using "Solomon" and it will work because the name with 7 letters are super cool enough for this code to reject -lol!
  */
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }



  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
   ///ANSWER
  /*
  YESSSSSSS it will return a value "Jacob Tucker"
  WHY?
  Because the pre condition is true and passed which requires the input name to either be greater than zero or equal to it
  meaning any number of character inputed becomes a valid and acceptable name
  */
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int




    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
   ///ANSWER
   /*
   YESSSSSSS it will return a value "Jacob Tucker"
   WHY?
   Because the post condition is true and passed which requires the input name to either be greater than zero or equal to it
   meaning any number of character inputed becomes a valid and acceptable name
   */
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```


