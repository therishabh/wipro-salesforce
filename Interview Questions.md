
# Q. What is the difference between Flow and Trigger?

#### 🔹 1. Basic Definition

####  Flow

Flow is a **declarative (no-code / low-code)** automation tool in Salesforce used to automate business processes.

####  Trigger

Trigger is a **programmatic automation (Apex code)** that executes **before or after DML operations** on records.

---

#### 🔹 2. Key Differences Table

| Feature         | Flow                            | Trigger                                |
| --------------- | ------------------------------- | -------------------------------------- |
| Type            | Declarative (No Code)           | Programmatic (Apex Code)               |
| Execution       | Runs using Flow Builder         | Runs using Apex runtime                |
| Use case        | Simple to medium business logic | Complex logic, bulk processing         |
| Before Save     | Yes (Fast Field Update Flow)    | Yes (Before Trigger)                   |
| After Save      | Yes                             | Yes                                    |
| Performance     | Slower compared to trigger      | Faster and more optimized              |
| Debugging       | Limited debugging tools         | Advanced debugging (Logs, Dev Console) |
| Version Control | Difficult                       | Easy with Git / CI-CD                  |
| Bulkification   | Automatic but limited control   | Fully controlled by developer          |
| Error Handling  | Limited                         | Full control with try-catch            |

---

#### 🔹 3. Execution Order Difference

* **Before Save Flow** runs **before before-trigger**
* **After Save Flow** runs **after after-trigger**

👉 So internally execution order is like:

```
Before Flow → Before Trigger → DML Save → After Trigger → After Flow
```

---

#### 🔹 4. Example Comparison

####  Example 1: Update a field when record is created

* Using Flow → Simple
* Using Trigger → Overkill

####  Example 2: Complex validation across multiple objects + callout

* Flow → Difficult / messy
* Trigger → Best approach

---

# Q. What approach would you follow Flow or Trigger and Why?

👉 **Answer: It depends on the business requirement complexity**

You should explain decision-making approach like a senior developer.

---

#### 🔹 Decision Rule (Interview Golden Answer)

I always follow this hierarchy:

#### ✅ Use **Flow when**

* Logic is simple
* Field update / email / task creation
* No complex loops
* No heavy data processing
* Admin should maintain it

#### ✅ Use **Trigger when**

* Complex business logic
* Multiple object relationship logic
* Bulk data handling
* Need full control on execution
* Performance critical
* Integration or callout involved

---

#### 🔷 Real-Time Scenario Answer (Very Important for Interview)

#### 🎯 Scenario: Insurance Claim Processing System

Let’s say we have a custom object:

👉 `Claim__c`

#### Requirement:

When a Claim is created:

1. Validate related Policy and Customer
2. Calculate claim eligibility based on multiple conditions
3. Update related Account risk score
4. Create payment record
5. Call external API for fraud check

---

####  Approach using Flow?

Flow can handle:

* Field updates
* Record creation

But problem:

* Complex conditions
* API callout
* Bulk processing
* Performance

👉 Flow will become **very complex and slow**

---

####  Approach using Trigger (Best Practice)

We use:

* **Trigger → Handler Class**
* **Service Class for business logic**
* **Queueable for callout**

##### Flow of execution:

1. Trigger fires on Claim__c
2. Handler processes records in bulk
3. Service class:

   * Validate policy
   * Calculate eligibility
   * Update Account
4. Queueable Job:

   * External Fraud API call

👉 This is **scalable + bulk-safe + clean architecture**

---

#### 🔷 Final Interview Answer (What YOU should say)


#### 🗣️ Answer Script

> Flow and Trigger both are automation tools in Salesforce.
> Flow is declarative and best suited for simple to medium business logic like field updates, email alerts, and record creation.
> Trigger is Apex-based and used for complex, bulk-safe, and performance-critical logic.

> In my approach, I always prefer **Flow for simple logic** because it is easy to maintain by admins.
> But for **complex scenarios like multi-object operations, heavy data processing, integrations, or performance-critical logic**, I prefer **Apex Trigger with proper handler framework**.

> For example, in one of my projects, we had a Claim processing system where we needed to validate policies, calculate eligibility, update related accounts, and call external fraud APIs.
> In that case, Flow was not efficient, so we implemented a Trigger + Service Layer + Queueable architecture which was scalable and bulk-safe.

---

# Q What are the limitations in Flows?

#### 1. Clear Explanation (Simple & Professional)

Salesforce Flow is a powerful declarative automation tool, but it has certain limitations compared to Apex. These limitations mainly relate to **performance, complex logic handling, governor limits, debugging, and reusability**.

For simple to medium business logic, Flow works great. But for **complex processing, heavy data operations, integrations, or scalable architecture**, Apex is more suitable.

---

#### 2. Detailed Technical Explanation

Key limitations of Flow:

#####  1. Governor Limits (Same as Apex)

* SOQL queries limit
* DML operations limit
* CPU time limit (10 seconds sync)
* Heap size

Flow internally executes using Apex engine, so limits apply.

---

#####  2. Performance Issues in Large Data Volume

* Flows process records **one-by-one (row-by-row)** in many cases
* No proper bulkification like Apex (unless carefully designed)
* Can cause **CPU time limit exceeded**

---

#####  3. Limited Error Handling

* No try-catch like Apex
* Fault paths are basic
* Hard to implement retry mechanism

---

#####  4. Debugging is Limited

* Debug logs are not very clear
* Hard to trace deep logic
* No breakpoints like code debugging

---

#####  5. Complex Logic is Hard to Implement

Examples:

* Nested loops
* Complex data transformation
* Dynamic SOQL
* Recursive logic

These are easier in Apex.

---

#####  6. Reusability is Limited

* Subflows exist but not as flexible as Apex classes
* No inheritance or interfaces

---

#####  7. Deployment Challenges

* Flows need activation
* Versioning issues
* Dependency issues during deployment

---

#####  8. Integration Limitations

* Callouts possible via HTTP Callout action
* But:

  * No advanced authentication handling like Named Credential with OAuth refresh easily
  * Complex request/response parsing is harder

---

#### 3. Real-Time Project Use Case

#### 🏦 Banking Use Case

In a banking loan processing system:

* A Flow is used to:

  * Create Loan Application
  * Assign to Relationship Manager
  * Send email

But for:

* Credit score calculation
* Risk engine integration
* Bulk loan updates (10,000+ records)

➡️ Flow fails due to performance + complexity
➡️ Apex Batch + Queueable + Integration used instead

---

#### 4. Code Example (When Flow is Not Enough → Apex Replacement)

Example: Bulk update records

```apex
public class LoanProcessorBatch implements Database.Batchable<SObject> {

    public Database.QueryLocator start(Database.BatchableContext bc) {
        return Database.getQueryLocator('SELECT Id, Status__c FROM Loan__c WHERE Status__c = \'Pending\'');
    }

    public void execute(Database.BatchableContext bc, List<Loan__c> scope) {
        for(Loan__c loan : scope) {
            loan.Status__c = 'Processed';
        }
        update scope;
    }

    public void finish(Database.BatchableContext bc) {}
}
```

👉 This is difficult and inefficient in Flow for large data.

---

#### 5. Best Practices & Governor Limit Considerations

✔ Use Flow for:

* Simple CRUD automation
* Approval routing
* Screen-based UI

✔ Use Apex when:

* Data > 200 records
* Complex logic
* Integration heavy
* Need transaction control

✔ Avoid:

* SOQL inside loops in Flow
* Too many elements in single Flow

---

#### 6. Common Mistakes to Avoid

- ❌ Using Flow for heavy batch processing
- ❌ Creating multiple DML elements in loop
- ❌ Not handling fault paths
- ❌ Not testing with bulk data
- ❌ Overusing Screen Flows for backend logic

---

#### 7. Interview Talking Points

You can say:

* Flow is great for **declarative automation**
* But has limitations in:

  * Bulk processing
  * Complex logic
  * Performance
  * Debugging
* For enterprise systems, we use **Flow + Apex hybrid approach**
* Always evaluate:
  👉 Volume
  👉 Complexity
  👉 Integration
  👉 Maintainability

---

#### 8. Follow-up Questions + Short Answers

**Q: When to choose Flow vs Apex?**
- 👉 Flow for simple automation, Apex for complex/bulk/integration

**Q: Can Flow handle bulk records?**
- 👉 Yes, but not as efficiently as Apex

**Q: How to improve Flow performance?**
- 👉 Reduce elements, avoid loops, use Get Records wisely

---


# Q. How to make callout from LWC on button click?

#### 1. Clear Explanation

In Salesforce, **LWC cannot directly make external API callouts** due to security restrictions.

Instead, the correct approach is:

👉 LWC Button Click
➡️ Calls Apex method
➡️ Apex makes HTTP callout
➡️ Returns response to LWC

---

#### 2. Detailed Technical Explanation

Steps involved:

1. Create Apex class with `@AuraEnabled`
2. Use `HttpRequest` + `Http` for callout
3. Use Named Credential for endpoint
4. Call Apex from LWC using `import`

---

#### 3. Real-Time Use Case

#### 🛒 E-commerce Example

User clicks **"Check Delivery Availability"**

Flow:

* User enters pincode
* Click button
* LWC calls Apex
* Apex calls external courier API
* Response shown on UI

---

#### 4. Code Example

#### 🔹 Apex Class

```apex
public with sharing class DeliveryService {

    @AuraEnabled
    public static String checkDelivery(String pincode) {

        Http http = new Http();
        HttpRequest req = new HttpRequest();

        req.setEndpoint('callout:Delivery_API/pincode/' + pincode);
        req.setMethod('GET');

        HttpResponse res = http.send(req);

        if(res.getStatusCode() == 200){
            return res.getBody();
        } else {
            throw new AuraHandledException('Delivery service failed');
        }
    }
}
```

---

#### 🔹 LWC JS

```javascript
import { LightningElement, track } from 'lwc';
import checkDelivery from '@salesforce/apex/DeliveryService.checkDelivery';

export default class DeliveryChecker extends LightningElement {
    @track result;
    pincode = '';

    handleChange(event) {
        this.pincode = event.target.value;
    }

    handleClick() {
        checkDelivery({ pincode: this.pincode })
            .then(response => {
                this.result = response;
            })
            .catch(error => {
                console.error(error);
            });
    }
}
```

---

#### 🔹 LWC HTML

```html
<template>
    <lightning-input label="Enter Pincode" onchange={handleChange}></lightning-input>

    <lightning-button label="Check Delivery" onclick={handleClick}></lightning-button>

    <p>{result}</p>
</template>
```

---

#### 5. Best Practices & Governor Limits

- ✔ Use Named Credentials (avoid hardcoding endpoint)
- ✔ Use `@AuraEnabled(cacheable=false)` for callouts
- ✔ Use try-catch in Apex
- ✔ Handle timeout

Limits:

* Max 100 callouts per transaction
* 10 sec timeout (sync)

---

#### 6. Common Mistakes to Avoid

- ❌ Direct callout from LWC (not allowed)
- ❌ Hardcoding endpoints
- ❌ Not handling errors
- ❌ Not using Named Credentials
- ❌ Not handling JSON parsing properly

---

#### 7. Interview Talking Points

Say:

* LWC cannot do callout directly due to security (CSP)
* We use Apex as middleware layer
* Always use Named Credentials
* Handle response & errors properly
* For async use Queueable or Future

---

#### 8. Follow-up Questions + Short Answers

**Q: Can LWC call external API directly?**
- 👉 No

**Q: How to secure API endpoint?**
- 👉 Named Credential + Auth Provider

**Q: How to make async callout?**
- 👉 Queueable / Future

**Q: How to handle large response?**
- 👉 Deserialize JSON into Apex wrapper class

---

# Q. What design patterns do you follow in Apex?

#### 1. Clear Explanation (Simple & Professional)

In Apex, we follow several **design patterns** to make code **scalable, maintainable, reusable, and testable**. The most commonly used patterns in Salesforce are:

* Trigger Framework (One Trigger per Object)
* Handler Pattern
* Service Layer Pattern
* Selector Pattern
* Domain Layer Pattern
* Factory Pattern
* Singleton Pattern
* Strategy Pattern

These patterns help us build **enterprise-grade applications** and are highly expected at Senior/Lead level.

---

#### 2. Detailed Technical Explanation

###  1. Trigger Framework Pattern

* Only **one trigger per object**
* Logic moved to handler class
* Supports bulkification

---

###  2. Handler Pattern

* Each trigger event handled in separate methods
* Keeps trigger thin

---

###  3. Service Layer Pattern

* Contains **business logic**
* Called from triggers, LWC, REST, batch

---

###  4. Selector Pattern

* Centralized SOQL queries
* Improves reusability and performance

---

###  5. Domain Layer Pattern

* Represents object behavior
* Contains logic related to specific SObject

---

###  6. Factory Pattern

* Used to create objects dynamically
* Useful in integrations and dynamic processing

---

###  7. Singleton Pattern

* Ensures only one instance of class
* Used for caching, config management

---

###  8. Strategy Pattern

* Select algorithm dynamically at runtime
* Used in pricing engines, validation rules, payment logic

---

#### 3. Real-Time Project Use Case

### 🏥 Healthcare Use Case

In a healthcare system:

* Trigger fires on Patient__c
* Handler routes logic
* Service layer processes insurance eligibility
* Selector fetches patient history
* Strategy pattern used for multiple insurance providers

This creates a **clean layered architecture**.

---

#### 4. Code Example

### 🔹 Trigger + Handler + Service Pattern

```apex
trigger PatientTrigger on Patient__c (after insert, after update) {
    PatientTriggerHandler handler = new PatientTriggerHandler();

    if(Trigger.isAfter && Trigger.isInsert) {
        handler.handleAfterInsert(Trigger.new);
    }
}
```

### 🔹 Handler Class

```apex
public class PatientTriggerHandler {

    public void handleAfterInsert(List<Patient__c> patients) {
        PatientService.processPatients(patients);
    }
}
```

### 🔹 Service Class

```apex
public class PatientService {

    public static void processPatients(List<Patient__c> patients) {
        for(Patient__c p : patients){
            p.Status__c = 'New';
        }
        update patients;
    }
}
```

---

#### 5. Best Practices & Governor Limits

- ✔ Always bulkify code
- ✔ Avoid SOQL inside loops
- ✔ Use selector for queries
- ✔ Use service layer for business logic
- ✔ Use Unit Tests for each layer

---

#### 6. Common Mistakes to Avoid

- ❌ Multiple triggers on same object
- ❌ Business logic inside trigger
- ❌ SOQL/DML in loops
- ❌ Not using handler classes
- ❌ No separation of concerns

---

#### 7. Interview Talking Points

You can say:

* I follow **layered architecture in Apex**
* Use **Trigger → Handler → Service → Selector**
* This improves:
  * Scalability
  * Maintainability
  * Testability
* I also use **Strategy pattern for dynamic logic**
* And **Singleton for caching**

---

#### 8. Follow-up Questions + Short Answers

**Q: Why one trigger per object?**
- 👉 Avoid recursion, better control

**Q: What is Selector pattern?**
- 👉 Central SOQL management

**Q: Where do you write business logic?**
- 👉 Service Layer

**Q: How to handle recursion?**
- 👉 Static variables in handler class

---

# Q. How to do Error Handling in Flow?

#### 1. Clear Explanation

Error handling in Flow is done using:

* **Fault Paths**
* **Custom Error Screens**
* **Platform Event / Logging**
* **Apex Exception Handling (if Apex used)**

Flow does not support try-catch like Apex, so we use **Fault connectors** to capture and handle errors.

---

#### 2. Detailed Technical Explanation

###  1. Fault Path

* Every Flow element has a **Fault connector**
* Used to capture errors

---

###  2. Custom Error Message

* Use Screen element to show friendly message

---

###  3. Logging Mechanism

* Create custom object like Error_Log__c
* Store error message

---

###  4. Apex Exception Handling

If Flow calls Apex:

```apex
try {
   // logic
} catch(Exception e){
   throw new AuraHandledException(e.getMessage());
}
```

Flow can catch this via Fault Path

---

###  5. Email Notification

Send error email to admin using action

---

#### 3. Real-Time Use Case

### 🏦 Banking Scenario

In Loan Flow:

* Create Loan Record
* Call credit score API
* If API fails → show message + log error + notify admin

---

#### 4. Flow Implementation Example (Concept)

Flow Steps:

1. Create Records (Loan)
2. Call Apex (Credit Score API)
3. If error → Fault Path

   * Create Error_Log__c record
   * Show Screen: "Service temporarily unavailable"
   * Send Email Alert

---

#### 5. Best Practices & Governor Limits

✔ Always use Fault path on DML & Apex actions
✔ Log errors in custom object
✔ Show user-friendly message (not technical error)
✔ Avoid exposing internal exception message

---

#### 6. Common Mistakes to Avoid

- ❌ Ignoring Fault connectors
- ❌ Showing system error directly to user
- ❌ No logging mechanism
- ❌ No alert to admin
- ❌ Overusing screen flows for backend logic

---

#### 7. Interview Talking Points

Say:

* Flow doesn't support try-catch
* We use **Fault paths for error handling**
* Implement:

  * Logging
  * Notifications
  * User-friendly messaging
* For complex error handling → use Apex

---

#### 8. Follow-up Questions + Short Answers

**Q: Can we retry failed Flow automatically?**
- 👉 Not directly, need Apex or scheduled flow

**Q: How to log Flow errors?**
- 👉 Custom object (Error_Log__c)

**Q: Can Flow catch Apex exception?**
- 👉 Yes via Fault path

**Q: How to notify admin?**
- 👉 Email alert / Platform Event

---
---

# Q. How to handle timeout issues with an external system?

#### 1. Clear Explanation (Simple & Professional)

Timeout issues occur when Salesforce sends a request to an external system and **doesn’t receive a response within the allowed time**.

To handle this, we should **avoid synchronous dependency**, implement **asynchronous callouts**, add **retry mechanisms**, use **timeouts properly**, and ensure **graceful fallback and logging**.

---

#### 2. Detailed Technical Explanation

### Types of Timeouts in Salesforce Callouts

* Default timeout: **10 seconds**
* Max allowed timeout: **120 seconds**

```apex
request.setTimeout(120000); // 120 seconds
```

---

### Approaches to Handle Timeout

### ✅ 1. Use Asynchronous Callouts

Use:

* Future
* Queueable
* Batch Apex

So UI/user is not blocked.

---

### ✅ 2. Retry Mechanism

* If callout fails → store request
* Retry using Scheduled/Queueable job

---

### ✅ 3. Circuit Breaker Pattern

* If system is down → stop calling temporarily
* Prevents cascading failures

---

### ✅ 4. Fallback Mechanism

* Show cached data
* Or show “Service unavailable, try later”

---

### ✅ 5. Named Credential + Proper Timeout

* Avoid hardcoding endpoint
* Manage auth and endpoint centrally

---

### ✅ 6. Use Platform Events for Decoupling

* Publish event
* Integration middleware processes later

---

#### 3. Real-Time Use Case

### 🏦 Banking Payment System

User clicks **"Make Payment"**

Problem:
External payment gateway is slow (timeout)

Solution:

* LWC calls Apex
* Apex enqueues **Queueable job**
* Payment request stored in `Payment_Request__c`
* Queueable retries if timeout
* UI shows “Payment in progress”

---

#### 4. Code Example

### 🔹 Queueable with Timeout + Retry

```apex id="p6z9he"
public class PaymentQueueable implements Queueable, Database.AllowsCallouts {

    public void execute(QueueableContext context) {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('callout:PaymentAPI');
        req.setMethod('POST');
        req.setTimeout(120000);

        Http http = new Http();

        try {
            HttpResponse res = http.send(req);

            if(res.getStatusCode() != 200){
                throw new CalloutException('Failed Payment');
            }

        } catch(Exception e){
            // retry logic (re-enqueue)
            System.enqueueJob(new PaymentQueueable());
        }
    }
}
```

---

#### 5. Best Practices & Governor Limits

- ✔ Use async callouts
- ✔ Avoid long-running synchronous calls
- ✔ Max 100 callouts per transaction
- ✔ Use timeout setting wisely
- ✔ Store failed requests for retry

---

#### 6. Common Mistakes to Avoid

- ❌ Doing callout in trigger synchronously
- ❌ Not handling timeout exception
- ❌ No retry mechanism
- ❌ Blocking user UI
- ❌ Hardcoding endpoints

---

#### 7. Interview Talking Points

You should say:

* Timeout is common in integrations
* I avoid synchronous dependency
* I use:

  * Queueable callouts
  * Retry mechanism
  * Logging
  * Named Credentials
* Also design **resilient architecture**

---

#### 8. Follow-up Questions + Short Answers

**Q: What is max timeout in Apex?**
- 👉 120 seconds

**Q: How to retry failed callout?**
- 👉 Queueable / Scheduled retry

**Q: How to avoid blocking UI?**
- 👉 Async processing

**Q: What is circuit breaker?**
- 👉 Stop hitting failing system temporarily

---

---

# Q. What approach will you suggest to populate list of Accounts on LWC page?

#### 1. Clear Explanation

To populate Accounts in LWC, we can use **three main approaches**:

1. **@wire with Apex (cacheable=true)** – best for read-only data
2. **Imperative Apex call** – when filtering/search required
3. **Lightning Data Service (LDS)** – for standard record access

For enterprise apps, best practice is:

👉 **Apex + @wire + cacheable + pagination**

---

#### 2. Detailed Technical Explanation

### Option 1: @wire (Reactive & Cached)

* Uses `@AuraEnabled(cacheable=true)`
* Automatically refreshes when params change

---

### Option 2: Imperative Apex

* Called on button click/search/filter
* More control

---

### Option 3: Lightning Data Service

* Use `getListUi` or `getRecord`
* No Apex required
* Limited flexibility

---

#### 3. Real-Time Use Case

### 🛒 E-commerce CRM

Sales team wants:

* List of Accounts
* Filter by City, Revenue
* Pagination
* Search

Solution:

* LWC with Apex
* Server-side filtering
* Pagination using OFFSET or keyset

---

#### 4. Code Example

---

### 🔹 Apex Class

```apex id="3pslxt"
public with sharing class AccountController {

    @AuraEnabled(cacheable=true)
    public static List<Account> getAccounts() {
        return [SELECT Id, Name, Industry FROM Account LIMIT 50];
    }
}
```

---

### 🔹 LWC JS (Using @wire)

```javascript id="pd4u0c"
import { LightningElement, wire } from 'lwc';
import getAccounts from '@salesforce/apex/AccountController.getAccounts';

export default class AccountList extends LightningElement {
    accounts;
    error;

    @wire(getAccounts)
    wiredAccounts({ error, data }) {
        if (data) {
            this.accounts = data;
        } else if (error) {
            this.error = error;
        }
    }
}
```

---

### 🔹 LWC HTML

```html id="o8qf3i"
<template>
    <template if:true={accounts}>
        <template for:each={accounts} for:item="acc">
            <p key={acc.Id}>{acc.Name} - {acc.Industry}</p>
        </template>
    </template>
</template>
```

---

#### 5. Best Practices & Governor Limits

- ✔ Use `cacheable=true` for read operations
- ✔ Implement pagination for large data
- ✔ Avoid fetching > 200 records at once
- ✔ Use selective SOQL (indexed fields)
- ✔ Avoid SOQL in loop

---

#### 6. Common Mistakes to Avoid

- ❌ Fetching 10,000 records in LWC
- ❌ No pagination
- ❌ Not using cacheable=true
- ❌ Calling Apex repeatedly without need
- ❌ Not handling errors

---

#### 7. Interview Talking Points

You should say:

* I choose approach based on use case:

  * @wire for read-only
  * Imperative for search/filter
  * LDS for standard UI
* For large data:

  * Pagination
  * Lazy loading
* Always optimize SOQL

---

#### 8. Follow-up Questions + Short Answers

**Q: Why use cacheable=true?**
- 👉 Enables client-side caching → better performance

**Q: Difference between @wire and imperative?**
- 👉 @wire reactive, imperative controlled call

**Q: How to handle large data?**
- 👉 Pagination / Lazy loading

**Q: Can we use LDS for list view?**
- 👉 Yes but limited flexibility

---
