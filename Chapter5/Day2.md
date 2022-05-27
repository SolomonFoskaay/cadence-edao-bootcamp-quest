## CHAPTER 5

### DAY 2


#### QUESTION 1: 
Explain why standards can be beneficial to the Flow ecosystem.
#### ANSWER: 
Standards can be beneficial to the flow ecosystem because it makes developers have common requirement to follow and implement in their contract which makes it easier
for platforms to implement them easily and safely.

For example, imagine if no standard for NFT, and every developer write their code as desired, then the NFT Marketplace will need to study each contract to add it to their platform
That is not good enough for the Flow ecosystem.


 <hr>
  
#### QUESTION 2: 
What is YOUR favourite food?
#### ANSWER:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter5-Day1-Quests-2-Event.png" width="75%" height="75%">

```cadence
pub contract FavouriteFood {

    //SolomonFoskaayQuestsSubmission

    //food1
    pub let favFood1: String
    pub let favFood2: String

    
    //initialize variables
    init() {
      self.favFood1 = "Eba"
      self.favFood2 = "Egusi Soup"
    }

}    
```


<hr>


#### QUESTION 3: 
Please fix this code (Hint: There are two things wrong):

The contract interface:

```cadence
pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}    
```

The implementing contract:

```cadence
pub contract Test {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff: IStuff {
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}    
```

#### ANSWER: 

The contract interface:

```cadence
pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}    
```

The implementing contract:

```cadence
pub contract Test {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff: IStuff {
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}    
```


