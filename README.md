# Cofi AI CRM: Multi-Agent Lead Analysis and Sales Outreach

Cofi AI CRM is a Python-based platform that helps sales teams evaluate potential customers, prioritize follow-up, and prepare personalized outreach. Designed around a coffee wholesale business, it transforms customer records into practical recommendations through a **multi-agent workflow powered by Google Gemini on Vertex AI**.

The project addresses a common business challenge: companies collect customer information and engagement data, but sales representatives still need to determine which leads deserve attention, how to approach them, and what to say.

## Multi-Agent Architecture

The application uses six specialized AI agent roles coordinated sequentially in Python. Each role has a distinct task, and relevant outputs are passed to later stages. These roles use the same underlying Gemini model with different instructions.

| Agent                        | What it does                                                                                                                                                                                                                                      |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lead Intake Agent**        | Reviews the customer record and available data fields, then produces a concise profile covering business details, preferences, engagement, and sales status.                                                                                      |
| **Lead Qualification Agent** | Evaluates buying-intent signals such as sample requests, website activity, recurring-order interest, estimated purchase volume, and existing lead scores. Returns a qualification level, confidence assessment, supporting reasons, and concerns. |
| **Follow-Up Strategy Agent** | Recommends a sales approach, contact channel, and urgency level based on the lead’s profile and qualification. Explains why the proposed approach fits the customer.                                                                              |
| **Outreach Agent**           | Drafts a personalized message using customer details, product preferences, and the recommended strategy. Produces email content or a short call script depending on the contact method.                                                           |
| **Outreach Review Agent**    | Evaluates the draft’s personalization, professionalism, call to action, and alignment with the lead’s needs. Provides feedback and revises the message when needed.                                                                               |
| **Sales Summary Agent**      | Combines the analysis into an executive summary, recommended next step, contact channel, and final outreach draft for the sales representative.                                                                                                   |

## Main Features

**Customer Data Preparation**
Loads CRM records from a CSV file, standardizes column names, and handles missing text and numeric values. Records contain information such as business type, product preferences, budget, engagement history, and assigned sales representative.

**Lead Lookup and Profile Summaries**
Retrieves a customer record by lead ID and converts detailed CRM fields into a readable business summary, helping representatives prepare for customer conversations.

**Lead Segmentation and Prioritization**
Includes helper functions to group leads into urgent, high, medium, or low priority. A ranking function selects top leads using existing follow-up priorities and lead scores.

**AI-Assisted Qualification**
Explains why a lead may be worth pursuing by examining engagement and purchasing signals. It also highlights uncertain or inconsistent information that may require further review.

**Personalized Follow-Up Recommendations**
Suggests actions suited to the customer’s situation, such as immediate outreach, a recurring-order discussion, or continued nurturing.

**Outreach Drafting and Review**
Creates customer-specific messages and passes them through a separate review stage before presenting the final draft. Messages are displayed for a sales representative to review and use; the prototype does not send them automatically.

**Interactive Gradio Interface**
Allows users to enter a lead ID and view the customer profile, qualification, sales strategy, outreach draft, review feedback, and final summary in one web interface.

## Related Predictive Analytics Work

A related lead-scoring analysis used logistic regression in Snowflake to estimate conversion likelihood from website engagement data and identify high-potential leads who had not yet converted.

The CRM notebook described here uses scores and priorities already present in its input dataset. It does not directly train or call the Snowflake model within the multi-agent workflow.

## Technology Stack

* **Python:** Data processing and workflow orchestration
* **pandas:** CSV loading, cleaning, filtering, and lead ranking
* **Google Gemini on Vertex AI:** Agent reasoning, recommendations, and message generation
* **Google Gen AI SDK:** Model integration
* **Gradio:** Interactive web interface
* **Google Colab:** Notebook development and experimentation

## Business Value

This project demonstrates how a multi-agent workflow can turn CRM data into actionable sales guidance. It is designed to reduce manual preparation, support consistent lead evaluation, and help representatives focus their efforts on promising opportunities while retaining control over customer communication.
