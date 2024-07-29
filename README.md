# Wipro Salesforce interview Questions

### Summary
[Question : What all asynchronous process available in salesforce.](#question--what-all-asynchronous-process-available-in-salesforce)<br/>
Question : Explain batch processing<br/>
Question : Best Practices follwed for apex<br/>
Question : Best practices follwed for triggeres.<br/>
Question : How to connect two systems (Integartion related questions- Connected app,named credentials)<br/>
Question : Different types of flows.<br/>
Question : What is the maximum number of records that can be processed by a trigger?<br/>
Question : Context variables in triggers<br/>
Question : Future method and Quable methods (Limitation, which senario you will go for future menthod)<br/>
Question : How to set field level security in Apex (WITH SECURITY_ENFORCED)?<br/>
Question : Best Practices for flows (Avoid hard code values, mixed DMLs, Avoid DML statements inside Loop, Error handling etc).<br/>
Question : Mixed DML exception(Future method)<br/>
Question : Schedulable classes: can we do callouts directly from schedulable class or not.<br/>
Question : Imaging you are processing a batch fo 50000 and you have to seprate the process sucessful and failed record, how you will achieve it.<br/>
Question : Questions related to field level security.<br/>
Question : Database stateful and stateless (Difference and senario if you faced any)<br/>
Question : How to pass the values from flow to Apex.<br/>
Question : Field restriction by apex<br/>
Question : application event in LWC<br/>
Question : life cycle of LWC<br/>
Question : Named credential<br/>
Question : Mixed DML exception<br/>
Question : Open Id connect for integration<br/>
Question : Calling one batch to another batch<br/>
Question : Is there a way to callout triggers<br/>
[Question : About recursive triggers](#question--about-recursive-triggers)<br/>
[Question : Reason for bulkification of your code](#question--reason-for-bulkification-of-your-code)<br/>
[Question : Database operation and syntax](#question--database-operation-and-syntax)<br/>
Question : What are public component in LWC<br/>
Question : Types of decorators in LWC<br/>
Question : Difference between, trigger.old and Trigger.oldmap<br/>
Question : Not using @future annotation in webservices callout, what will happen<br/>
Question : How can you implement recursive trigger in salesforce<br/>
Question : Composite request<br/>
Question : Component event and application event difference<br/>
Question : What is LDS(Lightning Data Services) in lwc<br/>
Question : SOQL 101 Exception<br/>
Question : Nested aura component can we have, which event will execute first<br/>
Question : Deployment tool.. CI/CD process.. how to setup<br/>
Question : explain one LWC component created by you.<br/>
Question : How will you get the data from Apex to LWC<br/>
Question : how many ways we can query the data<br/>
Question : What is Wire method<br/>
Question : Concept of promises in LWC ?<br/>
Question : how to establish communication between components<br/>
Question : Integration- breif what you have done.<br/>
Question : diff between userflow and web server flow ( connected App authorization)?<br/>
Question : serve side - how the authentication is happen?<br/>
Question : Platform event?<br/>
Question : Managed Package- exp<br/>
Question : Aura - share the method with another Aura comp?<br/>
Question : styling hooks in LWC?<br/>
Question : have you worked in service console.<br/>
Question : How did you do deployment<br/>
Question : Involved in any deployment<br/>
Question : Can we use multiple decorators for one property<br/>
Question : what is the need of LWC, when we are already having Aura<br/>
Question : How will you overcome the governor limit<br/>
Question : How to call from one batch class into another batch class<br/>
Question : Why apex callout is always asyc<br/>
Question : SECURITY_ENFORCE use in SOQL<br/>
Question : Security question on Triggers<br/>
Question : Can we pass one batch data to another batch process<br/>
Question : Types of Async classes<br/>
Question : About Iterable class in Batchable<br/>
Question : PMD violations<br/>
Question : Devops process<br/>
Question : Imperative apex<br/>
Question : Difference between aura and LWC component<br/>
Question : Types of Events in AURA<br/>



## Question : What all asynchronous process available in salesforce.
#### Answer : 
Salesforce provides several asynchronous processing options to handle operations that require large volumes of data, complex processing, or tasks that should not be performed in a synchronous transaction. Here's a comprehensive list of asynchronous processes available in Salesforce:

1. **Future Methods**
2. **Batch Apex**
3. **Scheduled Apex**
4. **Queueable Apex**
5. **Apex REST Callouts**

### 1. Future Methods

- **Use Case**: Perform long-running operations or callouts to external services without blocking the main thread.
- **Key Points**:
  - Methods annotated with `@future`.
  - Limited to 50 future method calls per Apex invocation.
  - Future methods cannot return values.
  - Cannot be chained.

#### Example
```apex
public class FutureMethodExample {
    @future(callout=true)
    public static void callExternalService() {
        // Callout code
    }
}
```

### 2. Batch Apex

- **Use Case**: Process large volumes of records asynchronously.
- **Key Points**:
  - Implement `Database.Batchable` interface.
  - Can handle millions of records.
  - Allows for stateful processing using `Database.Stateful`.

#### Example
```apex
public class BatchApexExample implements Database.Batchable<SObject> {
    public Database.QueryLocator start(Database.BatchableContext BC) {
        return Database.getQueryLocator('SELECT Id, Name FROM Account');
    }
    public void execute(Database.BatchableContext BC, List<SObject> scope) {
        // Process each batch of records
    }
    public void finish(Database.BatchableContext BC) {
        // Final operations
    }
}
```

### 3. Scheduled Apex

- **Use Case**: Schedule a batch job or other Apex code to run at specific times.
- **Key Points**:
  - Implement `Schedulable` interface.
  - Use `System.schedule` to schedule the job.

#### Example
```apex
public class ScheduledApexExample implements Schedulable {
    public void execute(SchedulableContext SC) {
        // Code to execute
    }
}

// Schedule the job
System.schedule('Job Name', '0 0 12 * * ?', new ScheduledApexExample());
```

### 4. Queueable Apex

- **Use Case**: Chain jobs and perform complex operations asynchronously.
- **Key Points**:
  - Implement `Queueable` interface.
  - Supports job chaining.
  - More flexible than future methods.

#### Example
```apex
public class QueueableApexExample implements Queueable {
    public void execute(QueueableContext context) {
        // Code to execute
    }
}

// Enqueue the job
Id jobId = System.enqueueJob(new QueueableApexExample());
```

### 5. Apex REST Callouts

- **Use Case**: Make HTTP requests to external services asynchronously.
- **Key Points**:
  - Use `@future(callout=true)` for asynchronous callouts.
  - Can be combined with future methods or Queueable Apex.

#### Example
```apex
public class RestCalloutExample {
    @future(callout=true)
    public static void makeCallout() {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('https://example.com/api');
        req.setMethod('GET');
        Http http = new Http();
        HttpResponse res = http.send(req);
    }
}
```


-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Explain batch processing
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Best Practices follwed for apex
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Best practices follwed for triggeres.
#### Answer :  
https://www.pantherschools.com/apex-trigger-best-practices-in-salesforce/

https://github.com/therishabh/salesforce-apex/blob/main/README.md#trigger

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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How to connect two systems (Integartion related questions- Connected app,named credentials)
#### Answer :

https://github.com/therishabh/salesforce-apex/blob/main/README.md#integration-in-salesforce

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Different types of flows.
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : What is the maximum number of records that can be processed by a trigger?
#### Answer :
**A trigger can process a maximum of 200 records at a time.**<br/><br/>

However, if you're dealing with a larger number of records, Salesforce will automatically break down the process into chunks of 200. For example, if you have 1000 records to process, the trigger will be called 5 times, each time handling 200 records.<br/><br/>

Additional Notes:<br/>
Platform Event triggers can handle up to 2000 records per chunk, which is different from standard object triggers.<br/><br/>

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Context variables in triggers
#### Answer :

https://github.com/therishabh/salesforce-apex/blob/main/README.md#trigger-context-variables

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Future method and Quable methods (Limitation, which senario you will go for future menthod)
#### Answer :

https://github.com/therishabh/salesforce-apex/blob/main/README.md#asynchronous-processing-basics

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How to set field level security in Apex (WITH SECURITY_ENFORCED)?
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Best Practices for flows (Avoid hard code values, mixed DMLs, Avoid DML statements inside Loop, Error handling etc).
#### Answer :
https://www.salesforceben.com/salesforce-flow-best-practices/

Here are the best Salesforce Flow practices I regularly follow when developing my flows.
1. Always Test Your Flows
2. Consider Using Subflows
3. Never Perform DML Statements in Loops
4. Document Your Flows
5. Never Hard Code Ids (Use Constants if You Must)
6. Plan for Faults (and Handle Them)
7. Make Use of Schedule-Triggered Flow and Asynchronous Paths

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Mixed DML exception (Future method)
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#future-method-in-apex
</br></br>
A mixed DML Operation Error comes when you try to perform DML operations on setup and non-setup objects in a single transaction. </br></br>

Setup objects are the sObjects that affect the user’s access to records in the organization. Here are examples of the Setup Objects:</br>

1. ObjectPermissions
2. PermissionSet
3. PermissionSetAssignment
4. QueueSObject
5. Territory
6. UserTerritory
7. UserRole
8. User

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Schedulable classes: can we do callouts directly from schedulable class or not.
#### Answer :

**Salesforce does not allow us to make callouts from Schedulable classes** </br>

We used to get **“System.CalloutException: Callout from scheduled Apex not supported”** Error when we are making a web service callout from a class which is implementing Database.Schedulable interface because Salesforce does not allow us to make callouts from Schedulable classes. </br></br>

@future method : A future runs as asynchronously. You can call a future method for executing long-running operations, such as callouts to external Web services or any operation you’d like to run in its own thread, on its own time </br>

**Scheduler Class** </br>
```apex
global class SampleScheduler implements Schedulable{
    
    global void execute(SchedulableContext sc) 
    {        
 
      BatchUtilClass.futureMethodSample();
    }    
}
```
<br/>
Future Class Method</br>

```apex

public class BatchUtilClass {
    @future(callout=true)
    public static void futureMethodSample() {
        Http http = new Http();
        HttpRequest request = new HttpRequest();
        request.setEndpoint('https://th-apex-http-callout.herokuapp.com/animals');
        request.setMethod('GET');
        HttpResponse response = http.send(request);

        if (response.getStatusCode() == 200) {
            Map<String, Object> results = (Map<String, Object>) JSON.deserializeUntyped(response.getBody());
            List<Object> animals = (List<Object>) results.get('animals');
            System.debug('Received the following animals:');
            for (Object animal: animals) {
                System.debug(animal);
            }
        }
    }
}

```
https://www.apexhours.com/system-calloutexception-callout-from-scheduled-apex-not-supported/

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Imaging you are processing a batch fo 50000 and you have to seprate the process sucessful and failed record, how you will achieve it.
#### Answer : 
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Questions related to field level security.
#### Answer : 

Field-Level Security (FLS) determines whether a user can view or edit the data in a specific field on an object. It is a key component of Salesforce’s security model and is applied to profiles and permission sets to control access to sensitive data.

https://github.com/therishabh/wipro-salesforce/blob/main/README.md#question--how-to-set-field-level-security-in-apex-with-security_enforced

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Database stateful and stateless (Difference and senario if you faced any)
#### Answer : 
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How to pass the values from flow to Apex.
#### Answer : 
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

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Field restriction by apex
#### Answer : 

https://github.com/therishabh/salesforce-apex/blob/main/README.md#user-mode-vs-system-mode

In Salesforce, Field-Level Security (FLS) is an essential component of data security, ensuring that users can only view or edit fields they have permission to access. While Field-Level Security is primarily managed through profiles and permission sets, you might need to handle field restrictions programmatically in Apex to respect these settings or implement additional security measures.

#### How to Handle Field Restrictions in Apex

#### 1. **Check Field-Level Security Programmatically**

Before performing operations on a field, you should check if the current user has access to that field. Salesforce provides methods in the `Schema` class to check field accessibility.

**Example: Checking Field Accessibility**

```apex
// Example to check if the current user has access to a field
public class FieldSecurityUtil {
    public static Boolean isFieldAccessible(Schema.SObjectField field) {
        Schema.DescribeFieldResult fieldDescribe = field.getDescribe();
        return fieldDescribe.isAccessible();
    }
    
    public static Boolean isFieldEditable(Schema.SObjectField field) {
        Schema.DescribeFieldResult fieldDescribe = field.getDescribe();
        return fieldDescribe.isUpdateable();
    }
}
```

**Usage in Apex Code**

```apex
if (FieldSecurityUtil.isFieldAccessible(Account.MyField__c)) {
    // Proceed with logic for accessible field
    Account acc = [SELECT Id, MyField__c FROM Account LIMIT 1];
    System.debug('Field value: ' + acc.MyField__c);
} else {
    System.debug('Field is not accessible.');
}
```

#### 2. **Handle Field-Level Security in Triggers**

When writing triggers, ensure that your code respects field-level permissions. For example, if your trigger updates fields, check if the fields are editable.

**Example: Trigger Code**

```apex
trigger AccountTrigger on Account (before update) {
    for (Account acc : Trigger.new) {
        if (FieldSecurityUtil.isFieldEditable(Account.MyField__c)) {
            // Logic to update the field if it is editable
            acc.MyField__c = 'New Value';
        } else {
            // Logic for fields that are not editable
            System.debug('Field MyField__c is not editable.');
        }
    }
}
```

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : application event in LWC
#### Answer : 

Events are used in LWC for components communication. There are typically 3 approaches for communication between the components using events.

1. Parent to Child Event communication in Lightning web component
2. Child to Parent Event Communication in Lightning Web Component
3. Publish Subscriber model (PubSub model) in Lightning Web Component or LMS (Two components which doesn’t have a direct relation)

![image](https://github.com/user-attachments/assets/cef17a11-06e7-4d2c-ba4c-005d04df6bf3)

https://github.com/therishabh/salesforce-lwc?tab=readme-ov-file#parent-to-child-communication

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : life cycle of LWC
#### Answer : 
https://github.com/therishabh/salesforce-lwc?tab=readme-ov-file#lifecycle-hooks

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Named credential
#### Answer : 

In Salesforce, a Named Credential is a configuration that allows you to securely store authentication details for external services. This feature is particularly useful for integrating with external systems or APIs, as it simplifies the management of authentication and improves security by keeping sensitive information out of the codebase.

##### Using Named Credentials in Apex

You can use Named Credentials in Apex code to make HTTP requests without hardcoding credentials. Salesforce handles authentication automatically based on the Named Credential configuration.

**Example: Making an HTTP Request**

```apex
public class MyHttpClient {
    public void callExternalService() {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('callout:My_Named_Credential/some/resource');
        req.setMethod('GET');
        
        Http http = new Http();
        HttpResponse res = http.send(req);
        
        if (res.getStatusCode() == 200) {
            // Process response
            System.debug(res.getBody());
        } else {
            // Handle error
            System.debug('Error: ' + res.getStatusCode() + ' ' + res.getStatus());
        }
    }
}
```

In this example, `callout:My_Named_Credential` refers to the Named Credential you configured, and Salesforce automatically handles the authentication.

Named Credentials in Salesforce are a powerful feature for securely managing authentication details when integrating with external services. They simplify the process of making secure HTTP requests and managing credentials, enhancing both security and maintainability of your integration solutions.

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Open Id connect for integration
#### Answer : 

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Calling one batch to another batch
#### Answer : 
https://www.emizentech.com/blog/call-batch-apex-from-another-batch-apex.html

https://github.com/therishabh/salesforce-apex/blob/main/README.md#batch-apex

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Is there a way to callout triggers
#### Answer : 
In Salesforce, "callout triggers" typically refers to making HTTP callouts from triggers, but it’s important to note that Salesforce does not support direct HTTP callouts from triggers due to governor limits and best practices. 

Here’s how you can indirectly achieve callouts from triggers using asynchronous methods:

#### Indirect Callouts from Triggers

#### 1. **Using Queueable Apex**

Queueable Apex allows you to perform asynchronous operations, including HTTP callouts. You can call a Queueable Apex class from a trigger to handle the callout.

**Steps to Use Queueable Apex for Callouts**

1. **Create the Queueable Apex Class**

   This class will perform the HTTP callout.

   ```apex
   public class CalloutQueueable implements Queueable {
       public void execute(QueueableContext context) {
           HttpRequest req = new HttpRequest();
           req.setEndpoint('https://api.example.com/resource');
           req.setMethod('GET');
           req.setHeader('Content-Type', 'application/json');
           
           Http http = new Http();
           HttpResponse res = http.send(req);
           
           if (res.getStatusCode() == 200) {
               // Process response
               System.debug(res.getBody());
           } else {
               // Handle error
               System.debug('Error: ' + res.getStatusCode() + ' ' + res.getStatus());
           }
       }
   }
   ```

2. **Call the Queueable Apex Class from the Trigger**

   In your trigger, you can enqueue the Queueable job.

   ```apex
   trigger AccountTrigger on Account (after insert) {
       if (Trigger.isAfter && Trigger.isInsert) {
           // Call Queueable Apex to perform callout
           System.enqueueJob(new CalloutQueueable());
       }
   }
   ```

#### 2. **Using Future Methods**

Future methods also allow asynchronous processing but are less flexible than Queueable Apex. They can be used for simple asynchronous operations and are limited in their ability to chain or handle complex scenarios.

**Steps to Use Future Methods for Callouts**

1. **Create a Future Method**

   Define a method in a class marked with `@future` to perform the callout.

   ```apex
   public class CalloutFuture {
       @future(callout=true)
       public static void makeCallout() {
           HttpRequest req = new HttpRequest();
           req.setEndpoint('https://api.example.com/resource');
           req.setMethod('GET');
           req.setHeader('Content-Type', 'application/json');
           
           Http http = new Http();
           HttpResponse res = http.send(req);
           
           if (res.getStatusCode() == 200) {
               // Process response
               System.debug(res.getBody());
           } else {
               // Handle error
               System.debug('Error: ' + res.getStatusCode() + ' ' + res.getStatus());
           }
       }
   }
   ```

2. **Call the Future Method from the Trigger**

   Invoke the future method from your trigger.

   ```apex
   trigger AccountTrigger on Account (after insert) {
       if (Trigger.isAfter && Trigger.isInsert) {
           // Call Future Method to perform callout
           CalloutFuture.makeCallout();
       }
   }
   ```

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : About recursive triggers
#### Answer : 
https://github.com/therishabh/salesforce-apex/blob/main/README.md#how-to-avoid-recursion-in-trigger

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Reason for bulkification of your code
#### Answer : 
**Bulkification** in Salesforce refers to the practice of designing Apex code to handle multiple records efficiently in a single execution context.
#### Reasons for Bulkification

1. **Governor Limits Compliance**

   Salesforce enforces various governor limits, such as limits on the number of SOQL queries, DML operations, and CPU time. Non-bulkified code can easily exceed these limits if it processes records individually. Bulkified code ensures that operations are performed in bulk, minimizing the number of SOQL queries and DML statements, and helps avoid hitting these limits.

2. **Performance Optimization**

   Processing records in bulk reduces the number of database operations and HTTP requests, which improves performance. 

3. **Avoiding Recursive Triggers**

   Bulkified code reduces the likelihood of hitting recursive triggers.
   
5. **Scalability**

   Bulkification ensures that code can handle large volumes of data without performance degradation. For example, if you need to process 10,000 records, bulkified code can handle this efficiently by processing records in batches rather than one at a time.

6. **Maintaining Data Integrity**

   Bulk operations help maintain data integrity by ensuring that related records are processed together. For instance, when updating a set of records, bulk operations ensure that related updates are performed consistently, reducing the risk of partial updates or data inconsistencies.


### Key Practices for Bulkification

1. **Use Collections**

   Always use collections (such as Lists, Maps, and Sets) to handle multiple records. This allows you to perform operations in bulk.

   ```apex
   // Bulk Insert Example
   List<Account> accountsToInsert = new List<Account>();
   for (Integer i = 0; i < 200; i++) {
       accountsToInsert.add(new Account(Name = 'Account ' + i));
   }
   insert accountsToInsert;
   ```

2. **Limit SOQL Queries**

   Avoid performing SOQL queries inside loops. Instead, query all needed records in a single query and use a Map to access them by ID.

   ```apex
   // Bulk Query Example
   List<Account> accounts = [SELECT Id, Name FROM Account WHERE CreatedDate = LAST_N_DAYS:30];
   Map<Id, Account> accountMap = new Map<Id, Account>();
   for (Account acc : accounts) {
       accountMap.put(acc.Id, acc);
   }
   
   // Access accounts by ID from the map
   ```

3. **Bulkify Triggers**

   Ensure that triggers are designed to handle multiple records at once. Use collections to process records and avoid SOQL or DML operations inside loops.

   ```apex
   trigger AccountTrigger on Account (before insert, before update) {
       Set<Id> accountIds = new Set<Id>();
       for (Account acc : Trigger.new) {
           accountIds.add(acc.Id);
       }

       // Perform bulk operations
       List<Contact> contacts = [SELECT Id, AccountId FROM Contact WHERE AccountId IN :accountIds];
       // Process contacts
   }
   ```

4. **Use Batch Apex for Large Data Volumes**

   When dealing with very large datasets, use Batch Apex to process records in manageable chunks.

   ```apex
   global class MyBatchClass implements Database.Batchable<sObject> {
       global Database.QueryLocator start(Database.BatchableContext BC) {
           return Database.getQueryLocator('SELECT Id FROM Account');
       }

       global void execute(Database.BatchableContext BC, List<sObject> scope) {
           // Bulk processing logic
           List<Account> accountsToUpdate = new List<Account>();
           for (Account acc : (List<Account>)scope) {
               acc.Name = 'Updated Name';
               accountsToUpdate.add(acc);
           }
           update accountsToUpdate;
       }

       global void finish(Database.BatchableContext BC) {
           // Post-processing logic
       }
   }
   ```

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Database operation and syntax
#### Answer : 


### 1. **SOQL (Salesforce Object Query Language)**

SOQL is used to query Salesforce data. It’s similar to SQL (Structured Query Language) but is tailored for the Salesforce data model.

**Basic Syntax**

```sql
SELECT field1, field2 FROM ObjectName WHERE condition
```

**Examples**

1. **Query Records**

   ```apex
   // Query to select all Account records with a specific name
   List<Account> accounts = [SELECT Id, Name FROM Account WHERE Name = 'Acme Corp'];
   ```

2. **Query with Multiple Conditions**

   ```apex
   // Query to select contacts with a specific last name and account
   List<Contact> contacts = [SELECT Id, FirstName, LastName FROM Contact WHERE LastName = 'Smith' AND Account.Name = 'Acme Corp'];
   ```

3. **Query with Relationships**

   ```apex
   // Query to select accounts and related contacts
   List<Account> accountsWithContacts = [SELECT Id, Name, (SELECT Id, FirstName, LastName FROM Contacts) FROM Account];
   ```

### 2. **SOSL (Salesforce Object Search Language)**

SOSL is used for text searches across multiple objects and fields.

**Basic Syntax**

```sql
FIND {searchQuery} IN {RETURNING object1(field1, field2), object2(field1, field2)}
```

**Examples**

1. **Search Across Objects**

   ```apex
   // Search for 'Acme' across Account and Contact objects
   List<List<SObject>> searchResults = [FIND 'Acme' IN ALL FIELDS RETURNING Account(Id, Name), Contact(Id, FirstName, LastName)];
   ```

2. **Search with Specific Fields**

   ```apex
   // Search for 'Smith' in the LastName field of Contact
   List<Contact> contacts = [FIND 'Smith' IN NAME RETURNING Contact(Id, FirstName, LastName)];
   ```

### 3. **DML Operations**

DML operations are used to manipulate data, including inserting, updating, deleting, and undeleting records.

**Syntax**

```apex
// Insert
insert newObject;

// Update
update existingObject;

// Delete
delete existingObject;

// Undelete
undelete existingObject;
```

**Examples**

1. **Insert Records**

   ```apex
   // Create a new account and insert it
   Account newAccount = new Account(Name = 'Acme Corp');
   insert newAccount;
   ```

2. **Update Records**

   ```apex
   // Update an existing account
   Account existingAccount = [SELECT Id, Name FROM Account WHERE Name = 'Acme Corp' LIMIT 1];
   existingAccount.Name = 'Acme Corporation';
   update existingAccount;
   ```

3. **Delete Records**

   ```apex
   // Delete an existing account
   Account accountToDelete = [SELECT Id FROM Account WHERE Name = 'Acme Corporation' LIMIT 1];
   delete accountToDelete;
   ```

4. **Undelete Records**

   ```apex
   // Undelete a record from the Recycle Bin
   Account accountToUndelete = [SELECT Id FROM Account WHERE Name = 'Acme Corporation' LIMIT 1 ALL ROWS];
   undelete accountToUndelete;
   ```

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : What are public component in LWC
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Types of decorators in LWC
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Difference between, trigger.old and Trigger.oldmap
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Not using @future annotation in webservices callout, what will happen
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How can you implement recursive trigger in salesforce
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Composite request
#### Answer : 
A Composite Request enables you to bundle multiple REST API requests into a single HTTP call. This is helpful for operations that involve creating, updating, or querying multiple records simultaneously. It helps to:

- **Reduce API Call Counts**: Minimize the number of API calls by sending a single composite request instead of multiple individual requests.
- **Improve Efficiency**: Decrease network latency and improve performance by batching operations.
- **Handle Complex Transactions**: Perform complex transactions and maintain data consistency by processing multiple related operations together.

#### Why Composite Resources
Lets understand the advantage of composite API.

- Multiple REST API calls for single call
- Processing speed can be made faster by collating the subrequests.
- Improves the performance of the application
- No additional coding required at Salesforce.
- Single call toward API limits.
- Synchronous responses.
- Multiple ways in composite resources work.
- Upsert upto five levels deep relationships.
- Flexible on upserting related or non related records.
- Can do a GET subrequest and the result can be input to next POST subrequest.
- Can handle more complicated and related objects and data.


Sample Request and URL.

URL : `/services/data/vXX.X/composite`

**Request Body sample.**

```apex
{
"compositeRequest" : [
  {
  "method" : "POST",
  "url" : "/services/data/v52.0/sobjects/Account",
  "referenceId" : "refAccount",
  "body" : { "Name" : "APEX HOURS" }
  },
  {
  "method" : "POST",
  "url" : "/services/data/v52.0/sobjects/Contact",
  "referenceId" : "refContact",
  "body" : { 
    "LastName" : "AMIT CHAUDHARY",
    "AccountId" : "@{refAccount.id}"
    }
  }]
}
```

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Component event and application event difference
#### Answer : 
### Component Events in LWC

**Component Events** in LWC are used for communication between components that have a parent-child relationship. These events are specifically designed to facilitate interaction within a component hierarchy.

#### Example

**Child Component (childComponent.html)**
```html
<template>
    <lightning-button label="Click Me" onclick={handleClick}></lightning-button>
</template>
```

**Child Component (childComponent.js)**
```js
import { LightningElement } from 'lwc';

export default class ChildComponent extends LightningElement {
    handleClick() {
        // Create and dispatch a custom event
        const event = new CustomEvent('myevent', {
            detail: { message: 'Hello from child' }
        });
        this.dispatchEvent(event);
    }
}
```

**Parent Component (parentComponent.html)**
```html
<template>
    <c-child-component onmyevent={handleChildEvent}></c-child-component>
</template>
```

**Parent Component (parentComponent.js)**
```js
import { LightningElement } from 'lwc';

export default class ParentComponent extends LightningElement {
    handleChildEvent(event) {
        // Handle the event from the child component
        const message = event.detail.message;
        console.log(message); // Outputs: Hello from child
    }
}
```

### Application Events in LWC

**Application Events** in LWC are not a part of the framework like in Aura components. LWC uses a different approach for global communication. Instead of application events, LWC relies on other methods such as:

1. **Pub/Sub (Publish/Subscribe) Model**: For cross-component communication that is not tied to a parent-child relationship. This pattern is typically managed using a custom event bus or a pub/sub library.

2. **Lightning Message Service (LMS)**: For inter-component communication within the Lightning Experience and Salesforce mobile app. LMS enables message passing across different components, even if they are not in a direct parent-child relationship.

https://github.com/therishabh/salesforce-lwc?tab=readme-ov-file#component-communication

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : What is LDS(Lightning Data Services) in lwc
#### Answer : 

https://medium.com/@saurabh.samirs/lightning-data-services-lds-in-lwc-67e9a50039d5

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

## Question : SOQL 101 Exception
#### Answer : 
In Salesforce we got the System.limitException: Too many SOQL Queries 101 very often.<br/><br/>

In Salesforce we can encounter the Salesforce Governor Limits **system limit exception too many soql queries 101** very often. This means we can only have up to 100 SOQL in a single context. This is a **hard** limit, which means you can’t increase it by contacting Salesforce support.<br/><br/>

The following error appears when we exceed the Governors Limit.<br/>
```
System.LimitException: Too many SOQL queries: 101 error
```
<br/>
As per the governor limit, the Total number of SOQL queries issued is 100 in Synchronous and 200 in Asynchronous context.<br/>

**Let see the all other reason for SOQL 101 Error.** <br/>

- Soql inside the for Loop
- A Trigger is not bulkified.
- Trigger is recursive
- Multiple processes are executing at the same time and updating the same record in the same transection.<br/><br/>


**Let see how to resolve this System.LimitException: Too many SOQL queries: 101 error.** <br/>

- Avoid SOQL queries inside For Loop
- Bulkify Apex Trigger and Recursion Handling
- Move some business logic into @future
- Minimize the No.of SOQLs by merging the queries

-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Nested aura component can we have, which event will execute first
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Deployment tool.. CI/CD process.. how to setup
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : explain one LWC component created by you.
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How will you get the data from Apex to LWC
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : how many ways we can query the data
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : What is Wire method
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Concept of promises in LWC ?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : how to establish communication between components
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Integration- breif what you have done.
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : diff between userflow and web server flow ( connected App authorization)?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : serve side - how the authentication is happen?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Platform event?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Managed Package- exp
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Aura - share the method with another Aura comp?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : styling hooks in LWC?
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : have you worked in service console.
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How did you do deployment
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Involved in any deployment
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Can we use multiple decorators for one property
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : what is the need of LWC, when we are already having Aura
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question :  How will you overcome the governor limit
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : How to call from one batch class into another batch class
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Why apex callout is always asyc
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : SECURITY_ENFORCE use in SOQL
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Security question on Triggers
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Can we pass one batch data to another batch process
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Types of Async classes
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : About Iterable class in Batchable
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : PMD violations
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Devops process
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Imperative apex
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Difference between aura and LWC component
#### Answer : 
-----------------------------------------------------------------------------------------------------------------------------------------------

## Question : Types of Events in AURA
#### Answer :

-----------------------------------------------------------------------------------------------------------------------------------------------

