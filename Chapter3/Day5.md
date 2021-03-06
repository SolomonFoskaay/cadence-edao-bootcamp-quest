## CHAPTER 3

### DAY 5


#### QUESTION 1: 
For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.
#### ANSWER (CONTRACT - AREA 1 to 3): 
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day5-Quests-1a-AccessControl.png" width="75%" height="75%">

```cadence
 access(all) contract SomeContract {

        //SolomonFoskaayQuestsSubmission

    pub var testStruct: SomeStruct

    pub struct SomeStruct {

        //
        // 4 Variables
        //

        pub(set) var a: String

        pub var b: String

        access(contract) var c: String

        access(self) var d: String

        

        //
        // 3 Functions
        //

        pub fun publicFunc() {}

        access(contract) fun contractFunc() {}

        access(self) fun privateFunc() {}

        
        pub fun structFunc() {
            /**************/
            /*** AREA 1 ***/
            /**************/

            //READ
            log (self.d)
            //WRITE
            self.d = "ten"
            //Call
            self.publicFunc()
            self.contractFunc()
            self.privateFunc()

            // 4 Variables
            //a - Read Here (YES) || Write Here (YES)
            //b - Read Here (YES) || Write Here (YES)
            //c - Read Here (YES) || Write Here (YES)
            //d - Read Here (YES) || Write Here (YES)

            // 3 Functions
            //publicFunc() - Callable Here (YES)
            //contractFunc() - Callable Here (YES)
            //privateFunc() - Callable Here (YES)
        }

        init() {
            self.a = "a"
            self.b = "b"
            self.c = "c"
            self.d = "d"
        }
    }

    pub resource SomeResource {
        pub var e: Int

        pub fun resourceFunc() {
            /**************/
            /*** AREA 2 ***/
            /**************/
                       
            // 4 Variables
            //a - Read Here (NO) || Write Here (NO)
            //b - Read Here (NO) || Write Here (NO)
            //c - Read Here (NO) || Write Here (NO)
            //d - Read Here (NO) || Write Here (NO)

            // 3 Functions
            //publicFunc() - Callable Here (NO)
            //contractFunc() - Callable Here (NO)
            //privateFunc() - Callable Here (NO)
        }

        init() {
            self.e = 17
        }
    }

    pub fun createSomeResource(): @SomeResource {
        return <- create SomeResource()
    }

    pub fun questsAreFun() {
        /**************/
        /*** AREA 3 ****/
        /**************/
        //READ
          log (self.testStruct.a)
        //WRITE
          self.testStruct.a = "ten"
        //CALL
            self.testStruct.publicFunc()
            self.testStruct.contractFunc()
            //self.testStruct.privateFunc()

        // 4 Variables
            //a - Read Here (YES) || Write Here (YES)
            //b - Read Here (YES) || Write Here (NO)
            //c - Read Here (YES) || Write Here (NO)
            //d - Read Here (NO) || Write Here (NO)

            // 3 Functions
            //publicFunc() - Callable Here (YES)
            //contractFunc() - Callable Here (YES)
            //privateFunc() - Callable Here (NO)
    }

    init() {
        self.testStruct = SomeStruct()
        
    }
}
```


#### ANSWER (SCRIPT -  AREA 4):
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter3-Day5-Quests-1b-AccessControlScript.png" width="75%" height="75%">

```cadence
 import SomeContract from 0x05

pub fun main() {
  /**************/
  /*** AREA 4 ***/
  /**************/
//SolomonFoskaayQuestsSubmission
    //READ
        log (SomeContract.testStruct.a)
    //WRITE
       SomeContract.testStruct.a = "ten"
    //Call
        SomeContract.testStruct.publicFunc()
        //SomeContract.testStruct.contractFunc()
        //SomeContract.testStruct.privateFunc()

  // 4 Variables
  //a - Read Here (YES) || Write Here (YES)
  //b - Read Here (YES) || Write Here (NO)
  //c - Read Here (NO)  || Write Here (NO)
  //d - Read Here (NO)  || Write Here (NO)

  // 3 Functions
  //publicFunc()    - Callable Here (YES)
  //contractFunc()  - Callable Here (NO)
  //privateFunc()   - Callable Here (NO)
}
```
  

