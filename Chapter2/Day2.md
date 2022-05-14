## CHAPTER 2

### DAY 2
Please answer in the language of your choice.

#### QUESTION 1: 
Explain why we wouldn't call changeGreeting in a script.
#### ANSWER: 
We couldn't call changeGreeting in a script because it requires changing data (the value of variable "greeting" in our smart contract) on the Blockchain and cost gas. That is only done via "Transaction" not "Script".
Script can only view existing data as is on the Blockchain.

#### QUESTION 2: 
What does the AuthAccount mean in the prepare phase of the transaction?
#### ANSWER: 
In the "prepare" phase of the transaction, AuthAccount means account of the signer that has been granted access to execute transactions and sign it.

#### QUESTION 3: 
What is the difference between the prepare phase and the execute phase in the transaction?
#### ANSWER: 
The "prepare" phase get needed access to the user account, which are essential to be used in the "Execution" phase (where the actual transaction is initiated and executed).

#### QUESTION 4: 
This is the hardest quest so far, so if it takes you some time, do not worry! I can help you in the Discord if you have questions.
Add two new things inside your contract:
A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
Add a script that reads myNumber from the contract
Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.
#### ANSWER: 
(4a) A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
(4b) function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day2-Quests-4a-Smart-Contract.png" width="75%" height="75%">

(4c) Add a script that reads myNumber from the contract
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day2-Quests-4b-Script.png" width="75%" height="75%">

(4d) Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day2-Quests-4c1-transaction.png" width="75%" height="75%">

Final result of script rerun after transaction execution to update "myNumber" variable value from "0" to "1234567890" in the smart contract
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day2-Quests-4c2-script.png" width="75%" height="75%">
