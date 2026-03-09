# Flask on Docker

[![Development Build](https://github.com/0marJim/flask-on-docker/actions/workflows/dev.yml/badge.svg)](https://github.com/0marJim/flask-on-docker/actions)

## Overview
This repository contains a production-ready, containerized web application built with Flask, PostgreSQL, Gunicorn, and Nginx. The multi-container architecture separates the database, the application server, and the reverse proxy into distinct Docker services. It features secure environment variable injection, robust static and media file routing directly through Nginx via shared Docker volumes, and automated development build testing via GitHub Actions.

## Demo
![Media Upload Demo](demo.gif)

## Build Instructions

### Prerequisites
* Docker and Docker Compose installed on your machine.

### Development Environment
To spin up the development environment (using Flask's built-in server):

1. Build and start the containers in the background:
   \`\`\`bash
   docker-compose up -d --build
   \`\`\`
2. Initialize and seed the database:
   \`\`\`bash
   docker-compose exec web python manage.py create_db
   docker-compose exec web python manage.py seed_db
   \`\`\`
3. The application will be available at `http://localhost:5001`.

### Production Environment
To spin up the production environment (using Gunicorn and Nginx):

1. Ensure you have created your `.env.prod.db` file with the required PostgreSQL credentials (not included in this repository for security).
2. Build and start the production cluster:
   \`\`\`bash
   docker-compose -f docker-compose.prod.yml up -d --build
   \`\`\`
3. Initialize the production database:
   \`\`\`bash
   docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
   \`\`\`
4. The application and media upload endpoint will be securely served via Nginx at `http://localhost:1338`.
