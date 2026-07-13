# Ring så Tränar Vi
AI-driven, call like training app for older adults (60+) and inactive individuals to safely start and maintain physical activity through simple, voice-guided workouts.

## Project Overview
A beginner-friendly fitness app designed for seniors and inactive users, offering simple workouts, voice guidance, and personalized support.
**Focus:** safety, simplicity, and confidence, like a guided phone call.

[PLACEHOLDER for some 3-5 screenshots]

## Demo

- Frontend: <frontend deployment URL [PLACEHOLDER]>
- Backend: <backend deployment URL [PLACEHOLDER]> (if public)

## Architecture Diagram
- Frontend handles UI, AI interaction, and authentication.
- Backend manages logic, data, and validation.
- Data is stored in a relational database, with media (audio/images) in object storage.
- Deployment [placeholder]

## Core Features
- Works without login (limited functionality)
- Authentication via Clerk (JWT)
- Admin role with extended access
- User profiles (name, context (notes), trainer, language, intensity)
- Multi-language support
- AI-guided workouts via Gemini
- Basic error handling

## AI Flow
Frontend → Gemini → function call → Backend → response → Gemini → User

## Data
- Database (Railway): Users, workouts, trainers, feedback
- Storage (Supabase): Audio + image assets (linked in DB)
## Components
- Frontend: UI, AI interaction, auth client
- Backend: API, business logic, JWT validation
- Database: Structured user + workout data
- Storage: Media assets
- External Services: Gemini (AI), Clerk (Auth)

## Repository Structure

- Frontend – User interface and client-side logic  
  <frontend repository link>

- Backend – API and business logic  
  <backend repository link>

- Infrastructure – Deployment and configuration  
  <infrastructure repository link>


