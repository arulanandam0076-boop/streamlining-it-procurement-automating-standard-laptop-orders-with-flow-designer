# Streamlining IT Procurement: Automating Standard Laptop Orders with Flow Designer

A ServiceNow automation project designed to streamline the hardware request fulfillment lifecycle using Flow Designer. When a standard laptop request is approved, this workflow automatically provisions and routes fulfillment tasks to the Hardware support group, minimizing turnaround time and eliminating manual dispatch bottlenecks.

---

## 📌 Project Overview

* **Platform:** ServiceNow
* **Role / Track:** ServiceNow System Administrator / Developer
* **Primary Module:** Flow Designer & Service Catalog Automation
* **Trigger:** Service Catalog Request Item (`sc_req_item`) Approval
* **Target Record:** Catalog Task (`sc_task`)

---

## 🎯 Business Problem & Solution

### The Challenge
Fulfillment for standard workplace equipment often relies on manual hand-offs. When requests wait for manual triaging after manager approval, fulfillment times lengthen, human errors in routing occur, and SLA compliance drops.

### The Solution
An automated, event-driven workflow built in ServiceNow Flow Designer that:
1. Listens for the approval of a **Standard Laptop** catalog item.
2. Automatically generates a child **Catalog Task (`sc_task`)** under the parent Requested Item (`sc_req_item`).
3. Dynamically assigns the task to the **Hardware** group with standard configuration and provisioning instructions.
4. Updates stage progress visible to both the requester and the fulfiller in real time.

---

## 🏗️ Workflow Architecture

```text
[End User submits Laptop Request]
               │
               ▼
      [Approval Process]
               │
      [Status: Approved] ───────────► (Flow Designer Trigger)
                                             │
                                             ▼
                                  [Create Catalog Task]
                                   ├── Parent: sc_req_item
                                   ├── Assignment Group: Hardware
                                   └── Short Description: "Provision Standard Laptop"
                                             │
                                             ▼
                                  [Hardware Team Fulfillment]
```

---

## 📂 Repository Structure

```text
.
├── README.md
└── Screenshots/
    ├── Screenshot 2026-10-01 134027.png   # Service Catalog Item setup
    ├── Screenshot 2026-10-01 134630.png   # Flow trigger and condition setup
    ├── Screenshot 2026-10-01 135103.png   # Action configuration & field mapping
    └── Screenshot 2026-10-01 135922.png   # Flow execution details & created SCTASK
```

---

## ⚙️ Implementation Milestones

### 1. Catalog Item Definition
* Configured the **Standard Laptop** item within the IT Service Catalog.
* Configured user-facing variables (e.g., specifications, delivery location, special instructions).

### 2. Flow Designer Configuration
* **Trigger:** Set trigger to `Service Catalog` / `sc_req_item` state update where `Approval` changes to `Approved`.
* **Action:** Added core ServiceNow action `Create Catalog Task`.
* **Data Mapping:**
  * **Requested Item:** Linked via Data Pill to the triggering `sc_req_item` record.
  * **Short Description:** Configured clear provisioning instructions.
  * **Assignment Group:** Assigned directly to the `Hardware` group.

### 3. Catalog Integration & Activation
* Linked the flow to the process engine of the catalog item.
* Activated the flow to enable real-time execution in the instance.

---

## 🧪 Verification & Results

| Test Step | Action Taken | Expected Result | Actual Result |
| :---: | :--- | :--- | :---: |
| **01** | Submit request via Service Portal | `REQ` and `RITM` records generated | ✅ Passed |
| **02** | Approve request | Approval state transitions to `Approved` | ✅ Passed |
| **03** | Flow Triggering | Flow Designer initiates execution instance | ✅ Passed |
| **04** | Task Creation | `sc_task` generated and routed to `Hardware` | ✅ Passed |

---

## 🖼️ Visual Walkthrough

### 1. Service Catalog Configuration
Configuring the catalog item and input parameters for the laptop order.

![Catalog Item Configuration](Screenshots/Screenshot%202026-10-01%20134027.png)

---

### 2. Trigger Logic & Conditions
Setting up the approval condition trigger in Flow Designer.

![Flow Trigger](Screenshots/Screenshot%202026-10-01%20134630.png)

---

### 3. Action Mapping: Create Catalog Task
Defining field mappings, assignment groups, and dynamic data pills.

![Create Catalog Task Action](Screenshots/Screenshot%202026-10-01%20135103.png)

---

### 4. Execution Details & Verification
Flow Designer execution log confirming clean execution and task generation.

![Execution Details](Screenshots/Screenshot%202026-10-01%20135922.png)

---

## 🚀 Setup & Git Instructions

To use this file in your local repository, replace the temporary text file:

```cmd
:: From C:\Arul
ren README.md.txt README.md

:: Stage, commit, and push
git add README.md Screenshots/
git commit -m "docs: add project README and process screenshots"
git push origin main
```