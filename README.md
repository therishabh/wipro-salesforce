# Wipro Salesforce interview Questions

### Question : What all asynchronous process available in salesforce.
#### Answer : 

### Question : Explain batch processing
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

### Question : Best Practices follwed for apex
#### Answer : 
##### 1. Bulkify Your Code
Bulkification of your code is the process of making your code able to handle multiple records at a time efficiently.
##### 2. Avoid DML/SOQL Queries in Loops
SOQL and DML are some of the most expensive operations we can perform within Salesforce Apex, and both have strict governor limits associated with them. 
##### 3. Avoid Hard-Coded IDs


##### 4. Explicitly Declare Sharing Model
When we begin writing a brand-new class, one of the first things we should do is declare our sharing model. If we require our code to bypass record access, we must always declare without sharing, but when we want it to enforce sharing rules, developers can often find themselves skipping this step.

##### 5. Use a Single Trigger per SObject Type


##### 6. Use SOQL for Loops
When we query a large set of records and assign the results to a variable, a large portion of our heap can be consumed.

##### 7. Test Multiple Scenarios
Salesforce mandates that we have at least 75% code coverage when we wish to deploy Apex code into production, and while having a high number of lines covered by tests is a good goal to have, it doesn’t tell the whole story when it comes to testing.

Writing tests only to achieve the code coverage requirement shows one thing: your code has been run, and it doesn’t actually provide any value other than showing that in a very specific scenario (which may or may not ever happen in practice!).

When writing our tests, we should worry about code coverage less, and instead concern ourselves with covering different use cases for our code, ensuring that we’re covering the scenarios in which the code is actually being run. We do this by writing multiple test methods, some of which may be testing the same methods and not generating additional covered lines, each of which runs our code under a different scenario.

##### 8. Avoid Nested Loops
Loops inside of loops – sometimes it can’t be avoided. You simply need to iterate over one thing related to another. Good stuff, right? While there may not seem to be anything immediately wrong here, and the code could very well run perfectly fine without running into performance issues or governor limits, the issue here is more one of maintainability and readability.

Rather than using nested loops, a good strategy is to abstract your logic into separate methods (which perform the logic themselves). This way, when we’re looking at a block of code from a higher level, it is far easier to understand. Abstracting our code out like this also has other benefits, such as making it easier to test specific aspects of our code.

##### 9. Have a Naming Convention

##### 10. Avoid Business Logic in Triggers

##### 11. Avoid Returning JSON to Lightning Components


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
