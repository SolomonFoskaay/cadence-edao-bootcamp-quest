## CHAPTER 2

### DAY 3
Please answer in the language of your choice.

#### QUESTION 1: 
In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
#### ANSWER: 
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day3-Quests-1-ArrayScript.png" width="75%" height="75%">

#### QUESTION 2: 
In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!
#### ANSWER:
<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day3-Quests-2-DictionaryMappingScript.png" width="75%" height="75%">

#### QUESTION 3: 
Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).
#### ANSWER: 
Force unwrap "!" is an operator used to unwrap variable value to display the content. But, if the value is "nil", then it helps to terminate the program instantly. If it finds valid variable value, then it removes the optional type to give out a valid variable value type (especially useful in Dictionary where the value are always "optional" because it can either hold a value like 1, "one" or nil).

EXAMPLE:

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day3-Quests-3-ForceUnwrapScript.png" width="75%" height="75%">

#### QUESTION 4: 
Using this picture below, explain...
What the error message means?
Why we're getting this error?
How to fix it?
<img src="https://github.com/SolomonFoskaay/beginner-cadence-course/raw/main/chapter2.0/images/wrongcode.png" width="75%" height="75%">

#### ANSWERS BELOW: 

(4a) What the error message means
#### ANSWER:
The error message "mismatched types. expected `String`, got `String?`" means the value from the Dictionary is "optional type" instead of just "String" expected as the return value based on String been specified at the function head as what is expected from the return statement.

(4b) Why we're getting this error
#### ANSWER:
We are getting this because Dictionary can output not just the value type like "Int", "Address" and "String", it can also output "Optional Type" which allows the output to also be "nil". Once our program got "nil" as value, it panics and terminate the program, leading to the "mismatched types. expected `String`, got `String?`" error shown.

(4c) How to fix it
#### ANSWER:
To fix it we need to add unwrapped operator "!" to the end of the return value to ensure it forces out real value type if existing and remove the nil for the program to avoid going into panic mode and terminating. See fix below:

BEFORE FIX APPLIED

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day3-Quests-4c1-MismatchErrorFixScript.png" width="75%" height="75%">

AFTER FIX APPLIED

<img src="https://github.com/SolomonFoskaay/cadence-edao-bootcamp-quest/blob/main/screenshots/EmeraldDAO-Cadence-Chapter2-Day3-Quests-4c2-MismatchErrorFixScript.png" width="75%" height="75%">
