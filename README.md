# Campus-Flow
CampusFlow - Making campus operations more transparent, organized, and accountable.


# CampusFlow - Smart College Operations Platform

A full-stack web application for managing campus complaints, maintenance requests, student queries, and administrative workflows in one centralized platform.



## 1. Overview

CampusFlow is a centralized campus operations management platform designed to simplify communication between students, faculty, hostel representatives, and college administration.

In many colleges, students report maintenance issues, sanitation problems, infrastructure faults, and administrative concerns through informal messaging groups, emails, or paper-based systems. These fragmented processes can make it difficult to track requests, assign responsibilities, monitor resolution times, and maintain accountability.

CampusFlow addresses this problem by providing a unified digital platform where users can submit requests, administrators can assign them to the appropriate departments, and everyone can track progress through a structured workflow.

The platform aims to improve transparency, reduce manual coordination, and help campus administrators identify recurring issues through operational analytics.

## 2. Problem Statement

Traditional campus issue-management processes face several challenges:

- **Fragmented communication:** Requests are scattered across messaging groups, emails, Google forms  and verbal communication.
- **Lack of transparency:** Students may not know whether their complaints have been acknowledged or assigned.
- **Unclear accountability:** Issues can remain unresolved when responsibility is not explicitly assigned.
- **Difficult prioritization:** Urgent infrastructure or safety-related problems may be mixed with routine requests.
- **Limited analytics:** Administrators lack a centralized view of recurring problems, departmental workloads, and resolution performance.
- **Poor record keeping:** Previous requests and their resolutions may be difficult to retrieve.

CampusFlow introduces a structured workflow to address these challenges.

## 3. Project Objectives

1. Centralize campus complaints, maintenance requests, and administrative queries.
2. Provide role-based dashboards for students, staff, and administrators.
3. Enable request assignment, prioritization, and status tracking.
4. Maintain a complete history of updates and actions.
5. Provide notifications for important status changes.
6. Generate useful operational metrics and reports.
7. Build a secure, responsive, and maintainable full-stack application.

## 4. Target Users

### Students

- Submit campus-related complaints and service requests.
- Upload supporting images when necessary.
- Track request status and assigned departments.
- Add comments or clarification.
- Review their request history.

### Department Staff

- View requests assigned to their department.
- Accept responsibility for requests.
- Update progress and add resolution notes.
- Change request status according to their permissions.
- Filter requests by priority, category, and age.

### Administrators

- View campus-wide requests and operational metrics.
- Assign requests to departments and staff members.
- Manage categories, users, and department records.
- Monitor overdue and unresolved issues.
- Review audit history and export reports.

### Optional role: Department Head

A department head can review departmental workload, reassign requests, and monitor resolution performance without having unrestricted access to all administrative settings.

## 5. Core Features

### 5.1 Authentication and Authorization

- User registration and login.
- Secure password hashing.
- Role-based access control.
- Protected frontend routes and backend endpoints.
- Session expiration and logout.
- Optional college-email verification.

### 5.2 Complaint and Request Management

Users can create requests with the following information:

- Title and detailed description.
- Category, such as electrical, plumbing, sanitation, infrastructure, or IT support.
- Location, such as hostel, academic block, laboratory, or common area.
- Priority: low, medium, high, or urgent.
- Optional image attachment.
- Submission timestamp.

Each request receives a unique identifier for easy tracking.

### 5.3 Request Lifecycle

Requests follow a defined workflow:

`Submitted → Acknowledged → In Progress → Resolved → Closed`

Additional states:

- **Rejected:** The request is invalid or outside the platform's scope.
- **Reopened:** The reported issue persists after being marked resolved.

Status transitions should be validated by the backend. For example, only authorized staff should mark an assigned request as resolved, while a student may be allowed to reopen their own request under defined conditions.

### 5.4 Department Assignment

- Administrators assign requests to the relevant department.
- Requests can be assigned to individual staff members.
- Staff can view their assigned workload.
- Reassignment requires an authorized action.
- Assignment history is recorded.

### 5.5 Dashboards and Analytics

**Student dashboard**

- Total requests submitted.
- Requests awaiting action.
- Requests currently in progress.
- Recently resolved requests.
- Recent status updates.

**Staff dashboard**

- Assigned requests.
- High-priority requests.
- Overdue requests.
- Requests grouped by status.
- Recently updated issues.

**Administrator dashboard**

- Total requests and open requests.
- Resolution rate.
- Average resolution time.
- Requests grouped by department and category.
- Trends in newly submitted requests.
- Departments with the highest pending workload.

Metrics should be calculated from stored request records, with clear definitions and appropriate date ranges.

### 5.6 Search, Filtering, and Pagination

Users with appropriate permissions can filter requests by:

- Status.
- Category.
- Department.
- Priority.
- Submission date.
- Assigned staff member.

The backend should support pagination and sorting to avoid loading every record at once.

### 5.7 Notifications

Provide in-app notifications when:

- A request is assigned.
- A request's status changes.
- A staff member comments on a request.
- Additional information is required.
- A request is resolved or reopened.

Email notifications can be added as an optional extension.

### 5.8 Comments and Activity History

Each request maintains a chronological history of important events, such as:

- Request created.
- Department assigned.
- Priority changed.
- Status updated.
- Staff comment added.
- Request resolved.

The activity history helps users understand what happened and when.

### 5.9 Reports and Data Export

Administrators can export filtered request records as CSV files.

Reports can summarize:

- Requests by department.
- Requests by category.
- Average resolution time.
- Open versus resolved requests.
- Trends over a selected date range.

### 5.10 Responsive User Interface

The frontend should support desktop, tablet, and mobile screens, with:

- A sidebar or mobile navigation menu.
- Accessible forms and validation messages.
- Clear status indicators.
- Loading states and skeletons.
- Empty states when no records are available.
- Useful error messages and retry actions.

## 6. Technology Stack

| Component           | Technology                          | Purpose                              |
| ------------------- | ----------------------------------- | ------------------------------------ |
| Frontend            | Next.js, React                      | User interface and routing           |
| Language            | TypeScript                          | Type safety                          |
| Styling             | Tailwind CSS                        | Responsive UI                        |
| Data fetching       | TanStack Query                      | API requests and cache management    |
| Backend             | Python, FastAPI                     | REST API and business logic          |
| ORM                 | SQLAlchemy                          | Database access                      |
| Database migrations | Alembic                             | Version-controlled schema changes    |
| Database            | PostgreSQL                          | Persistent relational storage        |
| Authentication      | Secure session cookies              | User authentication                  |
| Testing             | Pytest, frontend testing tools      | Automated testing                    |
| API documentation   | OpenAPI / Swagger UI                | API exploration                      |
| Version control     | Git, GitHub                         | Source control and collaboration     |
| Deployment          | Vercel and a Python-compatible host | Application hosting                  |
| Containerization    | Docker                              | Reproducible development environment |

The initial version does not require Redis, a message broker, or a microservices architecture. These can be introduced if the application later needs them.

## 7. System Architecture

CampusFlow follows a frontend–backend–database architecture.

```text
                    CAMPUSFLOW
                        |
          +-------------+-------------+
          |                           |
    Next.js Frontend             FastAPI Backend
          |                           |
    Student Dashboard          Authentication
    Staff Dashboard            Authorization
    Admin Dashboard             Request Management
    Request Forms               Assignment Workflow
    Notifications                Reporting APIs
          |                           |
          +------ HTTPS / REST -------+
                                      |
                                SQLAlchemy ORM
                                      |
                                  PostgreSQL
                                      |
                           Persistent Application Data
```

### Frontend responsibilities

- Render dashboards based on the user's role.
- Validate form inputs for usability.
- Send authenticated API requests.
- Display request status, comments, and notifications.
- Manage loading, error, and empty states.

### Backend responsibilities

- Authenticate users and enforce permissions.
- Validate request creation and status transitions.
- Assign requests to departments and staff.
- Persist data and record important actions.
- Calculate dashboard metrics.
- Enforce pagination, filtering, and input validation.

### Database responsibilities

- Store users, departments, requests, comments, notifications, and audit records.
- Enforce relational integrity.
- Maintain timestamps and request history.
- Support efficient queries through appropriate indexes.

**Important design principle:** Frontend checks improve usability, but authorization must always be enforced on the backend.

## 8. Database Design

The following tables form a suitable initial schema.

### Users

| Field         | Type           | Description           |
| ------------- | -------------- | --------------------- |
| id            | UUID           | Primary key           |
| name          | VARCHAR        | Full name             |
| email         | VARCHAR        | Unique login email    |
| password_hash | VARCHAR        | Hashed password       |
| role          | VARCHAR / ENUM | Student, staff, admin |
| department_id | UUID, nullable | Associated department |
| created_at    | TIMESTAMP      | Account creation time |

### Departments

| Field       | Type      | Description            |
| ----------- | --------- | ---------------------- |
| id          | UUID      | Primary key            |
| name        | VARCHAR   | Department name        |
| description | TEXT      | Department description |
| created_at  | TIMESTAMP | Creation time          |

### Requests

| Field         | Type                | Description                    |
| ------------- | ------------------- | ------------------------------ |
| id            | UUID                | Primary key                    |
| title         | VARCHAR             | Request title                  |
| description   | TEXT                | Detailed issue                 |
| category      | VARCHAR             | Issue category                 |
| location      | VARCHAR             | Campus location                |
| priority      | VARCHAR / ENUM      | Low, medium, high, urgent      |
| status        | VARCHAR / ENUM      | Current workflow status        |
| created_by    | UUID                | User who submitted the request |
| department_id | UUID, nullable      | Assigned department            |
| assigned_to   | UUID, nullable      | Assigned staff member          |
| created_at    | TIMESTAMP           | Submission time                |
| updated_at    | TIMESTAMP           | Last update                    |
| resolved_at   | TIMESTAMP, nullable | Resolution time                |

### Comments

| Field      | Type      | Description     |
| ---------- | --------- | --------------- |
| id         | UUID      | Primary key     |
| request_id | UUID      | Related request |
| author_id  | UUID      | Comment author  |
| body       | TEXT      | Comment content |
| created_at | TIMESTAMP | Creation time   |

### Notifications

| Field      | Type                | Description          |
| ---------- | ------------------- | -------------------- |
| id         | UUID                | Primary key          |
| user_id    | UUID                | Recipient            |
| request_id | UUID, nullable      | Related request      |
| message    | TEXT                | Notification content |
| read_at    | TIMESTAMP, nullable | Read timestamp       |
| created_at | TIMESTAMP           | Creation time        |

### Request Activity

| Field      | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| id         | UUID            | Primary key                |
| request_id | UUID            | Related request            |
| actor_id   | UUID            | User performing the action |
| action     | VARCHAR         | Action type                |
| old_value  | JSONB, nullable | Previous value             |
| new_value  | JSONB, nullable | New value                  |
| created_at | TIMESTAMP       | Event timestamp            |

The database schema should also define foreign keys, indexes, constraints, and appropriate deletion rules. For example, request records and audit history should not disappear simply because a user account is deactivated.

## 9. API Design

Use a versioned REST API under `/api/v1`.

### Authentication

| Method | Endpoint                | Purpose             |
| ------ | ----------------------- | ------------------- |
| POST   | `/api/v1/auth/register` | Register an account |
| POST   | `/api/v1/auth/login`    | Authenticate        |
| POST   | `/api/v1/auth/logout`   | End session         |
| GET    | `/api/v1/auth/me`       | Get current user    |

### Requests

| Method | Endpoint                           | Purpose                    |
| ------ | ---------------------------------- | -------------------------- |
| POST   | `/api/v1/requests`                 | Create a request           |
| GET    | `/api/v1/requests`                 | List accessible requests   |
| GET    | `/api/v1/requests/{id}`            | Get request details        |
| PATCH  | `/api/v1/requests/{id}`            | Update permitted fields    |
| POST   | `/api/v1/requests/{id}/assign`     | Assign department or staff |
| POST   | `/api/v1/requests/{id}/transition` | Change request status      |
| POST   | `/api/v1/requests/{id}/comments`   | Add a comment              |
| GET    | `/api/v1/requests/{id}/activity`   | View activity history      |

### Administration and reporting

| Method | Endpoint                     | Purpose                       |
| ------ | ---------------------------- | ----------------------------- |
| GET    | `/api/v1/departments`        | List departments              |
| POST   | `/api/v1/departments`        | Create a department           |
| GET    | `/api/v1/dashboard/summary`  | Retrieve dashboard metrics    |
| GET    | `/api/v1/reports/requests`   | Generate filtered report data |
| GET    | `/api/v1/notifications`      | List user notifications       |
| PATCH  | `/api/v1/notifications/{id}` | Mark a notification as read   |

All endpoints must enforce authentication and resource-level authorization where applicable. Administrative endpoints must be restricted to authorized administrators.

## 10. Security Considerations

Security is a core requirement, not an optional enhancement.

- Hash passwords using a suitable password-hashing algorithm such as Argon2id.
- Use HTTPS in production and secure, HttpOnly session cookies.
- Apply CSRF protection when using cookie-based authentication.
- Validate and constrain request fields on the backend.
- Enforce role and ownership checks on every protected resource.
- Restrict uploaded file types and sizes; store files outside executable paths.
- Keep secrets and database credentials in environment variables.
- Never commit `.env` files or real user information.
- Use rate limiting on authentication endpoints.
- Record sensitive administrative actions in an audit trail.
- Avoid exposing private student details in dashboard analytics.
- Use synthetic data for public demos unless real users have explicitly consented.

## 11. Suggested Project Structure

```text
campusflow/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── app/
│   │   │   ├── login/
│   │   │   ├── dashboard/
│   │   │   ├── requests/
│   │   │   └── admin/
│   │   ├── components/
│   │   ├── features/
│   │   ├── hooks/
│   │   ├── lib/
│   │   └── types/
│   ├── package.json
│   └── .env.example
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   └── v1/
│   │   ├── core/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── repositories/
│   │   ├── db/
│   │   └── main.py
│   ├── tests/
│   ├── alembic/
│   ├── requirements.txt
│   └── .env.example
├── docs/
│   ├── architecture.md
│   └── api.md
├── docker-compose.yml
├── .gitignore
├── LICENSE
└── README.md
```

This is a suggested structure; folders can be added as the implementation grows.

## 12. Local Setup

### Prerequisites

- Git
- Node.js and npm
- Python 3.11 or a compatible supported version
- PostgreSQL, or Docker with Docker Compose

### Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/campusflow.git
cd campusflow
```

### Configure the backend

```bash
cd backend
python -m venv .venv
```

Activate the virtual environment.

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Create your local environment file using `.env.example` as a template. Configure the database URL, session secret, and other required settings.

Run database migrations after they have been implemented:

```bash
alembic upgrade head
```

Start the development server:

```bash
uvicorn app.main:app --reload
```

The API documentation should be available at:

`http://localhost:8000/docs`

### Configure the frontend

Open a second terminal:

```bash
cd frontend
npm install
```

Create a local `.env.local` file containing the backend API base URL, for example:

```text
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000/api/v1
```

Configure cookie credentials, CORS, and the API origin consistently with your local development setup.

Start the frontend:

```bash
npm run dev
```

Open `http://localhost:3000` in your browser.

**Note:** These instructions describe the intended setup. The application, dependencies, environment variables, migrations, and scripts must be implemented before the repository will run successfully.

## 13. Testing Strategy

The project should include tests for both normal workflows and failure scenarios.

### Backend tests

- Registration, login, and logout.
- Unauthorized requests.
- Students accessing only their own requests.
- Staff accessing requests within their permitted scope.
- Admin-only department assignment.
- Valid and invalid status transitions.
- Pagination and filters.
- Notification creation and authorization.
- Database constraints and error handling.

### Frontend tests

- Form validation and submission.
- Role-specific navigation.
- Request list filtering.
- Loading, empty, and error states.
- Status updates and confirmation messages.

### Integration tests

- Student submits a request.
- Administrator assigns a department.
- Staff updates the request.
- Student sees the new status and notification.
- Request is resolved and appears in reports.

Use isolated test data and a separate test database.

## 14. Development Roadmap

### Phase 1 — Core MVP

- [ ] Set up frontend and backend.
- [ ] Create the database schema and migrations.
- [ ] Implement registration and authentication.
- [ ] Build request creation and listing.
- [ ] Implement request details and status tracking.
- [ ] Add role-based authorization.

### Phase 2 — Operational workflows

- [ ] Create department and staff management.
- [ ] Implement assignment and reassignment.
- [ ] Add comments and activity history.
- [ ] Implement notifications.
- [ ] Build role-specific dashboards.

### Phase 3 — Quality and reporting

- [ ] Add search, filtering, and pagination.
- [ ] Add dashboard analytics and CSV export.
- [ ] Write automated tests.
- [ ] Improve accessibility and mobile responsiveness.
- [ ] Add Docker-based local development.
- [ ] Deploy frontend and backend.
- [ ] Document API endpoints and system architecture.

### Future enhancements

- Email notifications and scheduled reminders.
- Duplicate issue detection.
- Map-based campus issue visualization.
- Service-level targets for request resolution.
- More advanced analytics and workload forecasting.
- Optional single sign-on for college accounts.

## 15. Expected Learning Outcomes

Building CampusFlow provides hands-on experience with:

- Component-based frontend development.
- Type-safe API integration.
- REST API design and documentation.
- Authentication and role-based authorization.
- Relational database modeling and migrations.
- Workflow state management.
- Transactions and data integrity.
- Automated testing and debugging.
- Application deployment and environment configuration.
- Security, maintainability, and software architecture.

## 16. Project Scope

The initial version focuses on request submission, department assignment, status tracking, authentication, and basic dashboards.

Advanced analytics, external email integrations, map visualization, and automated duplicate detection are optional enhancements rather than prerequisites for the MVP.

The project is intended to be extensible: new departments, categories, roles, and workflows should be configurable wherever practical instead of requiring changes throughout the codebase.

## 17. License

This project is intended to be released under the MIT License. Add a `LICENSE` file to the repository before claiming that the repository is licensed under MIT.

---

