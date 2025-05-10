# Flow Documentation

## Flow Name: `Next Best Module`

### 🎯 Purpose

This Flow is designed to dynamically identify and flag the next recommended Learning Module for a user. It is part of the personalized learning experience in the **Lead Like** initiative.

***

### 🧩 Context of Use

The Flow is called either manually or from a custom screen to determine which `Learning_Module__c` record should be marked as `Recommended_Next__c = true`, based on the earliest `CreatedDate` and a `Status__c` of "Not Started".

***

### 🔄 Flow Structure

1. **Start (Screen Flow)**
2. **Get Records: `Learning_Module__c`**
   * Criteria: `Status__c = 'Not Started'`
   * Order By: `CreatedDate ASC`
   * Store in variable: `var_LearningModule`
3. **Assignment: Set `Recommended_Next__c = true`**
   * Target: `var_LearningModule.Recommended_Next__c`
   * Value: `true`
4. **End**

***

### 🧠 Business Logic

* The Flow runs in user context and queries for available learning modules.
* Among the "Not Started" ones, it selects the oldest (created first).
* It flags this record as the next recommended module.

***

### ✅ Prerequisites

Ensure that:

* At least one record of `Learning_Module__c` exists with `Status__c = 'Not Started'`.
* The `Recommended_Next__c` is a calculated field, but the Flow sets it directly for testing/demonstration purposes.

***

### 🔧 Technical Notes

* **Object**: `Learning_Module__c`
* **Fields used**:
  * `Status__c` (Restricted Picklist): values include `"Not Started"`, `"In Progress"`, `"Completed"`
  * `Recommended_Next__c` (Formula Checkbox): formula = `ISPICKVAL(Status__c, "Not Started")`
  * `Persona_c__c` (Restricted Picklist): values include `"AI PM"`, `"Community Architect"`

***

### 📸 Demonstration Captures

* [x] Creation of a `Learning_Module__c` record with status "Not Started"
* [x] Flow run showing assignment result in Debug mode
* [x] Resulting module flagged as Recommended in UI

***

### 💡 Next Steps

* Automate flow triggering on module creation
* Include Flow test coverage in deployment package
* Integrate into Scratch Org definition for external demos

***

_This documentation is part of the Lead Like Git project. Include it under `/docs/flows/next-best-module.md` or in the appropriate section in GitBook._
