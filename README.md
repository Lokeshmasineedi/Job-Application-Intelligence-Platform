# Job Application Intelligence Platform

An event-driven job application intelligence platform designed to automatically discover job applications, monitor recruitment communications, identify hiring-stage updates, maintain application timelines, and notify users about important recruitment events.

## Problem

Job seekers often apply to multiple companies through different job portals and company career pages. Tracking application status manually becomes difficult because updates can arrive through different channels such as email, application portals, and recruitment systems.

This project aims to reduce that manual effort by automatically collecting application information and detecting subsequent recruitment updates.

## How It Works

```text
Job Portal / Career Page
          │
          ▼
   Application Detection
          │
          ▼
   Application Database
          │
          │
          ├───────────────┐
          │               │
          ▼               ▼
     Gmail API      Browser Extension
          │               │
          └───────┬───────┘
                  ▼
          Email Intelligence
                  │
          ▼
        Event Classification
                  │
                  ▼
        Application Matching
                  │
                  ▼
        Status / Event Update
                  │
          ┌───────┴────────┐
          ▼                ▼
      Dashboard       Notifications
```

## Core Features

### Automatic Application Detection

Detect relevant application information from supported job portals, career pages, browser-based application flows, and recruitment confirmation emails.

Information may include:

* Company
* Job title
* Job ID
* Job URL
* Application date
* Application source

### Recruitment Email Monitoring

Connect the user's Gmail account and monitor relevant recruitment communications.

The system is intended to identify events such as:

* Application confirmation
* Shortlisting
* Online assessment
* Assessment completion
* Technical interview
* HR interview
* Final interview
* Offer
* Rejection
* Recruiter communication
* Interview scheduling

### AI-Assisted Email Intelligence

Use a combination of deterministic rules and AI-based classification to understand recruitment emails and identify the relevant hiring event.

### Application Matching

Match incoming recruitment emails to the correct job application using signals such as:

* Company
* Email domain
* Job title
* Job ID
* Job URL
* Email thread
* Application date
* Message context

### Automatic Timeline Updates

Maintain a chronological recruitment timeline for each application.

Example:

```text
Application Detected
        ↓
Application Confirmed
        ↓
Online Assessment
        ↓
Assessment Completed
        ↓
Technical Interview
        ↓
HR Interview
        ↓
Offer / Rejection
```

### Notifications

Notify users when an important recruitment event is detected.

Example:

> Google — Software Engineer
> Technical interview invitation detected.

## Planned Technology Stack

### Frontend

* React
* HTML
* CSS
* JavaScript / TypeScript

### Backend

* Python
* FastAPI
* REST APIs

### Database

* PostgreSQL

### Integrations

* Gmail API
* Google Cloud Pub/Sub
* Browser Extension APIs
* Supported job-portal integrations

### AI

* LLM API
* AI-assisted email classification
* Entity extraction
* Application matching

### Development Tools

* Git
* GitHub
* Docker
* Postman

## Planned Architecture

```text
                         ┌─────────────┐
                         │    User     │
                         └──────┬──────┘
                                │
                                ▼
                         React Frontend
                                │
                             REST API
                                │
                                ▼
                         FastAPI Backend
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                 │
              ▼                 ▼                 ▼
        PostgreSQL          Gmail API      Browser Extension
                                  │
                                  ▼
                           Google Pub/Sub
                                  │
                                  ▼
                         Email Processing
                                  │
                                  ▼
                       Rules + AI Classifier
                                  │
                                  ▼
                       Application Matching
                                  │
                                  ▼
                         Event Processing
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
              PostgreSQL                 Notifications
                    │
                    ▼
                Dashboard
```

## Application Event Model

Each application will maintain an event history rather than storing only the latest status.

Example:

```text
Google
Software Engineer

17 Aug 2026
APPLICATION_DETECTED

17 Aug 2026
APPLICATION_CONFIRMED

21 Aug 2026
ONLINE_ASSESSMENT

25 Aug 2026
ASSESSMENT_COMPLETED

28 Aug 2026
TECHNICAL_INTERVIEW
```

## Planned Project Structure

```text
Job-Application-Intelligence-Platform/
│
├── backend/
│
├── frontend/
│
├── browser-extension/
│
├── tests/
│
├── docs/
│
├── README.md
├── .gitignore
└── LICENSE
```

## Development Roadmap

* [ ] Design application and event database schema
* [ ] Build FastAPI backend
* [ ] Implement user authentication
* [ ] Build PostgreSQL integration
* [ ] Develop application management APIs
* [ ] Build React dashboard
* [ ] Implement Gmail OAuth
* [ ] Integrate Gmail API
* [ ] Implement Gmail event processing
* [ ] Integrate Google Cloud Pub/Sub
* [ ] Develop recruitment email classification
* [ ] Implement application-to-email matching
* [ ] Build application event timeline
* [ ] Implement browser extension
* [ ] Add notification system
* [ ] Add Docker configuration
* [ ] Write automated tests
* [ ] Deploy the application

## Current Status

The project is currently in the planning and development stage.

The initial goal is to build a working end-to-end system that can automatically detect job applications, process recruitment emails, identify hiring-stage events, update application timelines, and notify users.

## Future Improvements

Potential future improvements include:

* Additional job-portal integrations
* Improved email classification
* Better application matching
* Interview calendar integration
* Recruitment analytics
* Application follow-up reminders
* Resume-to-job matching
* Job description analysis
* Personalized interview preparation
* Recruitment process analytics

## Disclaimer

This project is intended as an educational and engineering project. Job-portal integrations will depend on the APIs, permissions, and technical capabilities made available by individual platforms.
