## CHAPTER 3

### DAY 4


#### QUESTION 1: 
Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)
#### ANSWER: 
The 2 things interfaces can be used for are:
1. Restricting access to some contents of a resource/struct
2. Specifies the requirement that must be included in the resource that implement the interface

 <hr>
  
#### QUESTION 2: 
Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.
#### ANSWER:
1. 1st function, show an example of not restricting the type of the resource and accessing its content
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day4-Quests-2a-NotRestrictedInterfaceResourceContent.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //interface of resource type @Pet
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

    //1st function, show an example of not restricting the type of the resource and accessing its content
    pub fun notRestricted() {
      let noRestricted: @Pet <- create Pet()
      log(noRestricted.petName)
      destroy noRestricted
    }

    //initialize variables
    init() {
    }

}    
```

2. 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day4-Quests-2b-RestrictedInterfaceResourceContent.png" width="75%" height="75%">

```cadence
pub contract PetCenter {

    //SolomonFoskaayQuestsSubmission

    //interface of resource type @Pet
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


    //1st function, show an example of not restricting the type of the resource and accessing its content
    pub fun notRestricted() {
      let noRestricted: @Pet <- create Pet()
      log(noRestricted.petName)
      destroy noRestricted
    }

    //2nd function, show an example of restricting the type of the resource and NOT being able to access its content.
    pub fun yesRestricted() {
      let yesRestricted: @Pet{IPet} <- create Pet()
      log(yesRestricted.petName) //ERROR member of restricted type is not accessibe: petName
      destroy yesRestricted
    }



    //initialize variables
    init() {
    }

}        
```


<hr>
  
#### QUESTION 3: 
How would we fix this code?
```cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```
#### ANSWER: 
1. Before above code fixed - the following errors shown:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day4-Quests-3a-FixCodeErrors.png" width="75%" height="75%">

2. AFTER Error1 Fixed:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day4-Quests-3b-FixCodeErrors.png" width="75%" height="75%">


3. AFTER Error2 Fixed:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day4-Quests-3c-FixCodeErrors.png" width="75%" height="75%">

```cadence
pub contract Stuff {

    //SolomonFoskaayQuestsSubmission

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String //FIXED 2: include changeGreeting function head in the interface
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String //FIXED 1A: add favouriteFruit here

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Egg Plant" //FIXED 1B: initialize favourite fruit here
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```
  

