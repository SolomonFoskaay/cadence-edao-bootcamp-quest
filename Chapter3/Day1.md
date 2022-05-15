## CHAPTER 3

### DAY 1


#### QUESTION 1: 
In words, list 3 reasons why structs are different from resources.
#### ANSWER: 
Three(3) reasons why structs are different from resources are:
1. Struct is a data container WHY Resources is a more secured data container.
2. Struct is copiable from one variable to another WHY Resources can not be copied.
3. Struct is assigned to variable with "=" operator WHY Resources can not and only be done with "<-" move operator.

 <hr>
  
#### QUESTION 2: 
Describe a situation where a resource might be better to use than a struct.
#### ANSWER:
One of the most obvious situation where a resource might be better to use than a struct is when issuing NFT. 
It helps preserve the uniqueness and prevent costly mistake of overiding an NFT that may worth millions of dollars 
(guuuuhhhh beter not do such mistake on mainnet lol)

<hr>
  
#### QUESTION 3: 
What is the keyword to make a new resource?
#### ANSWER: 
The keyword to make a new resources is "create"

<hr>
  
#### QUESTION 4: 
Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?
#### ANSWER:
No, if the contract has now public function to create one, then resources can't just be created at will like struct in Transaction or Script.

<hr>
  
#### QUESTION 5: 
What is the type of the resource below?
```cadence
pub resource Jacob {

}
```
#### ANSWER:
The resource is type @Jacob

<hr>

  
#### QUESTION 6: 
Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.
```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): Jacob { // there is 1 here
        let myJacob = Jacob() // there are 2 here
        return myJacob // there is 1 here
    }
}
```
#### ANSWER:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day1-Quests-5-FixResourcesErrorsContract.png" width="75%" height="75%">
