# GitHub Copilot Ask & Agent Mode Guide for SAP ABAP Cloud Migrations

## Accelerating Lift-and-Shift Modernization

**Document Version:** 1.0  
**Target Audience:** SAP ABAP Developers (Intermediate to Advanced)  
**Date Created:** July 2026  
**Purpose:** Enable rapid code modernization from legacy ABAP to ABAP Cloud Clean Core using GitHub Copilot

---

## Table of Contents

1. Introduction
2. Prompt Engineering Strategies
3. Chat Management & Context Optimization
4. Creating Technical Design Documents
5. Practical Workflow Examples
6. Best Practices & Tips

---

## 1. Introduction

GitHub Copilot's **Ask Mode** and **Agent Mode** are powerful tools for accelerating SAP ABAP Cloud migrations. This document shares proven strategies from real lift-and-shift modernization projects, specifically focusing on converting legacy ABAP code (5-10 years old) to Clean Core-compliant versions.

### Key Use Cases Covered:

- Converting legacy Interfaces to Clean Core standards
- Modernizing Reports and Classes
- Generating business logic summaries and pseudo code
- Creating technical design documentation
- Building visual flow diagrams with error handling

---

## 2. Prompt Engineering Strategies

Effective prompt engineering is the foundation of getting quality outputs from GitHub Copilot. Here are proven strategies from real ABAP Cloud migration projects:

### 2.1 Structured Input Format - The 3-Part Method

When working with legacy ABAP code, use this three-part prompt structure:

**Part 1: Context Definition**

I have a legacy SAP ABAP class/interface/report that needs to be modernized to ABAP Cloud Clean Core.

Current System: [SAP System Version - e.g., S/4 HANA 2021]
Migration Scope: [Interface/Report/Class]
Current Technical Debt: [Brief description - e.g., "Uses deprecated FM, custom database logic"]

**Part 2: Request Specification**

Please perform the following analysis:
1. Generate a business logic summary (5-10 bullet points)
2. Identify deprecated patterns and Clean Core alternatives
3. Provide pseudo code for the modernized version
4. List TR objects that need to be created

**Part 3: Code Submission**

Here is the current ABAP code to analyze:

[PASTE FULL CLASS/INTERFACE CODE HERE]

### 2.2 Real-World Example: Interface Modernization Prompt

**Legacy Code Context:**

```
INTERFACE zif_payment_old.
  TYPES: BEGIN OF ty_payment,
           amount TYPE p DECIMALS 2,
           currency TYPE char3,
           bank_details TYPE string,
         END OF ty_payment.
  
  METHODS process_payment
    IMPORTING
      iv_payment TYPE ty_payment
    EXPORTING
      ev_status TYPE char1
      ev_msg    TYPE string.
      
  METHODS get_bank_details
    IMPORTING
      iv_account TYPE string
    EXPORTING
      ev_bank_code TYPE string.
ENDINTERFACE.
```

**Effective Prompt:**

Context:
- Legacy Payment Interface (5 years old) - S/4 HANA 2018
- Used in custom MM integration
- Contains direct database access patterns
- Needs Clean Core compliance for ABAP Cloud

Task:
1. Analyze this legacy interface and provide:
   - 5-10 point business logic summary
   - Data structure improvements for Clean Core
   - Method signature updates needed
   - Recommended Clean Core patterns (e.g., RAP, CDS)

2. Identify all TR objects (INTF, STRUC, DOMA, DTEL)

3. Provide pseudo code showing the modernized approach

4. Create a comparison table: Old Pattern vs. Clean Core Pattern

Here is the interface code:
[PASTE CODE]

### 2.3 Prompt Variations for Different Scenarios

**For Complex Class Analysis:**

I need to modernize a legacy ABAP class [CLASS_NAME] used in [module/process].

The class is currently ~[number] lines and handles [primary responsibility].

Provide:
1. Business logic breakdown (method by method)
2. Data flow diagram description
3. Clean Core compliance checklist
4. Refactoring roadmap (high-level steps)

Code: [PASTE]

**For Report Conversion:**

Convert this legacy ABAP report [REPORT_NAME] to modern ABAP Cloud practices.

Current Logic:
- Input: [describe input parameters]
- Processing: [describe main logic]
- Output: [describe output]

Convert to:
1. CDS view for data retrieval
2. Query-based filtering logic
3. OData service for consumption
4. Fiori UI considerations

Code: [PASTE]

**For Function Module to Method Migration:**

Migrate this legacy Function Module to a Clean Core method.

FM Details:
- Name: [FM_NAME]
- Used by: [number] of programs
- Main Purpose: [describe]
- Dependencies: [list any external calls]

Deliverables:
1. Equivalent method structure
2. Exception handling updated
3. Clean Core compatibility checklist

Code: [PASTE]

### 2.4 Prompt Engineering Best Practices

| Practice | Do ✅ | Don't ❌ |
|----------|-------|---------|
| Clarity | Be specific: "Convert to Clean Core REST API service" | Vague: "Make it modern" |
| Context | Provide system info, module, existing constraints | Assume Copilot knows your architecture |
| Structure | Use numbered lists and sections | One long paragraph |
| Code Format | Complete, copy-pasted code with syntax highlighting | Fragmented snippets or pseudocode |
| Scope | Focus one class/interface per prompt | Dump 10 programs at once |
| Iteration | Follow-up with refinements: "Now add error handling..." | Start over completely |
| Constraints | Mention Clean Core restrictions upfront | Expect Copilot to know deprecated FM list |

---

## 3. Chat Management & Context Optimization

### 3.1 Understanding Token Limits & Context Window

GitHub Copilot operates with a context window that includes:
- Your conversation history
- Attached files or code snippets
- System prompt information

**Practical Limits:**
- Single Large Code Block: 5,000-10,000 lines (depends on code density)
- Conversation History: Up to 20-30 exchanges before context becomes stale
- Optimal Chat Length: 15-25 messages per chat

### 3.2 When to Continue vs. Start a New Chat

**Continue in the Same Chat When:**

✅ Building on previous analysis (e.g., "Now add error handling to method X")
✅ Refining outputs (e.g., "Update the pseudo code to include exception logic")
✅ Sequential related tasks (e.g., analyze class → design CDS views → create service)
✅ Within 15-20 exchanges

Example Flow (Same Chat):
```
Message 1: [Analyze legacy interface]
Message 2: [Follow-up: "Add exception handling patterns"]
Message 3: [Follow-up: "Create technical design doc with this info"]
Message 4: [Follow-up: "Now create a flowchart for the process"]
```

**Start a New Chat When:**

❌ Switching to completely different component/module
❌ Chat exceeds 25 messages
❌ Context feels "stale" or Copilot is repeating patterns
❌ Working with unrelated legacy code
❌ Need fresh perspective on architecture

Example (New Chat Needed):
```
Chat 1: [Modernize Payment Interface]
Chat 2: [NEW CHAT] Modernize User Authentication Module
Chat 3: [NEW CHAT] Migrate Custom Reports to Fiori
```

### 3.3 Maintaining Conversation Coherence

**Strategy A: Progressive Refinement (Best for Design Docs)**

```
Turn 1: "Analyze this class - provide 5-10 point summary"
[Gets response]

Turn 2: "Based on that analysis, now create a TR objects table"
[Gets response]

Turn 3: "Create a technical design document using both summaries"
[Gets response]

Turn 4: "Now design a flowchart based on the method flow described above"
[Gets response]
```

Context Maintenance Tips:
- Reference previous outputs: "Based on the summary from Turn 1..."
- Use numbered sections to avoid ambiguity
- Remind Copilot of constraints: "Remember, this must be Clean Core compliant"

**Strategy B: Modular Chats (Best for Multiple Components)**

```
CHAT 1: Payment Interface Analysis
├─ Analyze structure
├─ Get TR objects
└─ Create summary

CHAT 2: Payment Class Modernization
├─ Design class methods
├─ Create pseudo code
└─ Design flowchart

CHAT 3: Integration Testing Design
├─ Design test scenarios
├─ Create test cases
└─ Documentation
```

### 3.4 Context Window Management Checklist

Before each prompt, ask yourself:

- [ ] Is this related to the previous task? (If no → new chat)
- [ ] How many messages have we exchanged? (If >20 → consider new chat)
- [ ] Is the conversation still focused on the same component? (If no → new chat)
- [ ] Will adding more code exceed comfortable limit? (If yes → new chat)
- [ ] Do I need Copilot to "forget" the previous context? (If yes → new chat)

### 3.5 Optimization Tips for Long Chats

| Technique | Usage | Example |
|-----------|-------|---------|
| Summarize | After 5-7 exchanges, ask for a summary | "Summarize what we've designed so far in 100 words" |
| Reference | Use turn numbers to reference back | "Referring to Turn 3's analysis..." |
| Bookmark | Ask Copilot to recall key decisions | "Remember the Clean Core patterns we identified?" |
| Compress | Move long outputs to external docs | "Save this as a markdown file for later reference" |

---

## 4. Creating Technical Design Documents

### 4.1 Class/Method Summary: 5-10 Point Pseudo Code Generation

This is the most powerful use case for Copilot. Here's the proven workflow:

**Step 1: Prepare Your Code**

Copy the entire class from Eclipse into a text file. Ensure:
- Full syntax is preserved
- Include all methods
- Include all type definitions
- Include import statements

**Step 2: Use the Summary Prompt Template**

I need to create a technical design document for a legacy ABAP class that's being modernized.

Class Context:
- Name: [CLASS_NAME]
- Current Module: [MM/FI/HR/etc.]
- LOC: [Approximate lines]
- Last Modified: [Year]
- Purpose: [Brief description]
- Clean Core Target: [Yes/No - describe constraints]

Deliverable:
Create a 5-10 point business logic summary that:
1. Explains what the class does in plain English
2. Lists each public method's responsibility
3. Identifies key data transformations
4. Notes any database access patterns
5. Highlights performance-critical sections
6. Lists external dependencies
7. Notes deprecated patterns found
8. Suggests Clean Core alternatives
9. Lists required TR objects
10. Provides pseudo code for modernization

Format as a technical document with sections.

Here is the class code:

[PASTE ENTIRE CLASS]

**Step 3: Structured Output Extraction**

Copilot will provide output like:

## Class Analysis: ZCL_PAYMENT_PROCESSOR

### 1. Business Logic Summary

The class handles payment processing with three main phases:
- Payment validation and formatting
- Integration with legacy banking system
- Response mapping to payment status

### 2. Method Breakdown

- CONSTRUCTOR: Initializes connection parameters
- VALIDATE_PAYMENT: Checks amount, currency, account details
- CALL_BANK_API: External FM call (DEPRECATED in Clean Core)
- MAP_RESPONSE: Transforms bank response to internal format
- GET_ERROR_MESSAGE: Exception handling

### 3. Data Transformations

- Input: Payment structure (Amount, Currency, Account)
- Processing: Direct DB select + FM call
- Output: Payment status + error message

### 4. Database Access Patterns

- Direct SELECT: "SELECT * FROM BKPF" (non-standard)
- Should use CDS Views in Clean Core

### 5. Performance-Critical Sections

- VALIDATE_PAYMENT: Uses indexed reads ✓
- CALL_BANK_API: External call (network latency) ⚠️

### 6. External Dependencies

- Function Module: Z_BANK_INTERFACE_CALL (custom, deprecated)
- RFC: RFC_READ_TABLE (deprecated pattern)
- Standard FM: SY-DATE (time zone issues)

### 7. Deprecated Patterns Identified

❌ Direct DB access (SELECT *)
❌ Custom function modules for integration
❌ String-based date handling
❌ No exception handling structure
❌ Hard-coded system parameters

### 8. Clean Core Alternatives

✅ CDS Views for data access
✅ OData services for external integration
✅ Type-safe data handling with ADT types
✅ Structured exception framework
✅ Environment-aware configuration

### 9. TR Objects Required

| Object Type | Object Name | Purpose |
|-------------|------------|---------|
| Interface | ZIF_PAYMENT_SERVICE | Contract for payment processing |
| Class | ZCL_PAYMENT_SERVICE | Modernized payment class |
| CDS View | Z_C_PAYMENT_VALIDATION | Data retrieval layer |
| CDS View | Z_I_PAYMENT_DATA | Transactional data |
| Service | Z_PAYMENT_ODATA | External system integration |
| Entity | PaymentHeader | OData entity |
| Entity | PaymentLine | OData entity |
| Table Type | ZTT_PAYMENT | For internal logic |

### 10. Pseudo Code (Modernized)

```
CLASS zcl_payment_service DEFINITION.
  PRIVATE SECTION.
    DATA: mo_payment_dao TYPE REF TO zif_payment_dao,
          mo_bank_adapter TYPE REF TO zif_bank_adapter.
  
  PUBLIC SECTION.
    METHODS process_payment
      IMPORTING is_payment TYPE zs_payment_data
      EXPORTING es_result TYPE zs_payment_result
      RAISING zcx_payment_error.
ENDCLASS.

CLASS zcl_payment_service IMPLEMENTATION.
  METHOD process_payment.
    " Validation: Use domain class validators
    TRY.
      DATA(lo_validator) = NEW zcl_payment_validator().
      lo_validator->validate( is_payment ).
    CATCH zcx_validation_error INTO DATA(lx_val_error).
      RAISE EXCEPTION TYPE zcx_payment_error(
        previous = lx_val_error ).
    ENDTRY.
    
    " Data Access: Use CDS DAO pattern
    DATA(lt_billing_data) = mo_payment_dao->get_billing_data(
      is_payment-customer_id ).
    
    " Integration: Use adapter pattern for banking system
    TRY.
      es_result = mo_bank_adapter->submit_payment(
        is_payment = is_payment
        it_billing_data = lt_billing_data ).
    CATCH zcx_bank_error INTO DATA(lx_bank_error).
      es_result-status = 'ERROR'.
      es_result-message = lx_bank_error->get_text().
    ENDTRY.
  ENDMETHOD.
ENDCLASS.
```

### 4.2 TR Objects Table Specification

Once you have the summary, use this follow-up prompt to populate the TR objects table:

**Prompt for TR Objects Population:**

Based on the class analysis above, I need a comprehensive TR objects table for the implementation team.

Requirements:
1. List all ABAP objects that need to be created
2. Include SAP-provided tables/domains to be used
3. Specify dependencies between objects
4. Add development component assignment
5. Include estimated effort per object

Format as a detailed table with these columns:
- Object Type
- Object Name
- Description
- Purpose/Usage
- Dependencies
- Development Component
- Estimated Effort
- Priority
- Notes

Use the methods and types identified in the class analysis above.

### 4.3 Creating Technical Design Document (All-in-One)

**Comprehensive Prompt:**

I need to create a complete technical design document for the modernized class. Using the analysis and TR objects we've identified, create a document that includes:

1. Executive Summary (2-3 paragraphs)
2. Architecture Overview
3. Functional Design
4. Technical Design
5. TR Objects Inventory
6. Implementation Roadmap
7. Testing Strategy
8. Migration Plan
9. Operations & Support

Create this as a professional document ready for stakeholder review.

---

## 5. Practical Workflow Examples

### 5.1 Complete Flow - Legacy Interface to Clean Core Service

**Chat Structure: Single Chat (5 Messages)**

**Message 1: Initial Analysis**

Context:
- Legacy Payment Interface used in FI module (created 2016)
- Custom database access patterns
- Used in 12 reports and 3 interfaces
- Must be converted to Clean Core OData service

Task:
Provide a 5-10 point business logic summary of this interface, identify all methods, 
and list the Clean Core patterns we should use instead.

[PASTE INTERFACE CODE]

**Message 2: TR Objects Specification**

Based on the analysis above, create a comprehensive TR objects table including:
- All custom objects needed
- Standard SAP objects we'll use
- Dependencies between objects
- Development component assignments
- Implementation sequence

Format for team handoff.

**Message 3: Technical Design Document**

Using the summary and TR objects table, create a complete technical design document 
with sections for: Executive Summary, Architecture, Functional Design, Technical Design, 
TR Objects, Implementation Roadmap.

**Message 4: Service Implementation Pseudo Code**

Now provide detailed pseudo code for:
1. Service class (ZCL_PAYMENT_SERVICE) with all public methods
2. Data Access Object (ZCL_PAYMENT_DAO) for CDS integration
3. Adapter for external bank system integration (REST-based, Clean Core compliant)
4. Exception handling structure

Include comments explaining Clean Core compliance.

**Message 5: Process Flowchart**

Create a textual description of a flowchart for the payment processing method.
Include:
- Start point
- Validation steps
- Data fetch operations
- External system call
- Error handling branches
- Success/failure responses
- End point

**Expected Deliverables After Chat:**

✅ Business logic summary (5-10 points)
✅ TR objects table (20+ rows)
✅ Technical design document
✅ Pseudo code for all classes
✅ Flowchart description

### 5.2 Report Conversion Process

**Sample Legacy Report Context**

```
REPORT z_old_payment_report.

PARAMETERS: p_date TYPE sy-datum,
            p_cust TYPE kna1-kunnr.

DATA: lt_bkpf TYPE TABLE OF bkpf,
      lt_output TYPE TABLE OF ty_payment_output.

SELECT * INTO TABLE lt_bkpf
  FROM bkpf
  WHERE budat = p_date
    AND bukrs = 'US01'.

LOOP AT lt_bkpf INTO DATA(ls_bkpf).
  CALL FUNCTION 'Z_GET_CUSTOMER_PAYMENT_STATUS'
    EXPORTING
      iv_document = ls_bkpf-belnr
      iv_customer = p_cust
    IMPORTING
      es_status = DATA(ls_status).
  
  APPEND VALUE #(
    doc_no = ls_bkpf-belnr,
    amount = ls_bkpf-dmbtr,
    status = ls_status-status
  ) TO lt_output.
ENDLOOP.

LOOP AT lt_output INTO DATA(ls_out).
  WRITE: / ls_out-doc_no, ls_out-amount, ls_out-status.
ENDLOOP.
```

---

## 6. Best Practices & Tips

### 6.1 Code Submission Best Practices

| Do ✅ | Don't ❌ |
|------|---------|
| Copy full method/class from Eclipse | Manually type or retype code |
| Include all TYPES and DATA definitions | Extract only the logic portions |
| Preserve all comments and formatting | Remove formatting to "simplify" |
| Include IMPORTING/EXPORTING sections | Only paste the code body |
| Keep original code as-is | Modify code before pasting |

### 6.2 Getting Better Summaries

**Effective Prompt:**

"This is a payment processing class from 2016. Provide a technical summary 
that explains: (1) what each public method does, (2) what data it processes, 
(3) any performance concerns, (4) deprecated patterns used. Format as 5-10 bullets 
for a design review."

### 6.3 When Copilot Misses Something

**Iteration Strategy:**

```
Turn 1: [Initial analysis]
Turn 2: "You missed the error handling logic in the catch blocks. 
         Please re-analyze including exception handling patterns."
Turn 3: "Now that we've covered exception handling, identify all 
         database access patterns and suggest CDS equivalents."
```

### 6.4 Validating Copilot's Recommendations

Before implementing suggestions:
- [ ] Check against SAP Clean Core Restrictions documentation
- [ ] Verify recommended CDS views exist in your landscape
- [ ] Test OData service patterns in dev environment
- [ ] Cross-check with your Clean Core guidelines
- [ ] Have a senior ABAP developer review critical suggestions

### 6.5 Common Pitfalls to Avoid

| Pitfall | Impact | Solution |
|---------|--------|----------|
| Starting new chat for each method | Loss of context, repetitive analysis | Use single chat for entire class |
| Not validating Copilot suggestions | Potential Clean Core violations | Peer review before implementation |
| Pasting incomplete code | Inaccurate analysis | Always include full class/interface |
| Ignoring deprecated patterns | Technical debt not addressed | Specifically ask for deprecation analysis |
| Not asking for TR objects | Missed objects in implementation | Always request TR object table |
| Vague prompts | Poor quality outputs | Use structured prompt templates |

### 6.6 Quick Reference: Prompt Templates

**Template A: Class Analysis**

```
Analyze this ABAP [CLASS/INTERFACE/FM] from [YEAR] for Clean Core migration.

Context: [Purpose], Used in [Module], [Constraints]

Provide:
1. 5-10 point business logic summary
2. Method breakdown
3. Data transformations
4. External dependencies
5. Deprecated patterns
6. Clean Core alternatives
7. TR objects table
8. Pseudo code for modernized version

Code: [PASTE]
```

**Template B: TR Objects Specification**

```
Create TR objects table for the class analyzed above.

Include: Object Type, Name, Description, Purpose, Dependencies, 
Dev Component, Effort, Priority, Notes.

Format for development team handoff.
```

**Template C: Technical Design Document**

```
Create complete technical design document with:
- Executive Summary
- Architecture Overview
- Functional Design
- Technical Design
- TR Objects Inventory
- Implementation Roadmap
- Testing Strategy
- Migration Plan
- Operations & Support

Make it Word-compatible.
```

**Template D: Process Flow**

```
Create flowchart description for the [METHOD_NAME] method showing:
- Entry/exit points
- Decision points (Yes/No branches)
- Data operations and sources
- External system calls
- Error handling
- Success/failure paths

Format for visual diagram conversion.
```

---

## 7. Summary & Next Steps

### What You Now Have:

✅ Structured prompt engineering techniques
✅ Chat management strategies
✅ Technical design document templates
✅ TR objects specification approach
✅ Flowchart generation method
✅ Best practices and pitfalls to avoid

### Implementation Roadmap:

**Week 1: Pilot with one legacy class**
- Use single chat for complete analysis
- Generate design document
- Get team feedback

**Week 2-3: Standardize across team**
- Share templates with developers
- Establish naming conventions
- Create TR objects board

**Week 4+: Scale to full migration**
- Apply to all lift-and-shift objects
- Measure time savings
- Refine based on lessons learned

### Estimated Time Savings:

- Class analysis: 2-3 hours → 30 minutes (70% reduction)
- Design document: 4-6 hours → 45 minutes (85% reduction)
- TR objects table: 1-2 hours → 15 minutes (90% reduction)
- Pseudo code generation: 3-4 hours → 30 minutes (85% reduction)

---

**Document Version History:**

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | July 2026 | Initial release - Ask & Agent modes guide |

*This document is a living guide. Update with new patterns as you discover them through your migration journey.*
