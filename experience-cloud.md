# Q. How do you create an Experience Cloud Site?
## ✅ 1. Concept Explanation (Simple)

Experience Cloud (formerly Community Cloud) allows us to create **external-facing portals** for:

* Customers
* Partners
* Vendors

These sites allow users to **log in and interact with Salesforce data** in a controlled way.

---

## 🛠️ 2. Steps to Create Experience Cloud Site

You can say this step-by-step in interview:

### 🔹 Step 1: Enable Digital Experiences

* Go to **Setup → Digital Experiences → Settings**
* Enable Digital Experiences
* Set domain name (example: `mycompany.force.com`)

### 🔹 Step 2: Create New Site

* Go to **All Sites → New**
* Choose template like:

  * Customer Service
  * Partner Central
  * Build Your Own (LWR or Aura)

### 🔹 Step 3: Configure Site

* Give **Name + URL**
* Click **Builder (Experience Builder)**

### 🔹 Step 4: Design UI

* Use drag & drop components
* Add pages, navigation, branding

### 🔹 Step 5: Configure Data Access

* Create **Profiles / Permission Sets**
* Configure **Sharing Rules**
* Use **Sharing Sets** for external users

### 🔹 Step 6: Add Login & Registration

* Configure Login Page
* Enable self-registration (if required)

### 🔹 Step 7: Publish Site

* Click **Publish**
* Site becomes live

---

## 💼 3. Real-time Project Use Case

You can say this:

> “In my previous project, we created a **Customer Support Portal** using Experience Cloud where users can:
>
> * Raise support tickets (Cases)
> * Track their status
> * View knowledge articles
>   We used **LWC components** to customize the UI and **Sharing Sets** to ensure users only see their own records.”

---

## 🎯 4. Interview Key Points (Say These Lines)

* “Experience Cloud is used for external portals like customer or partner portals”
* “We configure it using Experience Builder”
* “Security is handled using profiles, sharing rules, and sharing sets”
* “We can extend functionality using LWC and Apex”

---

# Q. How do you handle External User Authentication in Experience Cloud?

This is **VERY IMPORTANT interview question 🔥**

---

## ✅ 1. Concept Explanation

External users need to **authenticate securely** before accessing the Experience site.

Salesforce supports multiple authentication methods:

### 🔑 Authentication Options

1. **Username & Password (Standard Login)**
2. **Self Registration**
3. **Social Login (Google, Facebook, LinkedIn)**
4. **Single Sign-On (SSO) using SAML or OAuth**
5. **Multi-Factor Authentication (MFA)**

---

## 🛠️ 2. How to Configure Authentication

### 🔹 Option 1: Standard Login

* Create Contact + User
* Assign Profile
* Enable login via Experience site login page

---

### 🔹 Option 2: Self Registration

Steps:

* Enable **Self Registration** in Experience Builder
* Configure:

  * Account creation
  * Default Profile
  * Role assignment
* Customize using **Apex Handler class**

---

### 🔹 Option 3: SSO (SAML/OAuth)

Steps:

1. Create **Connected App**
2. Configure **Identity Provider**
3. Configure **SAML settings**
4. Map external user to Salesforce user

Used when company has external identity provider like:

* Azure AD
* Okta

---

### 🔹 Option 4: Social Login

* Create **Auth Provider**
* Use Google / Facebook
* Map to Salesforce user

---

## 💼 3. Real-time Use Case

You can say this in interview:

> “In my previous project, we implemented **SSO using Azure AD** for partner users.
> So partners could log in using their corporate credentials without creating separate passwords in Salesforce.
> We configured **SAML-based SSO**, mapped users using email, and added fallback login for internal users.”

Or

> “For customer portal, we used **Self Registration + Email Verification + MFA** for secure access.”

---

## 🔐 4. Security Best Practices (Very Important)

Say these to impress interviewer:

* Always enable **MFA for external users**
* Use **Login IP restrictions**
* Use **reCAPTCHA in self registration**
* Use **Password policies**
* Use **least privilege access**

---

## 🎯 5. Interview Key Points (Speak this confidently)

You can say:

> “External authentication in Experience Cloud can be handled using standard login, self-registration, SSO, or social login.
> In enterprise projects, we generally use **SSO with SAML or OAuth** for better security and user convenience.
> We also implement **MFA and sharing rules** to ensure secure data access.”

---

#### 🚀 Final Tip for You (Very Important)

Since you have **5 years experience**, interviewer may ask:

👉 “Which authentication method do you prefer and why?”

You answer:

> “For enterprise-level projects, I prefer **SSO with SAML/OAuth**, because it provides centralized identity management, better security, and seamless user experience.”

---

# Q. How do you control sharing for community users?

## ✅ 1. Concept Explanation (Simple)

In Experience Cloud, **external (community) users** should only see **their own data or related records**, so we need **special sharing mechanisms**.

Salesforce provides **4 main ways** to control data access for external users:

---

## 🔐 2. Ways to Control Sharing

### 🔹 1. Organization-Wide Defaults (OWD)

* First level of security
* Set object access as:

  * Private
  * Public Read Only

👉 For community users, we usually keep **OWD = Private**

---

### 🔹 2. Sharing Sets (Most Common for Customers)

👉 Used when users should see records related to their **Account or Contact**

Example:

* Contact → AccountId
* Case → AccountId

We map:

```
User.Contact.AccountId = Case.AccountId
```

➡️ So user sees only their account’s records

---

### 🔹 3. Share Groups

Used when:

* External users need to access **internal user owned records**

Example:

* Customer should see cases created by support team

---

### 🔹 4. Apex Managed Sharing

Used for **complex logic-based sharing**

Example:

* Share records based on custom logic
* Dynamic conditions

---

### 🔹 5. Role Hierarchy (Limited for external users)

* Only used in **Partner Community**
* Not for high volume customer users

---

## 💼 3. Real-time Project Use Case

You can say this confidently:

> “In my previous project, we had a **Customer Support Portal** where users could raise and track their support cases.
> We used **Sharing Sets** to ensure customers only see cases related to their own account.
> Additionally, we used **Share Groups** so that customers could also view cases created by internal support agents on their behalf.”

---

## 🔐 4. Best Practices

* Always keep **OWD = Private**
* Use **Sharing Sets for customer users**
* Avoid role hierarchy for high volume users
* Use **Apex sharing only when needed**

---

## 🎯 5. Interview Speaking Points

You can say this directly:

> “To control sharing for community users, we use OWD as private and then apply Sharing Sets, Share Groups, and Apex Managed Sharing based on use case.
> For customer community, Sharing Sets are most commonly used to map users to their account records.”

---

# Q. How do you use LWC inside Experience Cloud?

---

## ✅ 1. Concept Explanation

We use **Lightning Web Components (LWC)** in Experience Cloud to build **custom UI and business functionality**.

These LWCs are added inside **Experience Builder pages**.

---

## 🛠️ 2. Steps to Use LWC in Experience Cloud

### 🔹 Step 1: Create LWC

In your component meta XML:

```xml
<targets>
    <target>lightningCommunity__Page</target>
    <target>lightningCommunity__Default</target>
</targets>
```

This makes LWC **available in Experience Builder**

---

### 🔹 Step 2: Make Component Public

Use:

```xml
<isExposed>true</isExposed>
```

---

### 🔹 Step 3: Add to Experience Builder

* Go to **Experience Builder**
* Drag your LWC component onto page

---

### 🔹 Step 4: Connect Data

In LWC you can use:

* **Lightning Data Service (LDS)**
* **@wire Apex**
* **Imperative Apex calls**

---

## 💡 3. Common Use Cases of LWC in Experience Cloud

* Custom **Case Creation Form**
* Show **Booking Details**
* Search functionality
* Payment integration
* Dashboard UI

---

## 💼 4. Real-time Project Example

You can say:

> “In my previous project, we built a **custom LWC component for case creation and tracking** in Experience Cloud.
> We used **LDS for record creation**, and for advanced logic like file upload and validations we used **Apex controller**.
> We deployed the component in Experience Builder and configured it for external users.”

---

## ⚠️ 5. Important Considerations (Very Important)

### 🔹 Security

* Use **with sharing Apex**
* Use **FLS & CRUD checks**

### 🔹 Data Access

* External users only see data allowed by **sharing rules**

### 🔹 Performance

* Use caching
* Avoid heavy queries

---

## 🎯 6. Interview Speaking Points

Say this:

> “To use LWC in Experience Cloud, we expose the component using lightningCommunity targets and then place it in Experience Builder.
> We use LDS or Apex to fetch data, and we ensure proper sharing and security for external users.”

---

#### 🧠 BONUS: Strong Answer Combo (Say this to impress)

If interviewer asks both questions together, combine:

> “In Experience Cloud, we use LWC for building custom UI and business functionality, and data visibility is controlled using sharing sets, share groups, and OWD.
> This ensures that external users only see authorized data in the LWC components.”

---
Great 👍 this is a **very common and important interview question** for Experience Cloud.

Since you have **5 years experience**, interviewer expects you to answer with **clarity + use case + decision making**.

Let’s prepare a **strong, interview-ready answer** 👇

---

# Q. Difference between Customer Community vs Partner Community?

## ✅ 1. Simple Concept Explanation

Both **Customer Community** and **Partner Community** are part of **Experience Cloud**, but they are used for **different types of external users**.

👉 The main difference is **level of access and business purpose**

---

## 🔍 2. Key Differences (Explain clearly in interview)

| Feature            | Customer Community                | Partner Community                    |
| ------------------ | --------------------------------- | ------------------------------------ |
| 🎯 Purpose         | Support customers                 | Manage business partners/resellers   |
| 👤 Users           | End customers                     | Partners, distributors, resellers    |
| 🔐 Access Level    | Limited access                    | Advanced access                      |
| 🏢 Role Hierarchy  | ❌ Not available                   | ✅ Available                          |
| 📊 Data Visibility | Only own records                  | Broader access to shared data        |
| ⚙️ Sharing Model   | Sharing Sets & Share Groups       | Roles + Sharing Rules                |
| 📈 Use Cases       | Case support, FAQ, order tracking | Lead sharing, opportunity management |
| 💰 License Cost    | Lower                             | Higher                               |

---

## 🧠 3. Deep Technical Difference (Important for senior role)

### 🔹 Customer Community

* Uses **High Volume External Users**
* No role hierarchy
* Sharing controlled via:

  * Sharing Sets
  * Share Groups

👉 Suitable for **large number of users (lakhs of customers)**

---

### 🔹 Partner Community

* Uses **Partner Users (Role-based)**
* Supports **Role Hierarchy (up to 3 roles per account)**
* Can use:

  * Sharing Rules
  * Manual sharing
  * Apex sharing

👉 Suitable for **business partners who need more access**

---

## 💼 4. Real-time Use Case (Say this in interview)

### 🟢 Customer Community Example

> “In my previous project, we implemented a **Customer Support Portal** using Customer Community where users could:
>
> * Raise support cases
> * Track their orders
> * View knowledge articles
>   We used **Sharing Sets** so that customers could only see their own records.”

---

### 🔵 Partner Community Example

> “We also built a **Partner Portal** where distributors could:
>
> * View and update Opportunities
> * Manage Leads
> * Collaborate with internal sales team
>   For this we used **Partner Community** with role hierarchy and sharing rules.”

---

## 🎯 5. When to Use Which (Important Decision Question)

👉 If interviewer asks: *“Which one will you choose?”*

You answer like this:

### ✔️ Use Customer Community when:

* Large number of users
* Users only need **their own data**
* Example: customers, patients, users

---

### ✔️ Use Partner Community when:

* Users need **access to shared business data**
* Need **lead/opportunity collaboration**
* Need **role hierarchy**

---

# 🗣️ 6. Interview Speaking Answer (Final Ready Answer)

You can say this directly:

> “Customer Community and Partner Community both are Experience Cloud portals, but they differ in access level and use case.
> Customer Community is used for high-volume external users like customers, where users only access their own records using sharing sets.
> Partner Community is used for business partners where role hierarchy, sharing rules, and collaboration on leads and opportunities are required.
> So, we choose Customer Community for support portals and Partner Community for reseller or distributor management.”

---

# ⭐ 7. Bonus Tip to Impress Interviewer

Add this line:

> “Also Customer Community users are high-volume users without roles, whereas Partner users have roles and can participate in role hierarchy-based sharing.”

🔥 This line shows **senior-level understanding**

---
Perfect 👍 These are **core manager-round questions**.
Since this is a **Senior IC role**, your answers must show:

* Strong data model understanding
* Architectural thinking
* Scalability & governance awareness
* Real project ownership

I’ll give you **manager-level structured answers** that you can confidently speak.

---

# ✅ 1️⃣ Explain Sales Cloud Data Model

### 🔹 High-Level Answer (Start Like This)

> Sales Cloud data model is centered around managing the complete sales lifecycle — from Lead generation to Opportunity closure. The core objects are Lead, Account, Contact, and Opportunity, supported by Products, Pricebooks, Quotes, Activities, and Campaigns.

---

### 🔹 Core Objects & Relationships

#### 1️⃣ Lead (Unqualified Prospect)

* Stores raw prospect data.
* On conversion:

  * Lead → Account
  * Lead → Contact
  * Lead → Opportunity (optional)

Important:

* No direct relationship between Lead & Opportunity before conversion.

---

#### 2️⃣ Account (Company/Individual Customer)

* Parent object in Sales model.
* Has:

  * Contacts (Lookup/Master-detail)
  * Opportunities (Lookup)
  * Cases
  * Activities

Supports:

* Hierarchies (Parent Account)
* Role-based sharing

---

#### 3️⃣ Contact

* Person associated with Account.
* Can be related to:

  * Multiple Opportunities (via Contact Roles)
  * Campaigns
  * Cases

---

#### 4️⃣ Opportunity (Revenue Object)

Most critical object in Sales Cloud.

Key Fields:

* Stage
* Amount
* Close Date
* Probability
* Owner

Relationships:

* Account (Lookup)
* Opportunity Products (Master-detail)
* Quotes
* Activities

---

#### 5️⃣ Products & Revenue Model

Revenue structure:

Opportunity
→ OpportunityLineItem (junction object)
→ Product2
→ PricebookEntry
→ Pricebook2

This enables:

* Multi-currency
* Custom pricing
* Discounting logic

---

#### 6️⃣ Supporting Objects

* Campaign (Marketing)
* Task/Event (Activities)
* Quote (Pre-contract pricing)
* Forecasting objects
* Territory Management objects

---

### 🔹 Important Architectural Concepts

As a Senior Dev, mention:

* Role hierarchy & sharing model
* OWD settings
* Record types & sales processes
* Validation rules
* Approval processes
* Forecasting categories

---

### 🔥 Strong Closing Line

> From an architectural perspective, I always ensure the data model supports scalability, proper indexing, and optimized SOQL queries, especially in Opportunity-heavy orgs where large data volumes are involved.

---

# ✅ 2️⃣ How Have You Customized Opportunity Lifecycle?

This is where you show ownership.

### 🔹 Start Like This:

> I have customized Opportunity lifecycle by aligning business sales stages with system automation, validations, revenue tracking, and approval workflows.

---

### 🔹 1️⃣ Stage Customization

* Created custom Sales Processes
* Used Record Types for different business units
* Added stage-specific mandatory fields

Example:

* "Proposal Sent" → Require Quote attached
* "Closed Won" → Require Contract ID

---

### 🔹 2️⃣ Automation Based on Stage

Implemented:

* Auto probability update
* Close date auto-adjustment
* Stage-based task creation
* Email alerts to management
* Trigger-based revenue validation

Example:

> When Opportunity moves to "Closed Won", system automatically:
>
> * Creates onboarding Case
> * Creates Contract record
> * Sends notification to Finance team

---

### 🔹 3️⃣ Revenue Controls

* Validation on discount % threshold
* Approval process for high discount
* Pricebook restrictions by region
* Product bundling logic

---

### 🔹 4️⃣ Performance Optimization

* Avoided heavy trigger logic on every stage update
* Used Queueable for post-close integrations
* Indexed frequently filtered fields
* Optimized reports & dashboards

---

### 🔥 Strong IC Impact Statement

> I ensured that Opportunity automation was modular, bulkified, and scalable, as Opportunity is typically the highest transaction volume object in Sales Cloud.

---

# ✅ 3️⃣ How Do You Handle Complex Automation in Sales Cloud?

Manager is testing your architecture maturity here.

---

### 🔹 Step 1: Categorize Automation

I divide automation into:

1. Declarative (Flow, Validation, Approval)
2. Programmatic (Apex Trigger, Batch, Queueable)
3. Integration-driven automation

---

### 🔹 Step 2: Follow Automation Hierarchy

I always follow:

Flow first (if feasible)
Apex only when required

Avoid mixing too many tools unnecessarily.

---

### 🔹 Step 3: Example of Complex Automation

Example Scenario:

* On Opportunity update:

  * Validate pricing logic
  * Check credit limit from external system
  * Apply discount rules
  * Trigger approval if needed
  * Update related Account
  * Send integration payload to ERP

---

### 🔹 How I Architect It

Instead of putting everything in one trigger:

✔ Use Trigger Framework
✔ Separate service layer classes
✔ Use custom metadata for configurable rules
✔ Use Queueable for callouts
✔ Use Platform Events if decoupling needed

---

### 🔹 Handling Order of Execution

Be ready to say:

> I carefully design automation considering Salesforce Order of Execution to avoid recursion, duplicate processing, and unexpected field overwrites.

---

### 🔹 Bulk & Governor Limit Handling

* Use collections
* Single SOQL per object
* No SOQL inside loops
* Use Maps for lookups
* Avoid DML inside loops

---

### 🔹 Monitoring & Error Handling

* Custom logging object
* Try-catch blocks
* Retry mechanism for failed integrations
* Email alert for failed transactions

---

### 🔥 Very Strong Manager-Level Closing

> My focus in complex automation is maintainability and scalability. I avoid tightly coupled logic and ensure the solution can evolve as business requirements grow.

---

# 🎯 What Manager Is Actually Evaluating

They want to see:

✔ You understand Sales Cloud deeply
✔ You think architecturally
✔ You care about performance
✔ You understand enterprise complexity
✔ You can own things independently

---
🎯 What interviewer really wants to know

- When they ask “Are you an individual contributor?”, they are checking:
- Can you work independently without hand-holding?
- Can you take ownership of features end-to-end?
- Can you design + develop + deliver?
- Are you reliable without constant supervision?

Answer : 

> Yes, I am a strong individual contributor. In my current role, I take ownership of features end-to-end, from requirement understanding to development, testing, and deployment.
At the same time, I also collaborate closely with my team, review code, and help junior developers when needed.
So I can work independently as well as contribute to the team’s success.