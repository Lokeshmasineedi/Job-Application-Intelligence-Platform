# Job Application Intelligence Platform

An event-driven job application intelligence platform that automatically discovers job applications, monitors recruitment communications, identifies hiring-stage updates, maintains application timelines, and notifies users of important recruitment events with minimal manual intervention.

## Overview

Managing multiple job applications across company career pages, job portals, and email communications can become difficult because application updates are distributed across different platforms and inbox messages.

The Job Application Intelligence Platform centralizes this process by automatically detecting job applications and recruitment-related emails, extracting relevant information, matching communications to the appropriate application, identifying recruitment events, updating application status, and notifying users when meaningful changes occur.

The system follows the principle:

> **Record once, track automatically.**

## Key Features

* Automatic detection of job applications from supported job portals and application confirmation pages
* Gmail integration for monitoring recruitment-related communications
* Automatic extraction of company, role, job ID, job URL, application date, and related application information
* Event-driven Gmail notification processing using Google Cloud Pub/Sub
* AI-assisted classification of recruitment emails
* Detection of application confirmations, shortlists, online assessments, interviews, offers, rejections, recruiter outreach, and scheduling updates
* Intelligent matching of incoming emails with existing job applications
* Application status and recruitment timeline management
* Automatic dashboard updates
* Real-time user notifications for important application events
* Confidence-based handling of uncertain email classifications
* Complete recruitment event history for each application
* Secure user authentication and authorization
* RESTful backend APIs
* PostgreSQL-based application and event storage
* Browser extension support for capturing application information from supported portals

## How It Works

### 1. Connect Account

The user creates an account and connects their Gmail account using secure OAuth authentication.

### 2. Apply for a Job

The user applies for a job through a supported job portal or company career page.

The system automatically captures available information such as:

* Company
* Job title
* Job ID
* Job URL
* Application date
* Application source

### 3. Detect Application Confirmation

When an application confirmation email is received, the Gmail integration detects the mailbox change and retrieves the relevant message.

The system extracts useful information from the email and associates it with the corresponding application.

### 4. Analyze Recruitment Communication

Incoming recruitment emails pass through an email intelligence pipeline that combines deterministic rules with AI-assisted classification.

Possible recruitment events include:

* Application Confirmation
* Shortlisted
* Online Assessment
* Assessment Completed
* Technical Interview
* HR Interview
* Final Interview
* Offer
* Rejection
* Recruiter Outreach
* Interview Scheduling

### 5. Match Email With Application

The system identifies the application associated with the email using multiple signals such as:

* Company
* Sender domain
* Job title
* Job ID
* Job URL
* Email thread
* Application date
* Message context

### 6. Update Application Timeline

After identifying the recruitment event, the application timeline is automatically updated.

Example:

```text
Google — Software Engineer

17 Aug
Application Detected

17 Aug
Application Confirmed

21 Aug
Online Assessment

25 Aug
Assessment Completed

28 Aug
Technical Interview
```

### 7. Notify the User

The system sends a notification when an important recruitment event is detected.

Example:

```text
Google — Application Update

Your application for Software Engineer
has progressed to a Technical Interview.
```

## System Architecture

```text
                         USER
                           |
                           v
                  +----------------+
                  | React Frontend |
                  +-------+--------+
                          |
                       REST API
                          |
                          v
                  +----------------+
                  | FastAPI Backend|
                  +-------+--------+
                          |
          +---------------+----------------+
          |               |                |
          v               v                v
    +-----------+   +-----------+   +-------------+
    | PostgreSQL|   | Gmail API |   | Notification|
    +-----------+   +-----+-----+   +-------------+
                          |
                          v
                  +---------------+
                  | Google Cloud  |
                  |    Pub/Sub    |
                  +-------+-------+
                          |
                          v
                  +---------------+
                  | Email          |
                  | Processing     |
                  +-------+--------+
                          |
              +-----------+-----------+
              |                       |
              v                       v
       Rule-Based Analysis     AI Classifier
              |                       |
              +-----------+-----------+
                          |
                          v
                  Application Matcher
                          |
                          v
                  Status/Event Engine
                          |
                          v
                     PostgreSQL
                          |
                          v
                     Dashboard
```

## Application Lifecycle

```text
Application Detected
        |
        v
Application Confirmed
        |
        v
Shortlisted
        |
        v
Online Assessment
        |
        v
Assessment Completed
        |
        v
Technical Interview
        |
        v
HR Interview
        |
        v
Final Interview
        |
        +------------+
        |            |
        v            v
      Offer       Rejected
```

The actual application timeline depends on the recruitment process of each company.

## Email Intelligence Pipeline

```text
Incoming Email
      |
      v
Extract Email Metadata
      |
      v
Recruitment Relevance Check
      |
      v
Company / Role / Job Identification
      |
      v
Application Matching
      |
      v
Recruitment Event Classification
      |
      v
Confidence Evaluation
      |
      v
Application Status Update
      |
      v
Notification
```

The system does not rely exclusively on AI. Deterministic rules are used for strong signals, while AI-assisted classification is used for ambiguous recruitment communications.

## Database Design

### Users

Stores authenticated user information.

```text
users
-------------------------
id
name
email
password_hash
created_at
```

### Applications

Stores detected job applications.

```text
applications
-------------------------
id
user_id
company
role
job_id
job_url
applied_at
current_status
source
created_at
```

### Events

Stores the complete recruitment history of an application.

```text
events
-------------------------
id
application_id
event_type
event_time
source
confidence
created_at
```

### Emails

Stores relevant email metadata and classification results.

```text
emails
-------------------------
id
user_id
message_id
sender
subject
received_at
classification
created_at
```

### Notifications

Stores notifications generated for users.

```text
notifications
-------------------------
id
user_id
application_id
message
read
created_at
```

## Technology Stack

### Frontend

* React
* HTML5
* CSS3
* JavaScript / TypeScript

### Backend

* Python
* FastAPI
* REST APIs

### Database

* PostgreSQL

### AI

* LLM API
* AI-assisted email classification
* Entity extraction
* Recruitment event detection

### Integrations

* Gmail API
* Google OAuth
* Google Cloud Pub/Sub
* Browser Extension APIs
* Supported job-portal integrations

### Development & Deployment

* Git
* GitHub
* Docker
* REST API testing tools

## Security

The application follows security principles for handling user and email-related information.

Key considerations include:

* OAuth-based Gmail authentication
* Least-privilege access to user email data
* Secure credential and token handling
* Password hashing
* User-level authorization
* Application data isolation
* Environment variables for secrets
* Protection of API credentials
* Validation of external input
* Secure API communication

Sensitive credentials and OAuth tokens are never committed to the repository.

## Example Workflow

```text
User applies for:

Company: Google
Role: Software Engineer
Job ID: SWE-2026-123
```

The system detects the application from a supported application source or confirmation email.

Later, Gmail receives:

```text
Subject:
Your Google application has progressed
```

The system processes the email and identifies:

```text
Company: Google
Role: Software Engineer
Event: Online Assessment
Confidence: High
```

The application timeline is automatically updated:

```text
Applied
   |
   v
Application Confirmed
   |
   v
Online Assessment
```

The user receives:

```text
Google — Application Update

Your Software Engineer application
has progressed to an Online Assessment.
```

## Project Structure

```text
Job-Application-Intelligence-Platform/
|
├── backend/
│   ├── app/
│   ├── api/
│   ├── models/
│   ├── services/
│   ├── database/
│   └── tests/
|
├── frontend/
│   ├── src/
│   ├── components/
│   ├── pages/
│   └── services/
|
├── browser-extension/
│   ├── manifest.json
│   ├── background/
│   ├── content/
│   └── popup/
|
├── docs/
│   ├── architecture/
│   └── api/
|
├── tests/
|
├── .gitignore
├── docker-compose.yml
├── README.md
└── LICENSE
```

## Future Enhancements

* Additional job-portal integrations
* More recruitment email providers
* Calendar integration for interview scheduling
* Advanced application analytics
* Interview preparation recommendations
* Automatic job-description extraction
* Personalized application insights
* Recruitment process duration analysis
* Application follow-up recommendations
* Advanced notification preferences

## Project Goals

The project demonstrates practical implementation of:

* Event-driven architecture
* Backend API development
* Database design
* OAuth authentication
* External API integration
* Email processing
* AI-assisted classification
* Entity matching
* State management
* Automated notifications
* Browser-extension development
* Containerized application development

## License

MIT License
