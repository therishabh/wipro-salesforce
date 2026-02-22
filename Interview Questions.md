
# Q. What is the difference between Flow and Trigger?

#### 🔹 1. Basic Definition

#### 🔸 Flow

Flow is a **declarative (no-code / low-code)** automation tool in Salesforce used to automate business processes.

#### 🔸 Trigger

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

#### 🔸 Example 1: Update a field when record is created

* Using Flow → Simple
* Using Trigger → Overkill

#### 🔸 Example 2: Complex validation across multiple objects + callout

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

#### 🔸 Approach using Flow?

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

#### 🔸 Approach using Trigger (Best Practice)

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

Great questions 👍 These are very common in **Senior Salesforce Developer / Lead interviews**.

I’ll answer both one by one in your requested structured format.

---

# Q What are the limitations in Flows?

#### 1. Clear Explanation (Simple & Professional)

Salesforce Flow is a powerful declarative automation tool, but it has certain limitations compared to Apex. These limitations mainly relate to **performance, complex logic handling, governor limits, debugging, and reusability**.

For simple to medium business logic, Flow works great. But for **complex processing, heavy data operations, integrations, or scalable architecture**, Apex is more suitable.

---

#### 2. Detailed Technical Explanation

Key limitations of Flow:

##### 🔸 1. Governor Limits (Same as Apex)

* SOQL queries limit
* DML operations limit
* CPU time limit (10 seconds sync)
* Heap size

Flow internally executes using Apex engine, so limits apply.

---

##### 🔸 2. Performance Issues in Large Data Volume

* Flows process records **one-by-one (row-by-row)** in many cases
* No proper bulkification like Apex (unless carefully designed)
* Can cause **CPU time limit exceeded**

---

##### 🔸 3. Limited Error Handling

* No try-catch like Apex
* Fault paths are basic
* Hard to implement retry mechanism

---

##### 🔸 4. Debugging is Limited

* Debug logs are not very clear
* Hard to trace deep logic
* No breakpoints like code debugging

---

##### 🔸 5. Complex Logic is Hard to Implement

Examples:

* Nested loops
* Complex data transformation
* Dynamic SOQL
* Recursive logic

These are easier in Apex.

---

##### 🔸 6. Reusability is Limited

* Subflows exist but not as flexible as Apex classes
* No inheritance or interfaces

---

##### 🔸 7. Deployment Challenges

* Flows need activation
* Versioning issues
* Dependency issues during deployment

---

##### 🔸 8. Integration Limitations

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

❌ Using Flow for heavy batch processing
❌ Creating multiple DML elements in loop
❌ Not handling fault paths
❌ Not testing with bulk data
❌ Overusing Screen Flows for backend logic

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

✔ Use Named Credentials (avoid hardcoding endpoint)
✔ Use `@AuraEnabled(cacheable=false)` for callouts
✔ Use try-catch in Apex
✔ Handle timeout

Limits:

* Max 100 callouts per transaction
* 10 sec timeout (sync)

---

#### 6. Common Mistakes to Avoid

❌ Direct callout from LWC (not allowed)
❌ Hardcoding endpoints
❌ Not handling errors
❌ Not using Named Credentials
❌ Not handling JSON parsing properly

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

