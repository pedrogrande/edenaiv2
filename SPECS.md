# SPECS.md

## Overview

This document outlines the specifications for the AI Agent application, detailing its features, user stories, and acceptance criteria.

## Features

- Pre-built agent roster
- Agent creation, editing, and deletion
- Chat interface with conversation history
- User authentication and session management
- Integration with external APIs and services

## Architecture

- Backend: RESTful API using FastAPI
- Frontend:
- Database: PostgreSQL for persistent storage
- AI Models: Integration with OpenAI and other LLM providers

## User stories

### Core (Onboarding & Basic Use)

- As a beginner, I want to see a roster of pre-built agents so that I can try out a useful agent without any setup. [core, discovery]
- As a user, I want to see an agent and its configuration so that I can understand what it does and how to use it. [core, UX]
- As a user, I want to be able to create and edit agents with a simple form interface so I don't need to understand the code. [core, CRUD]
- As a user, I want to create, edit, and delete my own agents so that I can reuse and share my custom agents. [core, CRUD]
- As a user, I want to give my agent a name, purpose and simple instructions in plain English so that I can easily define its purpose. [core, UX]
- As a user, I want to select an LLM provider and model for my agent so that I can customize its capabilities. [core, configuration]
- As a user, I want to configure my agent's tools and plugins so that it can perform specific tasks. [core, configuration]
- As a user, I want to set my agent's behavior and personality so that it aligns with my needs. [core, configuration]
- As a user I want to be greeted by the system's "concierge" agent so that I can receive guidance and assistance in creating my own agents. [core, UX]
- As a user, I want to collaborate with my agent in a simple interface so that I can get immediate answers and results. [core, chat]
- As a user, I want my conversation history to be saved so that I can continue my work later without losing context. [core, persistence]

#### Acceptance criteria (Core)

- roster of pre-built agents
  - The UI exposes an "Agents" roster with at least 5 agent cards with name, short description, tags, and a "Collaborate" button.
  - An API endpoint returns agent roster and pagination metadata.

- Create / Edit / Delete agents
  - The API provides POST /v1/agents, GET /v1/agents/{id}, PATCH /v1/agents/{id}, DELETE /v1/agents/{id}.
  - Successful creation returns 201 and the new agent's ID; updates return 200 with the modified resource.
  - The DB contains the new/updated record and the UI reflects changes within one refresh.

- Collaboration History
  - The UI supports a chat view for an agent and stores messages in a session tied to the agent and user.
  - Collaboration history is retrievable via GET /v1/agents/{id}/sessions and GET /v1/sessions/{session_id}.
  - Users can delete a session; deletion removes the session and its messages from the primary store.

- Name & Simple Instruction
  - Creating an agent requires a non-empty name (max 255 chars) and a short instruction field; server returns 422 for invalid input.
