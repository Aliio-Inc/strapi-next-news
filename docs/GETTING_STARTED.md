# Getting Started with Next News

Welcome to **Next News**! This guide will help you set up the project locally, understand its structure, and get you up and running quickly.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Development Server](#running-the-development-server)
- [Project Structure](#project-structure)
- [Basic Usage](#basic-usage)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- **Node.js** (v14 or later): [Download Node.js](https://nodejs.org/)
- **npm** or **Yarn**: Comes with Node.js, but you can install Yarn separately if preferred.
- **Git**: [Download Git](https://git-scm.com/downloads)
- **Database**: PostgreSQL or MongoDB, depending on your preference.
- **Strapi Account** _(optional for deployment)_: [Sign Up for Strapi](https://strapi.io/)

## Installation

### 1. Clone the Repository

Begin by cloning the Next News repository to your local machine:

```bash
git clone https://github.com/Aliio-Inc/strapi-next-news.git
cd strapi-next-news
```

### 2. Install Dependencies

Next News consists of two main parts: the **frontend** (built with Next.js) and the **backend** (powered by Strapi). Install dependencies for both.

#### Frontend

```bash
cd frontend
npm install
# or
yarn install
```

#### Backend

```bash
cd ../backend
npm install
# or
yarn install
```

### 3. Configure Environment Variables

Environment variables are essential for configuring your application. Create `.env` files in both the `frontend` and `backend` directories based on the provided `.env.example` files.

#### Frontend (`frontend/.env`)

```env
NEXT_PUBLIC_API_URL=http://localhost:1337
# Add other frontend-specific environment variables here
```

#### Backend (`backend/.env`)

```env
DATABASE_URL=postgres://user:password@localhost:5432/next_news
# Add other backend-specific environment variables here
```

**Note:** Replace `user`, `password`, and other placeholders with your actual database credentials.

### 4. Set Up the Database

Ensure your chosen database (PostgreSQL or MongoDB) is installed and running. Create a new database for Next News.

#### PostgreSQL Example

```bash
# Access PostgreSQL prompt
psql -U your_username

# Create a new database
CREATE DATABASE next_news;

# Exit the prompt
\q
```

### 5. Initialize Strapi Backend

Navigate to the backend directory and start the Strapi development server:

```bash
cd backend
npm run develop
# or
yarn develop
```

Strapi will be available at [http://localhost:1337](http://localhost:1337). Access the Strapi admin panel to manage content types, users, and settings.

### 6. Start the Next.js Frontend

In a new terminal window, navigate to the frontend directory and start the Next.js development server:

```bash
cd frontend
npm run dev
# or
yarn dev
```

The Next.js application will be available at [http://localhost:3000](http://localhost:3000).

## Project Structure

Understanding the project structure will help you navigate and contribute effectively.

```
/Next-News
│
├── frontend
│   ├── components        # Reusable React components
│   ├── pages             # Next.js pages
│   ├── public            # Static assets
│   ├── styles            # CSS and styling files
│   ├── utils             # Utility functions
│   └── ...               # Other frontend-specific directories
│
├── backend
│   ├── api               # Strapi API endpoints
│   ├── config            # Configuration files
│   ├── extensions        # Strapi extensions and customizations
│   ├── public            # Public assets for Strapi
│   └── ...               # Other backend-specific directories
│
├── docs
│   ├── Getting_Started.md
│   ├── Installation.md
│   ├── Configuration.md
│   ├── Usage.md
│   ├── Architecture.md
│   ├── API_Documentation.md
│   ├── Deployment_Guide.md
│   ├── FAQ.md
│   ├── Best_Practices.md
│   └── Changelog.md
│
├── .github
│   ├── ISSUE_TEMPLATE.md
│   └── PULL_REQUEST_TEMPLATE.md
│
├── LICENSE.md
├── README.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── CHANGELOG.md
```

## Basic Usage

### Creating Content

1. **Access Strapi Admin Panel**: Navigate to [http://localhost:1337/admin](http://localhost:1337/admin) and log in.
2. **Create Content Types**: Define your content structures such as Articles, Categories, Authors, etc.
3. **Add Content**: Start adding news articles, categories, and other relevant content.

### Navigating the Frontend

- **Home Page**: Displays the latest news articles.
- **Categories**: Browse articles by category.
- **Search**: Use the search functionality to find specific articles.
- **User Authentication**: Register and log in to access personalized features.

## Troubleshooting

### Common Issues

- **Backend Not Starting**:

  - Ensure the database is running and the `DATABASE_URL` in `backend/.env` is correct.
  - Check for missing dependencies and reinstall if necessary.

- **Frontend Not Connecting to Backend**:

  - Verify that `NEXT_PUBLIC_API_URL` in `frontend/.env` points to the correct Strapi backend URL.
  - Ensure the Strapi server is running.

- **CORS Errors**:
  - Configure CORS settings in Strapi to allow requests from your frontend URL.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue**: Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page.
- **Join the Community**: Participate in discussions and seek help from other contributors.

## Next Steps

Once you have the project up and running, consider exploring the following:

- **Customization**: Modify the frontend design using Shadcn or add new features.
- **API Integration**: Extend or customize Strapi APIs to fit your needs.
- **Deployment**: Deploy the application to a hosting provider like Vercel for the frontend and Heroku or DigitalOcean for the backend.
- **Contributing**: Read the [CONTRIBUTING.md](./CONTRIBUTING.md) to learn how to contribute to the project.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Provides a clear starting point for new users, explaining what the guide covers.
- **Prerequisites**: Lists all necessary tools and accounts needed before installation.
- **Installation Steps**: Detailed instructions on how to clone the repository, install dependencies, configure environment variables, set up the database, and start both frontend and backend servers.
- **Project Structure**: An overview of the directory layout to help users navigate the project.
- **Basic Usage**: Guides users on how to create content and navigate the application.
- **Troubleshooting**: Addresses common issues and provides solutions.
- **Next Steps**: Encourages users to further customize, extend, deploy, or contribute to the project.
- **Footer**: Includes project information and contact details for further assistance.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
