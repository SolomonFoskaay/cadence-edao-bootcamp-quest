## CHAPTER 4

### DAY 3


#### QUESTION 1: 
Why did we add a Collection to this contract? List the two main reasons.
#### ANSWER: 
We can add collection to this contract for different reasons but the two major reasons are:

  i. To store multiple NFTs in same /storage/ path without having to rename the path due to Account Storage not allowing to store more than one data per /storage/ path by default

  ii. To make it easier to track NFTs and their IDs belonging to same collection in one place in a sngle storage path.



 <hr>
  
#### QUESTION 2: 
What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")
#### ANSWER:
There are different things to do when you have resources "nested" inside of resource.
But, the most essential is to create a destructor using "destroy" keyword in the resource to ensure those nested resources are destroyed after use


<hr>


#### QUESTION 3: 
Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.
#### ANSWER: 
Some extra things to add to this contract are:

i. Limit who can mint NFT from the collection

ii. Limit the Number of NFT that can ever exist

iii. Ensure no other collection can be added to our own NFT collection to avoid dilluting it

Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.
NO

Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?
NO
