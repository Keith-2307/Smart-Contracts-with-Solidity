## Unit 20 - "Looks like we've made our first contract!" ##  

### Level One: The AssociateProfitSplitter Contract ###
---

This will accept ether into the contract and divide it evenly among associate-level employees. This will allow the human resources department to pay employees quickly and efficiently.

**Starting your project:**

Navigate to the [Remix IDE](https://remix.ethereum.org/) and create a new contract called **AssociateProfitSplitter.sol**.
While developing and testing my contract, I used the [Ganache](https://www.trufflesuite.com/ganache) development chain, and pointed MetaMask to **localhost:8545**, or replace the port with what I have set in my workspace.  

Ganache Development Chain- Employee Prefunded Addresses.
![Picture2](https://user-images.githubusercontent.com/83662813/135871192-b2deeec9-d16e-469f-94a2-45cfda28fc4a.png)

AssociateProfitSplitter.sol - Contract Code
![Picture3](https://user-images.githubusercontent.com/83662813/135871519-875d3cad-9aa0-4946-9efd-b213c2705cf3.png)

The following public variables were defined at the top of the contract.

• **employee_one** — The **address** of the first employee. Make sure to set this to payable.

• **employee_two** — Another **address payable** that represents the second employee.

• **employee_three** — The third **address payable** that represents the third employee.

Then a constructor function was created to accept the variables:

• **address payable _one**

• **address payable _two**

• **address payable _three**

Within the constructor, I had to set the employee addresses to equal the parameter values. This allowed me to avoid hardcoding the employee addresses.

Next, I created the following functions:

•	**balance** — This function should be set to **public view returns(uint)** and must return the contract's current balance. Since we should always be sending ether to the beneficiaries, this function should always return **0**. If it does not, the **deposit** function is not handling the remainders properly and should be fixed. This will serve as a test function of sorts.

•	**deposit** — This function should be set to **public payable** check, ensuring that only the owner can call the function.

  o	In this function, perform the following steps:
  
   -Set a **uint amount** to equal **msg.value / 3**; in order to calculate the split               value of the ether.
     
   -Transfer the **amount** to **employee_one**.
     
   -Repeat the steps for **employee_two** and **employee_three**.
     
   -Since uint only contains positive whole numbers, and Solidity does not                   fully support float/decimals, we must deal with a potential remainder at                 the end of this function, since **amount** will discard the remainder during                 division.
     
   -We may either have **1** or **2** wei left over, so transfer the **msg.value** -         **amount * 3** back to **msg.sender**. This will re-multiply the **amount** by 3,       then subtract it from the msg.value to account for any leftover wei and send it back     to human resources.
   
   •	Create a fallback **function using function () external payable** and call the **deposit** function from within it. This will ensure that the logic in deposit executes if ether is sent directly to the contract. This is important to prevent ether from being locked in the contract, since we don't have a **withdraw** function in this use case.
   
   
### Test the Contract ###

In the **Deploy** tab in Remix, I deployed the contract to my local Ganache chain by connecting to **Injected Web3** and ensuring MetaMask is pointed to **localhost:8545.**

I needed to fill in the constructor parameters with my designated **employee** addresses.

The **deposit** function was tested by sending various values. I kept an eye on the **employee** balances as I sent different amounts of ether to the contract and ensured the logic is executing properly.

Deposited 2 ETH to each employee contract.
![Picture4](https://user-images.githubusercontent.com/83662813/135876257-3968aea8-7c23-4a5f-8d72-7a1eba5d5b21.png)

Funded employee addresses, showing the 2 ETH increase per account.
![Picture5](https://user-images.githubusercontent.com/83662813/135876502-3fc2a241-6707-4631-a954-7e604e62e42a.png)

Transaction log for one of the employee address’s used
![Picture6](https://user-images.githubusercontent.com/83662813/135876705-5aafa6cc-2af4-4df9-988d-3a18a464e28c.png)

### Deploy the contracts to a live Testnet ###

After feeling comfortable with my contracts, I pointed MetaMask to the Kovan or Ropsten network. Made sure that I have tested ether on this network!

After switching MetaMask to Kovan, I deployed the contracts as before, and copied/kept a note of their deployed addresses. The transactions will also be in my MetaMask history, and on the blockchain permanently to explore later.

Compile Smart Contract
![Picture7](https://user-images.githubusercontent.com/83662813/135877074-5c0a22c3-55ad-4974-ab8f-bc732f20a4f9.png)

Deploy and Run Transaction smart contract with MetaMask Confirmation ((ScreenShot 1).
![Picture8](https://user-images.githubusercontent.com/83662813/135877280-b7c3a5fb-02ed-4b75-96ac-bb730cc7de4f.png)

Deploy and Run Transaction smart contract with MetaMask Confirmation (ScreenShot 2).
![Picture9](https://user-images.githubusercontent.com/83662813/135877471-4fb4c8d4-769d-4085-999d-4c888ee8b669.png)

The smart contract executes the Fallback option.
![Picture10](https://user-images.githubusercontent.com/83662813/135877669-f123e935-a6ff-4e7a-a075-de39448d6230.png)

Finally confirming the balance by Interacting with Smart Contract.
![Picture11](https://user-images.githubusercontent.com/83662813/135877860-30b0d89b-ada5-4f9f-93c9-b06aab1666db.png)





