# Pricing Kata

Work in pairs to solve this kata. 

You're going to build a system that will accept items. Each item has a nam, price and possibly a discount (x pieces for y sum). 
The system will also scan a customers items and output the total price with the relevant discounts. You get to choose how you
design the setup (adding items and discount) and in which order you implement this functionality. The Checkout class (if you 
choose to name it Checkout) should receive pricing when it is created, and should be able to scan items. The scan method should 
return the sum of purchases. 


## Specification

The finished function(s) should be able to handle the following: 
* Register an item (name, unit price)
* Register an item with a discount rule (name, unit price, threshold, discount price at threshold level)
* Connect a checkout with a set of prices
* Scan an item and return the correct price
* Reject unknown item without adverse effects for already scanned items
* Scan items that trigger a discount


## Solving the kata

Spend time discussing the order in which you want to proceed. You don't get to write any code in the implementation class 
unless you have a test that covers it. Write the test first and verify that it fails before implementing the correct behaviour. 
Refactor as you go when the need arises. 

Write down some notes on which order you want to implement functionality, and why. We will go through the choices each group
has made and the code, as I'm sure each group will solve the problem in a different way. 