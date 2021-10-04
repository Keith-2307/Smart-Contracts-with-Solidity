## Unit 20 - "Looks like we've made our first contract!" ##  

### Level Two: The TieredProfitSplitter Contract ###
---

In this contract, rather than splitting the profits between associate-level employees, I calculated rudimentary percentages for different tiers of employees (CEO, CTO, and Bob). While developing and testing the contract, I used the [Ganache](https://www.trufflesuite.com/ganache) development chain and pointed MetaMask to **localhost:8545**.

The TieredProfitSplitter Contract with Fallback function
![Picture12](https://user-images.githubusercontent.com/83662813/135879164-2d129e04-a72e-4339-9920-21f9c813e1a2.png)

Ganache Development Chain – Employee addresses Pre-Fund transfer
![Picture13](https://user-images.githubusercontent.com/83662813/135879385-70114e6e-ef90-4927-a414-466e457a3443.png)

This was done by doing the following transactions:

• Calculate the number of points/units by dividing **msg.value** by **100**.

•	This will allow us to multiply the points with a number representing a percentage. For example, **points * 60** will output a number that is ~60% of the **msg.value.**

• The **uint amount** variable will be used to store the amount to send each employee temporarily. For each employee, set the **amount** to equal the number of **points** multiplied by the percentage (say, 60 for 60%).

• After calculating the **amount** for the first employee, add the amount to the total to keep a running total of how much of the **msg.value** we are distributing so far.

• Then, transfer the **amount** to **employee_one**. Repeat the steps for each employee, setting the amount to equal the points multiplied by their given percentage.

• For example, each transfer should look something like the following for each employee, until after transferring to the third employee:

   -	Step 1: **amount = points * 60;**
   
      o	For **employee_one**, distribute **points * 60.**
      
      o	For **employee_two**, distribute **points * 25.**
      
      o	For **employee_three**, distribute **points * 15.**
      
MetaMask Notification of transfer to employee addresses. Indicating the 60/25/15 split from 9 ETHER deposit.
 ![Picture14](https://user-images.githubusercontent.com/83662813/135881085-d0048fe7-4000-4781-9d2e-9c145ecab0d7.png)
 
 Ganache Employee Addresses post transfer. Indicating the 60/25/15 split of 9 ETHER.
 ![Picture15](https://user-images.githubusercontent.com/83662813/135881451-7cb4c81b-be20-49de-bc15-d18de0638a71.png)
      
Transaction Confirmation for TieredProfitSplitter Contract on Ganache. (Blocks)
![Picture16](https://user-images.githubusercontent.com/83662813/135881656-0a8bf7ab-2e37-41a6-83fb-6bca6c1c6c37.png)

Transaction Confirmation For 9 ETHER transfer on Ganache.
![Picture17](https://user-images.githubusercontent.com/83662813/135881858-720f9d3c-cb7d-4bf3-81e1-f8928dfa99f3.png)

   - Step 2: **total += amount**;
   
   - Step 3: **employee_one.transfer(amount)**;
   
Compiled Tiered Profit Splitter smart contract
![Picture18](https://user-images.githubusercontent.com/83662813/135882401-3558d532-3853-4a7d-94f9-82a8a863dde6.png)

Confirmation request to Deploy and Run transaction smart contract (screen shot 1)
![Picture19](https://user-images.githubusercontent.com/83662813/135882586-c1c78f29-0961-4d21-aee4-ad0e130fcdfe.png)

Confirmation request to Deploy and Run transaction smart contract (screen shot 2)
![Picture20](https://user-images.githubusercontent.com/83662813/135882790-da977f79-4c85-4cda-9a9e-ae646b0c1394.png)

• Send the remainder to the employee with the highest percentage by subtracting total from msg.value, and sending that to an employee.

• Deploy and test the contract functionality by depositing various ether values (greater than 100 wei).

### Interacting with Smart Contract ###

200 wei Deposit:
![Picture21](https://user-images.githubusercontent.com/83662813/135883186-df72144a-cd97-4fe4-b720-defbb29afec6.png)

400 wei Deposit
![Picture22](https://user-images.githubusercontent.com/83662813/135883386-aff90969-01e4-4f8c-8a85-a3045afa56df.png)

800 wei Deposit
![Picture23](https://user-images.githubusercontent.com/83662813/135883692-3a975b07-da4f-46c3-ac64-4deb1b54afe3.png)

•	The provided **balance** function can be used as a test to see if the logic you have in the **deposit** function is valid. Since all the ether should be transferred to employees, this function should always return **0**, since the contract should never store ether itself.

•	Note: The 100 wei threshold is due to the way we calculate the points. If we send less than 100 wei, for example, 80 wei, **points** will equal **0** because **80 / 100** equals **0** because the remainder is discarded. We will learn more advanced arbitrary precision division later in the course. In this case, we can disregard the threshold as 100 wei is a significantly smaller value than the ether or Gwei units that are far more commonly used in the real world (most people aren't sending less than a penny's worth of ether).








