# Wipro Salesforce interview Questions

### Question : What all asynchronous process available in salesforce.
#### Answer : 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Question : Explain batch processing
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

### Question : Best Practices follwed for apex
#### Answer : 

https://www.salesforceben.com/12-salesforce-apex-best-practices/

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
https://www.pantherschools.com/apex-trigger-best-practices-in-salesforce/

As a developer, to develop effective triggers we can follow the below best practices
- One trigger per object
- Logic Less Trigger
- Context-specific handler methods
- Avoid SOQL Query inside for loop
- Avoid hardcoding IDs
- Avoid nested for loop
- Avoid DML inside for loop
- Bulkify Your Code
- Enforced Sharing in Salesforce
- Use @future Appropriately
- Use WHERE Clause in SOQL Query
- Use Test-Driven Development

### Question : How to connect two systems (Integartion related questions- Connected app,named credentials)
#### Answer :

https://github.com/therishabh/salesforce-apex/blob/main/README.md#integration-in-salesforce


### Question : Different types of flows.
#### Answer :

Salesforce Flows can be classified into five subtypes: <br/><br/>
**Screen Flows**<br/>
Require user interaction and include screens, local actions, steps, choices, or dynamic choices. For example, a customer survey after a support case is completed.<br/><br/>
**Schedule-Triggered Flows**<br/>
Run in the background at a specified time and at a repeated frequency to perform actions on a batch of records. For example, a financial firm might need to generate reports at the end of every financial quarter.<br/><br/>
**Autolaunched Flows**<br/>
Run without user interaction and don't support screens, local actions, choices, or choice sets. They are triggered by a specific event or record update and can automate complicated tasks like sending email notifications, modifying records, or creating new records. For example, when a large opportunity closes, send an alert to the right people on your team.<br/><br/>
**Record-Triggered Flows**<br/>
Run in the background, either before or after a record save. They are triggered when a record is created or updated and can be used to automate processes such as updating related records or sending notifications to users. For example, when a large opportunity closes, send an alert to the right people on your team.<br/><br/>
**Platform Event-Triggered Flows**<br/>
Run when a platform event message is received.<br/><br/>

### Question : What is the maximum number of records that can be processed by a trigger?
#### Answer :
**A trigger can process a maximum of 200 records at a time.**<br/><br/>

However, if you're dealing with a larger number of records, Salesforce will automatically break down the process into chunks of 200. For example, if you have 1000 records to process, the trigger will be called 5 times, each time handling 200 records.<br/><br/>

Additional Notes:<br/>
Platform Event triggers can handle up to 2000 records per chunk, which is different from standard object triggers.<br/><br/>

### Question : Context variables in triggers
#### Answer :

https://github.com/therishabh/salesforce-apex/blob/main/README.md#trigger-context-variables

### Question : Types of Events in AURA
#### Answer :

### Question : Future method and Quable methods (Limitation, which senario you will go for future menthod)
#### Answer :

### Question : How to set field level security in Apex (WITH SECURITY_ENFORCED)?
#### Answer :

Setting field-level security in Apex ensures that your code respects the field-level security settings configured in Salesforce. Using the **WITH SECURITY_ENFORCED** keyword in SOQL queries is one way to enforce field-level security checks. Here's how you can use it:<br/><br/>

**Enforcing Field-Level Security with WITH SECURITY_ENFORCED**<br/>
When you add WITH SECURITY_ENFORCED to your SOQL queries, Salesforce will automatically enforce field- and object-level security checks. If a user does not have access to a field or object, the query will fail, ensuring that your code does not inadvertently expose restricted data.<br/><br/>

**Example Usage**<br/>
Here's an example of how to use WITH SECURITY_ENFORCED in a SOQL query:<br/>

```apex
try {
    List<Account> accounts = [SELECT Id, Name, Phone FROM Account WITH SECURITY_ENFORCED WHERE IsActive = true];
    // Process the accounts
    for (Account acc : accounts) {
        System.debug('Account Name: ' + acc.Name);
    }
} catch (Exception e) {
    System.debug('Insufficient permissions: ' + e.getMessage());
}
```

### Question : Best Practices for flows (Avoid hard code values, mixed DMLs, Avoid DML statements inside Loop, Error handling etc).

### Question : Mixed DML exception(Future method)

### Question : Schedulable classes: can we do callouts directly from schedulable class or not.

### Question : Imaging you are processing a batch fo 50000 and you have to seprate the process sucessful and failed record, how you will achieve it.
**Answer :**<br/>
Processing large batches of records in Salesforce requires careful handling to ensure that successful and failed records are managed properly. Here’s how you can achieve this when processing a batch of 50,000 records using Batch Apex, with separate handling for successful and failed records:<br/><br/>

**Steps**
- Define Batch Apex Class: Implement the Database.Batchable interface.
- Separate Successful and Failed Records: Use collections to keep track of successful and failed records during processing.
- Handle Results in the Finish Method: Log or process the successful and failed records accordingly.

**Example Batch Apex Class**<br/>
Here’s a complete example demonstrating how to process 50,000 records, separating successful and failed records: <br/>

```apex
global class MyBatchClass implements Database.Batchable<SObject>, Database.Stateful {
    // Lists to keep track of successful and failed records
    private List<Account> successfulRecords = new List<Account>();
    private List<Account> failedRecords = new List<Account>();
    
    global Database.QueryLocator start(Database.BatchableContext BC) {
        // Query to fetch the records to be processed
        return Database.getQueryLocator('SELECT Id, Name FROM Account WHERE ...');
    }

    global void execute(Database.BatchableContext BC, List<Account> scope) {
        // Process each batch of records
        for (Account acc : scope) {
            try {
                // Perform some processing (e.g., update the name)
                acc.Name = acc.Name + ' - Processed';
                // Add to successful records list
                successfulRecords.add(acc);
            } catch (Exception e) {
                // Add to failed records list with an error message
                acc.addError('Processing failed: ' + e.getMessage());
                failedRecords.add(acc);
            }
        }
        
        // Perform DML operations
        if (!successfulRecords.isEmpty()) {
            try {
                update successfulRecords;
            } catch (Exception e) {
                // Handle exception if update fails for any record
                for (Account acc : successfulRecords) {
                    acc.addError('Update failed: ' + e.getMessage());
                    failedRecords.add(acc);
                }
            }
        }
    }

    global void finish(Database.BatchableContext BC) {
        // Log successful records
        for (Account acc : successfulRecords) {
            System.debug('Successfully processed account: ' + acc.Id);
        }
        
        // Log failed records
        for (Account acc : failedRecords) {
            System.debug('Failed to process account: ' + acc.Id + ' - Error: ' + acc.getErrors()[0].getMessage());
        }
        
        // Further handling of failed records (e.g., reprocess, notify admin)
    }
}

```

**Explanation**
- **Stateful Interface:** The **Database.Stateful** interface is used to maintain the state across batch transactions, allowing you to keep track of successful and failed records.
- **Collections for Successful and Failed Records:** Two lists (successfulRecords and failedRecords) are used to track records that are processed successfully and those that fail during processing.
- **Try-Catch Blocks:** In the execute method, each record is processed within a try-catch block to handle exceptions individually and categorize the records accordingly.
- **Error Handling:** Failed records are added to the failedRecords list with an appropriate error message.
- **Finish Method:** In the finish method, both successful and failed records are logged. You can extend this part to send notifications, write to a custom object, or perform other actions as needed.


### Question : Questions related to field level security.

### Question : Database stateful and stateless (Difference and senario if you faced any)
https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

In Salesforce, Batch Apex classes can implement either the `Database.Stateful` or `Database.Batchable` interfaces. Understanding the difference between these two interfaces, as well as when and how to use them, is important for developing efficient and effective batch processes.

### Difference Between Stateful and Stateless

1. **Database.Stateful**:
    - **Definition**: Implements the `Database.Stateful` interface to maintain state across transaction boundaries.
    - **Usage**: Use `Database.Stateful` when you need to maintain state information (like aggregate values, collections, etc.) across multiple batch transactions.
    - **Example**: Tracking processed record IDs, maintaining counters, or aggregating values across all batches.

2. **Database.Batchable** (Stateless):
    - **Definition**: Implements the `Database.Batchable` interface without the `Database.Stateful` interface, which means it is stateless.
    - **Usage**: Use `Database.Batchable` when you do not need to maintain state across batch transactions. Each batch transaction is independent and does not share any data with other transactions.
    - **Example**: Processing records independently where no shared state is required.

### Example Scenario

#### Scenario: Aggregate Calculation Across Batches

Imagine you have a batch process that needs to calculate the total amount of all `Opportunity` records and update a custom field on the `Account` record with the aggregated value. Since this calculation requires maintaining a running total across multiple batches, you would use `Database.Stateful`.

#### Example Stateful Batch Apex Class

```apex
global class AggregateOpportunitiesBatch implements Database.Batchable<SObject>, Database.Stateful {
    private Decimal totalAmount = 0; // Maintain state

    global Database.QueryLocator start(Database.BatchableContext BC) {
        return Database.getQueryLocator('SELECT Amount, AccountId FROM Opportunity WHERE IsClosed = true');
    }

    global void execute(Database.BatchableContext BC, List<SObject> scope) {
        for (Opportunity opp : (List<Opportunity>) scope) {
            totalAmount += opp.Amount;
        }
    }

    global void finish(Database.BatchableContext BC) {
        // Update Accounts with the aggregated totalAmount
        List<Account> accountsToUpdate = [SELECT Id FROM Account WHERE Id IN (SELECT AccountId FROM Opportunity WHERE IsClosed = true)];
        for (Account acc : accountsToUpdate) {
            acc.Total_Opportunity_Amount__c = totalAmount;
        }
        update accountsToUpdate;
        System.debug('Total Opportunity Amount: ' + totalAmount);
    }
}
```

### Example Stateless Batch Apex Class

For a stateless scenario, consider a batch process that updates a field on each `Contact` record independently, such as setting a `Last_Processed__c` date field to the current date.

```apex
global class UpdateContactsBatch implements Database.Batchable<SObject> {
    global Database.QueryLocator start(Database.BatchableContext BC) {
        return Database.getQueryLocator('SELECT Id FROM Contact');
    }

    global void execute(Database.BatchableContext BC, List<SObject> scope) {
        for (Contact con : (List<Contact>) scope) {
            con.Last_Processed__c = System.today();
        }
        update scope;
    }

    global void finish(Database.BatchableContext BC) {
        System.debug('Contact records updated with the current date.');
    }
}
```

### Summary of Differences and Usage

| Aspect                | Database.Stateful                       | Database.Stateless                          |
|-----------------------|-----------------------------------------|---------------------------------------------|
| **State Maintenance** | Maintains state across transactions     | Does not maintain state across transactions |
| **Use Case**          | Aggregations, counters, accumulating data | Independent record processing               |
| **Example**           | Aggregating `Opportunity` amounts       | Updating `Contact` fields independently     |

### Scenarios Faced

#### Scenario 1: Aggregation and Counting

**Situation**: I needed to process a large number of records and keep a running count of how many records met certain criteria (e.g., number of closed Opportunities). This required using `Database.Stateful` to maintain the count across multiple batch transactions.

**Implementation**: Using a counter variable in a stateful batch class to maintain the running total and update a summary field on a parent record at the end.

#### Scenario 2: Independent Record Updates

**Situation**: I had to update a specific field on all `Contact` records in the system, and each update was independent of the others (e.g., setting a flag or date field).

**Implementation**: A stateless batch class was used because each `Contact` record was processed independently, and no shared state was required.

By understanding and applying the differences between `Database.Stateful` and `Database.Batchable` (stateless), you can choose the appropriate approach for your batch processing needs, ensuring efficient and effective execution of your Salesforce batch processes.


### Question : How to pass the values from flow to Apex.

https://github.com/therishabh/salesforce-apex/blob/main/README.md#invocable-method

Passing values from a Salesforce Flow to an Apex class involves creating an Apex invocable method that accepts input parameters. These parameters can then be mapped to Flow variables when the Flow is designed. Here is a step-by-step guide on how to achieve this:

### Steps to Pass Values from Flow to Apex Class

1. **Create the Apex Class with an Invocable Method**:
   - Define an Apex class.
   - Create an inner class to hold the input parameters.
   - Annotate the method with `@InvocableMethod`.

2. **Define Input Parameters in the Flow**:
   - Use the Flow Builder to create variables.
   - Map these variables to the inputs of the invocable method.

### Example

Let's say you want to pass a contact's first name, last name, and email from a Flow to an Apex class to create a new Contact record.

#### Step 1: Create the Apex Class

```apex
public class CreateContactFromFlow {
    
    // Define an inner class to hold the input parameters
    public class ContactInput {
        @InvocableVariable
        public String firstName;
        
        @InvocableVariable
        public String lastName;
        
        @InvocableVariable
        public String email;
    }
    
    // Define the invocable method
    @InvocableMethod(label='Create Contact' description='Create a new contact from Flow')
    public static void createContact(List<ContactInput> inputParams) {
        List<Contact> contactsToCreate = new List<Contact>();
        
        for (ContactInput input : inputParams) {
            Contact newContact = new Contact(
                FirstName = input.firstName,
                LastName = input.lastName,
                Email = input.email
            );
            contactsToCreate.add(newContact);
        }
        
        if (!contactsToCreate.isEmpty()) {
            insert contactsToCreate;
        }
    }
}
```

#### Step 2: Create the Flow and Map Variables

1. **Open Flow Builder**: Go to Setup -> Process Automation -> Flows and click "New Flow".
2. **Select Screen Flow or Auto-launched Flow**: Choose the type of Flow based on your requirements.
3. **Create Variables**:
   - Create three variables: `firstName`, `lastName`, and `email`.
   - Ensure the data types match those expected by the Apex class (`Text` in this case).

4. **Add an Action**:
   - In the Flow, add an "Action" element.
   - Search for the "Create Contact" action (the label you defined in the `@InvocableMethod` annotation).
   - Map the Flow variables to the input parameters of the invocable method.

5. **Finish the Flow**:
   - Complete the Flow by adding any other necessary elements (e.g., screens, decisions, etc.).
   - Save and activate the Flow.

### Detailed Steps in Flow Builder

1. **Create Variables**:
   - Click "Manager" on the left panel.
   - Click "New Resource" and select "Variable".
   - Create `firstName`, `lastName`, and `email` variables with `Text` data type.

2. **Add Action Element**:
   - Drag the "Action" element onto the canvas.
   - In the Action search box, type "Create Contact".
   - Select the "Create Contact" action.

3. **Map Flow Variables**:
   - In the Action configuration, map the Flow variables to the inputs of the invocable method.
     - `firstName` -> `firstName`
     - `lastName` -> `lastName`
     - `email` -> `email`

4. **Complete the Flow**:
   - Add any other elements as needed.
   - Connect the elements to define the Flow logic.
   - Save and activate the Flow.

### Example Flow Configuration

Here's how the Action configuration might look:

- **Label**: Create Contact
- **API Name**: Create_Contact
- **Set Input Values**:
  - `firstName`: {!firstName}
  - `lastName`: {!lastName}
  - `email`: {!email}

### Conclusion

By following these steps, you can effectively pass values from a Flow to an Apex class in Salesforce. This approach leverages the power of Flow for user-friendly configuration and the flexibility of Apex for complex business logic.


### Question : Field restriction by apex

### Question : application event in LWC

### Question : life cycle of LWC

https://github.com/therishabh/salesforce-lwc?tab=readme-ov-file#lifecycle-hooks

### Question : Named credential

### Question : Mixed DML exception
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Open Id connect for integration
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Calling one batch to another batch
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : What are context variables in triggers
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Is there a way to callout triggers
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : About recursive triggers
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Reason for bulkification of your code
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Field level permission thru org level
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Database operation and syntax
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : What are public component in LWC
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Types of decorators in LWC
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Difference between, trigger.old and Trigger.oldmap
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Not using @future annotation in webservices callout, what will happen
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : How can you implement recursive trigger in salesforce
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Composite request
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Component event and application event difference
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : What is LDS(Lightning Data Services) in lwc
#### Answer : 
Lightning Data Service (LDS) is a powerful tool provided by Salesforce that allows Lightning Web Components (LWC) to interact with Salesforce data without the need for Apex code. It operates on the client-side and offers several key features that streamline data retrieval and management within LWC.

One of the key benefits of LDS is its client-side caching mechanism. When a component fetches data using LDS, the data is cached locally in the browser’s memory. Subsequent requests for the same data within the same session can be served from the cache, eliminating the need for additional server round trips. This improves performance and responsiveness of the application, especially in scenarios where the same data is accessed frequently.

**Benefits Over Traditional Apex Data Queries:** </br>
Compared to traditional Apex data queries, LDS offers several advantages:</br></br>

**`Reduced Server Load`:** Since data is fetched and cached on the client side, LDS reduces the load on the Salesforce server by minimizing the number of server requests.</br></br>
**`Faster Response Times`:** With client-side caching, LDS can serve data more quickly, leading to faster response times and improved user experience.</br></br>
**`Enhanced Offline Support`:** LDS supports offline data access, allowing components to continue functioning even when the user is offline or experiencing connectivity issues.</br></br>
**`Automatic Record Updates`:** LDS automatically detects changes to records and updates the local cache accordingly, ensuring that components always have access to the latest data without manual refreshing.</br></br>
**Example:**</br>
Let’s consider an example where we have a Lightning Web Component that displays a list of accounts using LDS.</br></br>

```html
<!-- accountsList.html -->
<template>
    <lightning-card title="Accounts List">
        <template if:true={accounts}>
            <ul>
                <template for:each={accounts} for:item="account">
                    <li key={account.Id}>{account.Name}</li>
                </template>
            </ul>
        </template>
        <template if:false={accounts}>
            No accounts found.
        </template>
    </lightning-card>
</template>
```

```apex
// accountsList.js
import { LightningElement, wire } from 'lwc';
import { getListUi } from 'lightning/uiListApi';
import ACCOUNT_OBJECT from '@salesforce/schema/Account';
 
export default class AccountsList extends LightningElement {
    @wire(getListUi, { objectApiName: ACCOUNT_OBJECT, listViewApiName: 'All' })
    wiredAccounts({ error, data }) {
        if (data) {
            this.accounts = data.records.records;
        } else if (error) {
            console.error(error);
        }
    }
}
```

**Output:** </br>
![image](https://github.com/user-attachments/assets/5eeddd32-4c94-48b8-ab12-1d169373d023)

In this example, we use the `getListUi` wire adapter from `lightning/uiListApi` to fetch a list of accounts. The result is automatically cached by LDS, and subsequent requests for the same data will be served from the cache, resulting in improved performance and responsiveness.</br></br>

The base component of Lightning Data Service are</br>

`lightning-record-edit-form` — Displays an editable form.</br>
`lightning-record-view-form` — Displays a read-only form.</br>
`lightning-record-form` — Supports edit, view, and read-only modes.</br>

-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : SOQL 101 Exception
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

### Question : Nested aura component can we have, which event will execute first
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------


