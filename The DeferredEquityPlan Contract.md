## Unit 20 - "Looks like we've made our first contract!" ##

### Level Three: The DeferredEquityPlan Contract ###
---

In this contract, we will be managing an employee's "deferred equity incentive plan," in which 1000 shares will be distributed over four years to the employee. We won't need to work with ether in this contract, but we will be storing and setting amounts that represent the number of distributed shares the employee owns and enforcing the vetting periods automatically.

The Deferred Equity Plan Contract Code.
![Picture2](https://user-images.githubusercontent.com/83662813/135885653-8f2d7837-3fdb-4ad2-a8fe-ce90e729a24c.gif)

**A two-minute primer on deferred equity incentive plans:** In this set-up, employees receive shares for joining and staying with the firm. They may receive, for example, an award of 1000 shares when joining, but with a four-year vesting period for these shares. This means that these shares would stay with the company, with only 250 shares (1000/4) distributed to and owned by the employee each year. If the employee leaves within the first four years, he or she would forfeit ownership of any remaining (“unvested”) shares.

•	If, for example, the employee only sticks around for the first two years before moving on, the employee’s account will end up with 500 shares (250 shares * 2 years), with the remaining 500 shares staying with the company. In this example, only half of the shares (and any distributions of company profit associated with them) actually “vested,” or became fully owned by the employee. The remaining half, which were still “deferred” or “unvested,” ended up fully owned by the company since the employee left midway through the incentive/vesting period.

•	Specific vesting periods, the dollar/crypto value of shares awarded, and the percentage equity stake (the percentage ownership of the company) all tend to vary according to the company, the specialized skills, or seniority of the employee, and the negotiating positions of the employee/company. If you receive an offer from a company offering equity (which is great!), just make sure you can clarify the current dollar value of those shares being offered (based on, perhaps, valuation implied by the most recent outside funding round). In other words, don’t be content with just receiving “X” number of shares without having a credible sense of what amount of dollars that “X” number represents. Be sure to understand your vesting schedule as well, particularly if you think you may not stick around for an extended period.

Prefunded Equity Plan Employee Addresses
![Picture24](https://user-images.githubusercontent.com/83662813/135886143-ba77e6c4-b260-4b98-a928-148605ef80fc.png)

Using the starter code, perform the following:

  •	Human resources will be set in the constructor as the **msg.sender**, since HR will be deploying the contract.
  
  •	Below the **employee** initialization variables at the top (after bool active = true;), set the total shares and annual distribution:

   o	Create a **uint** called **total_shares** and set this to **1000**.
   
   o	Create another **uint** called **annual_distribution** and set this to **250**. This equates to a four-year vesting period for the **total_shares**, as **250** will be distributed per year. Since it is expensive to calculate this in Solidity, we can simply set these values manually. You can tweak them as you see fit, as long as you can divide **total_shares** by **annual_distribution** evenly.

Created unit functions
![Picture25](https://user-images.githubusercontent.com/83662813/135887459-80131cb6-42ad-499c-a737-b6b441b0c35f.png)   

•	The **uint start_time = now**; line permanently stores the contract's start date. We'll use this to calculate the vested shares later. Below this variable, set the **unlock_time** to equal **now** plus **365 days**. We will increment each distribution period.

•	The **uint public distributed_shares** will track how many vested shares the employee has claimed and were distributed. By default, this is **0**.

•	In the **distribute** function:
  o	Add the following **require** statements:
  
   1.Require that **unlock_time** is less than, or equal to, now.
   
   2.Require that **distributed_shares** is less than the **total_shares** the employee was set for.
   
   3.Ensure to provide error messages in your **require** statements.
   
  o	After the require statements, add 365 days to the unlock_time. This will calculate next year's unlock time before distributing this year's shares. We want to perform all our calculations like this before distributing the shares.
  
  ![Picture26](https://user-images.githubusercontent.com/83662813/135888802-de78d015-1e5c-44be-8d48-7b76d6ae256c.png)

   o	Next, set the new value for **distributed_shares** by calculating how many years have passed since **start_time** multiplied by **annual_distributions**. For example:
   
   1. The **distributed_shares** is equal to **(now - start_time)** divided by **365 days**, multiplied by the annual distribution. If **now - start_time** is less than 365 days, the output will be **0** since the remainder will be discarded. If it is something like **400** days, the output will equal 1, meaning **distributed_shares** would equal **250**.  

   2. Make sure to include the parenthesis around **now - start_time** in your calculation to ensure that the order of operations is followed properly.

   o	The final **if** statement provided checks in the case the employee does not cash out until 5+ years after the contract start, the contract does not reward more than the **total_shares** agreed upon in the contract.
   
 •	For this contract, test the timelock functionality by adding a new variable called **uint fakenow = now**; as the first line of the contract, then replace every other instance of **now** with **fakenow**. Utilize the following **fastforward** function to manipulate **fakenow** during testing.

•	Add this function to "fast forward" time by 100 days when the contract is deployed (requires setting up **fakenow**):

          'function fastforward() public {'
  	        'fakenow += 100 days;}'

![Picture27](https://user-images.githubusercontent.com/83662813/135890342-1717312b-fabd-4b7b-a879-eddd9980f170.png)

Compile the Deferred Equity Plan contract
![Picture28](https://user-images.githubusercontent.com/83662813/135890502-0fc3f016-af13-4880-98e5-061e45ccd7c4.png)

MetaMask Notification for: Deploy and test your contract locally.
![Picture29](https://user-images.githubusercontent.com/83662813/135890731-1a25f4cd-78be-461d-98df-bf2229f042e0.png)

Deployed Deferred Equity Plan Contract, showing results of confirmation.
![Picture30](https://user-images.githubusercontent.com/83662813/135890917-d260f89a-0251-41d2-b738-580bff77095a.png)

Deployed Contracts:
![Picture31](https://user-images.githubusercontent.com/83662813/135891120-9da32688-d081-45d1-974a-eb53bac416aa.png)


## Interacting With Smart Contracts ##

MetaMask Fast Forward Confirmation Request
![Picture32](https://user-images.githubusercontent.com/83662813/135891330-ee633f56-369c-4899-a086-c3d201eacf4d.png)

Fast Forward Test Result for Deferred Equity Plan Contract
![Picture33](https://user-images.githubusercontent.com/83662813/135891500-d15a8d03-19c5-47a2-9ee5-573b2d3a91de.png)

MetaMask Distribute Confirmation Request
![Picture34](https://user-images.githubusercontent.com/83662813/135891744-653084b7-4a9f-4167-9d54-2f3fa64474d7.png)

Distribute Function results on the Deferred Equity Plan
![Picture35](https://user-images.githubusercontent.com/83662813/135891926-dd7d6429-7694-4f2d-8cd5-4d8b5c8be5dd.png)

The final test was the unlock function shown below:
![Picture36](https://user-images.githubusercontent.com/83662813/135892229-9c8464ab-4220-4a97-b1f8-5dace948083f.png)

Once you are satisfied with your contract's logic, revert the **fakenow** testing logic.
![Picture3](https://user-images.githubusercontent.com/83662813/135892468-003597ee-852a-4d7c-9584-7509c93c4049.gif)

