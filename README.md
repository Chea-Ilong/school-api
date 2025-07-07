# School Management API

This is a RESTful API built using **Express.js**, **Sequelize ORM**, and **MySQL** to manage Students, Courses, and Teachers. It includes full CRUD operations, **JWT-based authentication**, Swagger API documentation, and a Faker-based database seeder.

---

## 📦 Features

- 🔐 **JWT Authentication** with user registration and login
- 🛡️ **Protected Routes** requiring authentication
- 🧑‍🎓 CRUD for Students (protected)
- 🧑‍🏫 CRUD for Teachers (protected)
- 📘 CRUD for Courses (protected)
- 🔁 Associations:
  - One Teacher teaches many Courses
  - Many Students enroll in many Courses (Many-to-Many)
- 📚 Swagger documentation (`/docs`) with JWT security
- 🧪 Faker.js seeder for generating test data
- 🔒 Password hashing with bcryptjs
- ⏰ Token expiration management

---

## 🚀 Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/KimangKhenng/school-api.git
cd school-api
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure `.env`

Create a `.env` file in the root:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=yourpassword
DB_NAME=school_db
DB_PORT=3306
PORT=3000
JWT_SECRET=your_super_secret_jwt_key_here_change_in_production
```

### 4. Run the Server

```bash
npm run dev
```

Visit: [http://localhost:3000/docs](http://localhost:3000/api-docs)

---

## 📂 Project Structure

```
.
├── index.js
├── config
│   └── swagger.js
├── controllers
│   ├── student.controller.js
│   ├── teacher.controller.js
│   └── course.controller.js
├── models
│   └── index.js
├── routes
│   ├── student.routes.js
│   ├── teacher.routes.js
│   └── course.routes.js
├── seed.js
└── .env
```

---

## 🧪 Seeding Fake Data

To populate the database with fake students, courses, and teachers using Faker.js:

```bash
npm run seed
```

This will:
- Recreate all tables
- Insert 5 teachers, 10 courses, and 20 students
- Enroll students in random courses

---

## 📘 API Documentation

Swagger UI is available at:

```
http://localhost:3000/docs
```

It includes all CRUD endpoints for:

- `/students`
- `/teachers`
- `/courses`

---

## ⚙️ Scripts

| Script        | Description            |
|---------------|------------------------|
| `npm start`   | Start the server       |
| `node seed.js`| Seed database with Faker.js |

---

## 🧑‍💻 Technologies Used

- Express.js
- Sequelize ORM
- MySQL
- Swagger (swagger-jsdoc + swagger-ui-express)
- Faker.js
- dotenv

---

## 📄 License

MIT

---

## 🔐 Authentication

The API now includes JWT-based authentication with the following endpoints:

### Public Endpoints (No Authentication Required)
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login and receive JWT token

### Protected Endpoints (JWT Authentication Required)
- `GET /auth/profile` - Get current user profile
- All student, course, and teacher CRUD operations

### Usage Examples

#### Register a User
```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john.doe@example.com",
    "password": "password123"
  }'
```

#### Login
```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john.doe@example.com",
    "password": "password123"
  }'
```

#### Access Protected Routes
```bash
curl http://localhost:3000/students \
  -H "Authorization: Bearer YOUR_JWT_TOKEN_HERE"
```