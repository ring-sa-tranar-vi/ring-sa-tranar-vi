# Ring så Tränar Vi
Ring så tränar vi is a beginner -friendly fitness app designed for seniors and inactive users, offering simple workouts, voice guidance, and personalized support.

AI-driven, call like training app for older adults (60+) and inactive individuals to safely start and maintain physical activity through simple, voice-guided workouts.

**Focus:** safety, simplicity, and confidence, like a guided phone call.

## Project Overview

<img width="300" alt="homepage" src="https://github.com/user-attachments/assets/67396f8d-8540-48d9-9675-4cc5bd213594" />

<img width="300"  alt="choose trainer" src="https://github.com/user-attachments/assets/d8c743f9-d845-42cf-ba5d-36a71226819a" />

<img width="300" alt="events and organisations" src="https://github.com/user-attachments/assets/dc733fa3-99bb-494c-affb-3e9dfc29ed75" />


The system consists of three separate repositories that together make up the application:

1. **Frontend** — React application providing the user interface, AI trainer sessions, company portal, and admin functionality.
  
2. **Backend** — Spring Boot application providing the REST API, business logic, data access, authentication, and integrations with external services.
  
3. **App **— React Native application providing the mobile user interface and access to the core training and AI-guided workout functionality.
  
4. **Infrastructure** — Infrastructure-as-code and deployment configuration for the application's environments and cloud resources.
  

The frontend communicates with the backend through a REST API. Authentication is handled through **Clerk**, while the infrastructure repository manages the resources and configuration required to run the system.

Key Features

- **Guest access** — The application can be used without logging in, with limited functionality.
- **Authentication** — User authentication is handled through Clerk using JWTs.
- **Admin access** — Administrators have access to extended functionality.
- **User profiles** — Profiles include name, context/notes, trainer, language, and workout intensity.
- **Multi-language support** — The application supports multiple languages.
- **AI-guided workouts** — Workouts are generated and guided using Gemini.
- **Error handling** — Basic error handling is implemented across the application.

### Repositories

| Repository | Responsibility | Main Technologies |
| --- | --- | --- |
| [**Frontend**](https://github.com/ring-sa-tranar-vi/frontend) | User interface and client-side application | React, TypeScript, Vite |
| [**Backend**](https://github.com/ring-sa-tranar-vi/backend) | REST API, business logic, authentication, and integrations | Java 21, Spring Boot, Gradle |
| [**App**](https://github.com/ring-sa-tranar-vi/app) | User interface and client-side native application | React Native, Expo |
| [**Infrastructure**](https://github.com/ring-sa-tranar-vi/infrastructure) | Cloud infrastructure and environment configuration | Infrastructure as Code |

See each repository's README for detailed documentation.

## Demo

Frontend:

- [Production](https://prod-ringsatranarvi-app.web.app/)
  
- [Staging](https://staging-ringsatranarvi-app.web.app)
  

Backend:

- [Production](https://prod-backend-service-49973934534.europe-west3.run.app/)
  
- [Staging](https://staging-backend-service-49973934534.europe-west3.run.app)

Getting Started

The recommended orde to getting started is:

1. Read this README to understand the overall system.
2. Clone the repositories relevant to your work.
3. Read the README in the repository you will be working on.
4. Configure the required environment variables.
5. Start the backend if working on functionality that requires API access.
6. Start the frontend.
7. Follow the repository-specific development and testing workflows.


## Architecture Diagram
- Frontend handles UI, AI interaction, and authentication.
- Backend manages logic, data, and validation.
- Data is stored in a relational database, with media (audio/images) in object storage.
- The infrastructure repository is responsible for the underlying infrastructure and environment configuration.

<img width="800" alt="ring så tränar vi architecture" src="https://github.com/user-attachments/assets/42ce4e3b-a6e1-4529-9483-a61bd7ea8ec6" />


### Userflow chart

The userflow below illustrates the main journey through the application, from the initial interaction to the different available paths and outcomes. It provides an overview of how users move between the different screens and actions.

<img width="800" height="1123" alt="Ring så tränar vi Userflow" src="https://github.com/user-attachments/assets/e23790b6-7896-48d0-b69b-e0642d3a6f77" />

## Components & External Services

- **Frontend** — Provides the user interface, handles AI interactions, and manages the client-side authentication flow.
  
- **Backend** — Provides the REST API, handles business logic and data access, and validates authentication tokens.
  
- **Database** — Stores structured application data, including users, workouts, trainers, and feedback.
  
- **Storage** — Stores media assets, including audio and images.
  
- **External Services** — **Gemini** provides AI functionality, while **Clerk** handles authentication.
  

## Authentication

Authentication is handled through **Clerk**.

The general authentication flow is:

```
User  
  ↓
Clerk  
  ↓
Authenticated session
  ↓
Clerk JWT  
  ↓
Frontend 
  ↓
Backend API  
  ↓
Authorization
```

The frontend obtains the user's authentication token from Clerk and includes it when communicating with protected backend endpoints. The backend validates the token and determines what the authenticated user is authorized to do.

## AI Flow

The AI-guided workout flow is handled through an interaction between the frontend, Gemini, and the backend.

```
User
  ↓
Frontend
  ↓
Gemini
  ↓
Function call
  ↓
Backend
  ↓
Response
  ↓
Gemini
  ↓
Frontend
  ↓
User
```

- **User interaction** — The user interacts with the AI trainer through the frontend, for example by starting a workout or responding to the trainer.
- **Frontend → Gemini** — The frontend sends the user's input and relevant context to Gemini, which determines how the AI trainer should respond.
- **Gemini → Backend (function call)** — When the AI needs information or an action from the application, Gemini triggers a predefined function call. The request is sent to the backend rather than allowing the AI to access application data directly.
- **Backend processing** — The backend validates the request, applies business logic, and retrieves or updates the required data.
- **Backend → Gemini** — The backend returns the result of the requested operation to Gemini.
- **Gemini → User** — Gemini uses the backend response together with the conversation context to generate the next response for the user. The frontend then presents the response through the application's AI/voice interface.

Frontend → Gemini → function call → Backend → response → Gemini → User

## Data & Storage

The application separates **structured application data** from **media assets**. The database stores the information needed to manage users and workouts, while media files such as audio and images are stored separately.

```text
Frontend
   ↓
Backend
   ↓
Database ──────────→ Structured application data
   │
   └───────────────→ Media references
                         ↓
                     Storage
                         ↓
                  Audio + images
```

- **Database (Neon)** — Stores structured application data, including users, workouts, trainers, and feedback.
- **Media Storage (Google cloud storage)** — Stores media assets such as audio files and images.
- **Database references** — Media files are not stored directly in the database. Instead, relevant media information or references are stored in the database, allowing the application to retrieve the corresponding assets from Supabase.
- **Backend access** — The backend acts as the main layer for accessing and managing application data, keeping database and storage operations separate from the frontend.

## Environments

The system is deployed to separate environments to support development, testing, and production.

At a high level:

```
Development
    │
    ▼
Staging
    │
    ▼
Production
```

Staging
- Frontend: https://staging-ringsatranarvi-app.web.app
- Backend: https://staging-backend-service-49973934534.europe-west3.run.app

Production
- Frontend: https://prod-ringsatranarvi-app.web.app/
- Backend: https://prod-backend-service-49973934534.europe-west3.run.app/

Environment-specific configuration, infrastructure, and deployment processes are managed through the infrastructure and application repositories.

Environment-specific configuration, infrastructure, and deployment processes are managed through the infrastructure and application repositories.

## Monitioring & Observability

**Grafana** is used to monitor the application's infrastructure and services. It provides dashboards for visualizing metrics, logs, and system health in one place.

Grafana helps the team:

- Monitor application and infrastructure performance.
- Detect errors and unusual behavior.
- Track service health and availability.
- Investigate issues and troubleshoot problems.
- Get an overview of the system across different environments.

Grafana is primarily a **monitoring and observability tool**. It does not handle application logic or user data; instead, it helps the development team understand how the system is running and identify problems early.

## Development Workflow

The project uses **Trunk-Based Development**.

Changes are developed in short-lived branches and merged into the relevant repository's `main` branch through pull requests.

Depending on the change, a feature may require changes in one or more repositories.

For example:

```
Frontend change
    ↓
Frontend repository
    ↓
Pull Request
    ↓
CI
    ↓
Merge to main
```

Changes affecting multiple parts of the system may require coordinated pull requests across the frontend, backend, and infrastructure repositories.

## CI/CD

Each application repository has its own CI/CD workflow.

At a high level:

```
Frontend Repository ──┐
                      ├──► CI/CD ──► Environments
Backend Repository ───┤
                      │
Infrastructure ───────┘
```

The frontend is deployed to Firebase Hosting, while the backend and infrastructure are deployed according to their respective repository workflows.

See the individual repository READMEs for detailed deployment information.

## Documentation

Detailed technical documentation is maintained in each repository:

- **[Frontend]()** — Application architecture, features, routing, state management, testing, deployment, and troubleshooting.
- **[Backend]()** — API, authentication, database, business logic, integrations, testing, and troubleshooting.
- [**App**]() — Native mobile application for phones, providing the mobile user interface and access to the app's core functionality
- **[Infrastructure]()** — Infrastructure configuration, environments, cloud resources, and deployment.

## Known Limitations

- The app currently depends on the available exercise/workout data.
  
- Workout recommendations are not yet fully personalized.
  
- The app may not yet support every type of training or workout style.
  
- You can only cancel a call scheduled within 4 weeks from now.
  
- You need to manually assign admin roles to users.
  
- We can only login with Google or Facebook account
  

## Future Roadmap

- Add more exercises and workout variations
  
- Improve personalized workout recommendations
  
- Add user profiles and training goals
  
- Add workout history
  
- Add reminders and notifications
  
- Improve exercise instructions and demonstrations
  
- Add more training categories
  
- Improve UI/UX based on user feedback
  
- Add super admin and they can manage admins as well
