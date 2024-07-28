# Wipro Salesforce interview Questions

### Question : What all asynchronous process available in salesforce.
#### Answer : 

### Question : Explain batch processing
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

### Question : Best Practices follwed for apex
#### Answer : 
#### 1. Bulkify Your Code
Bulkification of your code is the process of making your code able to handle multiple records at a time efficiently.
#### 2. Avoid DML/SOQL Queries in Loops
SOQL and DML are some of the most expensive operations we can perform within Salesforce Apex, and both have strict governor limits associated with them. 
#### 3. Avoid Hard-Coded IDs


#### 4. Explicitly Declare Sharing Model
When we begin writing a brand-new class, one of the first things we should do is declare our sharing model. If we require our code to bypass record access, we must always declare without sharing, but when we want it to enforce sharing rules, developers can often find themselves skipping this step.

#### 5. Use a Single Trigger per SObject Type


#### 6. Use SOQL for Loops
When we query a large set of records and assign the results to a variable, a large portion of our heap can be consumed.

#### 7. Test Multiple Scenarios
Salesforce mandates that we have at least 75% code coverage when we wish to deploy Apex code into production, and while having a high number of lines covered by tests is a good goal to have, it doesn’t tell the whole story when it comes to testing.

Writing tests only to achieve the code coverage requirement shows one thing: your code has been run, and it doesn’t actually provide any value other than showing that in a very specific scenario (which may or may not ever happen in practice!).

When writing our tests, we should worry about code coverage less, and instead concern ourselves with covering different use cases for our code, ensuring that we’re covering the scenarios in which the code is actually being run. We do this by writing multiple test methods, some of which may be testing the same methods and not generating additional covered lines, each of which runs our code under a different scenario.

#### 8. Avoid Nested Loops
Loops inside of loops – sometimes it can’t be avoided. You simply need to iterate over one thing related to another. Good stuff, right? While there may not seem to be anything immediately wrong here, and the code could very well run perfectly fine without running into performance issues or governor limits, the issue here is more one of maintainability and readability.
![image](https://github.com/user-attachments/assets/6cbe9b39-e714-48af-9808-839ded04052c)


Rather than using nested loops, a good strategy is to abstract your logic into separate methods (which perform the logic themselves). This way, when we’re looking at a block of code from a higher level, it is far easier to understand. Abstracting our code out like this also has other benefits, such as making it easier to test specific aspects of our code.
![image](https://github.com/user-attachments/assets/b9b4d8c5-a333-4eb4-9140-d47161e0ff1f)


#### 9. Have a Naming Convention
Naming conventions tend to be a hot topic in any developer team. The benefits are clear if everyone follows them, as they make it easier for other people in your team to understand what’s going on within an org.

#### 10. Avoid Business Logic in Triggers

#### 11. Avoid Returning JSON to Lightning Components
When we’re writing @AuraEnable methods for our Lightning Components, we frequently need to return more complex data structures, such as records, custom data types, or lists of these types.

An easy approach would be to serialize these objects into JSON, and then deserialize them within our component’s JavaScript (that is what the JS in JSON standards for after all!).
![image](https://github.com/user-attachments/assets/f624867b-e2a8-43f5-a933-f93a674f89f9)


However, this approach is actually an anti-pattern and can lead to some poor performance within our components. Instead, we should be directly returning these objects and letting the platform handle the rest for us.
![image](https://github.com/user-attachments/assets/c40f9be2-0e5a-4c6c-8b29-6848ca8638c2)

Converting our returned data into JSON results in us consuming large amounts of heap memory and spending many CPU cycles converting these objects into a lovely and long string


### Question : Best practices follwed for triggeres.
#### Answer : 


### Question : How to connect two systems (Integartion related questions- Connected app,named credentials)

### Question : Different types of flows.

### Question : What is the maximum number of records that can be processed by a trigger?

### Question : Context variables in triggers

### Question : Types of Events in AURA

### Question : Future method and Quable methods (Limitation, which senario you will go for future menthod)

### Question : How to set field level security in Apex (WITH SECURITY_ENFORCED)?

### Question : Best Practices for flows (Avoid hard code values, mixed DMLs, Avoid DML statements inside Loop, Error handling etc).

### Question : Mixed DML exception(Future method)

### Question : Schedulable classes: can we do callouts directly from schedulable class or not.

### Question : Imaging you are processing a batch fo 50000 and you have to seprate the process sucessful and failed record, how you will achieve it.

### Question : Questions related to field level security.

### Question : Database stateful and stateless (Difference and senario if you faced any)

### Question : How to pass the values from flow to Apex.

### Question : Field restriction by apex

### Question : application event in LWC

### Question : life cycle of LWC

### Question : Named credential

### Question :
