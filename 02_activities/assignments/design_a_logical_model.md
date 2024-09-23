# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).
![Bookstore Diagram]([./bookstore-diagram.png](https://github.com/DmytroBolokhonov/sql/blob/model-design/02_activities/assignments/dmytro_bolokhonov_design_a_logical_model.png))

## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

## Customer_Address Architectures: Type 1 vs. Type 2 SCD

The store can adopt one of two possible architectures for handling customer addresses: **Type 1 Slowly Changing Dimension (SCD)**, which overwrites address changes, or **Type 2 SCD**, which retains a history of changes.

### Type 1 SCD: Overwriting Changes
In this approach, when a customer’s address is updated, the old address is overwritten, and only the most current address is stored. No historical data is maintained.

**Customer_Address (Type 1)**:
- `customer_id` (Primary Key, Foreign Key)
- `address_line_1`
- `address_line_2`
- `city`
- `province`
- `postal_code`
- `country`

### Type 2 SCD: Retaining Changes
In this design, a new record is created whenever a customer’s address is updated, preserving the old address and allowing for the tracking of address changes over time.

**Customer_Address (Type 2)**:
- `address_id` (Primary Key)
- `customer_id` (Foreign Key)
- `address_line_1`
- `address_line_2`
- `city`
- `province`
- `postal_code`
- `country`
- `address_start_date`
- `address_end_date`
- `is_current` (Boolean): Indicates whether this is the current address (true/false).

### Privacy Considerations
#### Type 1 (Overwriting Changes)
- **Pros**: Simplifies data management with fewer records.
- **Cons**: Lacks historical data, which may be a disadvantage for auditing or tracking changes.

#### Type 2 (Retaining Changes)
- **Pros**: Retains a full history of address changes, which is useful for audits and tracking customer data.
- **Cons**: Storing historical addresses may increase privacy risks, especially if old addresses contain sensitive information.

## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

## Comparison Between My ERD and the AdventureWorks Schema

The **AdventureWorks** schema is highly detailed and organized, covering specific business domains. When comparing it to my ERD, there are several key differences:

### Scope and Coverage
- **AdventureWorks**: Spans various business areas such as sales, purchasing, human resources, and production, making it a comprehensive model suited for enterprise-level applications.  
- **My ERD**: Initially, my design focused on core entities related to a bookstore (Employee, Order, Sales, Customer, and Book). Inspired by the AdventureWorks schema, I’ve since expanded to include more entities and improve the depth of my design.

### Entity Relationships
- **AdventureWorks**: Features complex relationships, including many-to-many relationships, associative entities, and hierarchical structures.  
- **My ERD**: Started with simpler one-to-many and many-to-one relationships. However, after studying the AdventureWorks schema, I have incorporated more detailed and complex relationships into my design.

### Attribute Details
- **AdventureWorks**: Attributes are thoroughly detailed, including constraints, data types, and relationships across multiple tables.  
- **My ERD**: Initially less detailed, but inspired by AdventureWorks, I have refined the granularity of attributes in my model.

### Complexity
- **AdventureWorks**: A large, complex schema with numerous tables and intricate relationships.  
- **My ERD**: As I've drawn inspiration from AdventureWorks, my ERD has evolved to include additional tables and increased complexity.

### Normalization
- **AdventureWorks**: Likely follows high levels of normalization to minimize redundancy and enhance data integrity.  
- **My ERD**: Initially less normalized, but after analyzing AdventureWorks, I have aimed for higher normalization levels to improve data organization and consistency.

### Summary
The AdventureWorks schema has inspired me to enhance the level of detail and complexity in my ERD, making it more robust and reflective of best practices in database design.


# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `September 28, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-4-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
