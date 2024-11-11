# Next News

![Next News Logo](https://github.com/Aliio-Inc/strapi-next-news/blob/main/assets/logo.png?raw=true)

Next News is an open-source, modern news portal built with **Strapi**, **Next.js 14**, and **Shadcn**. It provides a scalable and customizable platform for publishing and managing news articles, ensuring a seamless experience for both content creators and readers.

## Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Technologies](#technologies)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Architecture](#architecture)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## Features

- **Headless CMS**: Powered by Strapi for flexible content management.
- **Server-Side Rendering**: Utilizes Next.js 14 for optimal performance and SEO.
- **UI Components**: Styled with Shadcn for a sleek and responsive design.
- **Real-Time Updates**: Live previews and updates for seamless content editing.
- **Authentication**: Secure user authentication and role-based access control.
- **SEO Optimization**: Built-in SEO best practices to enhance visibility.
- **Customizable**: Easily extendable and customizable to fit various needs.
- **Responsive Design**: Mobile-friendly layouts for all devices.
- **Internationalization**: Support for multiple languages.

## Demo

Check out the live demo of Next News [here](https://next-news.vercel.app).

## Technologies

- **Frontend**:
  - [Next.js 14](https://nextjs.org/)
  - [Shadcn](https://shadcn.com/)
  - [React](https://reactjs.org/)
  - [TypeScript](https://www.typescriptlang.org/)
- **Backend**:
  - [Strapi](https://strapi.io/)
  - [Node.js](https://nodejs.org/)
- **Database**:
  - [PostgreSQL](https://www.postgresql.org/) / [MongoDB](https://www.mongodb.com/) _(choose based on your preference)_
- **Deployment**:
  - [Vercel](https://vercel.com/)
  - [Heroku](https://www.heroku.com/)
- **Others**:
  - [Docker](https://www.docker.com/) _(optional)_
  - [GitHub Actions](https://github.com/features/actions) for CI/CD

## Installation

### Prerequisites

- **Node.js** (v14 or later)
- **npm** or **yarn**
- **Git**
- **Strapi** account _(optional for deployment)_

### Clone the Repository

```bash
git clone https://github.com/Aliio-Inc/strapi-next-news.git
cd strapi-next-news
```

### Install Dependencies

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

### Setup Environment Variables

Create a `.env` file in both the `frontend` and `backend` directories based on the provided `.env.example` files.

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

### Run the Application

#### Start the Backend (Strapi)

```bash
cd backend
npm run develop
# or
yarn develop
```

Strapi will be available at `http://localhost:1337`.

#### Start the Frontend (Next.js)

```bash
cd frontend
npm run dev
# or
yarn dev
```

Next.js will be available at `http://localhost:3000`.

## Configuration

### Strapi Configuration

- **Content Types**: Manage your content types via the Strapi admin panel.
- **Plugins**: Configure plugins such as Authentication, Email, etc.
- **Roles & Permissions**: Set up user roles and permissions for content access.

### Next.js Configuration

- **Pages & Components**: Customize the pages and components located in the `pages` and `components` directories.
- **API Routes**: Extend or modify API routes as needed.
- **Styling**: Adjust styles using Shadcn or integrate other styling libraries.

## Usage

- **Creating Content**: Use the Strapi admin panel to create and manage news articles.
- **Navigating the Site**: Browse the latest news, categories, and search for specific topics.
- **User Authentication**: Register and log in to access personalized features.

## Architecture

Next News follows a **Headless CMS** architecture, separating the frontend and backend for greater flexibility and scalability.

- **Frontend**: Built with Next.js 14, leveraging server-side rendering and static site generation for performance.
- **Backend**: Powered by Strapi, providing a robust and customizable API for content management.
- **Styling**: Utilizes Shadcn for consistent and responsive UI components.

### Directory Structure

```
/Next-News
│
├── frontend
│   ├── components
│   ├── pages
│   ├── public
│   ├── styles
│   └── ...
│
├── backend
│   ├── api
│   ├── config
│   ├── extensions
│   └── ...
│
├── docs
│   └── ...
│
├── .github
│   └── ...
│
├── README.md
└── ...
```

## API Documentation

Comprehensive API documentation is available in the [API Documentation](./docs/API_Documentation.md) file. It covers all available endpoints, request/response structures, and authentication methods.

## Deployment

Next News can be deployed using various platforms. Below are the general steps for deploying both the frontend and backend.

### Deploying the Backend (Strapi)

1. **Choose a Hosting Provider**: Options include Heroku, DigitalOcean, AWS, etc.
2. **Configure Environment Variables**: Ensure all necessary environment variables are set.
3. **Database Setup**: Use a managed database service or set up your own.
4. **Deploy**: Follow the provider-specific instructions to deploy the Strapi backend.

### Deploying the Frontend (Next.js)

1. **Choose a Hosting Provider**: Vercel is recommended for Next.js applications.
2. **Connect Repository**: Link your GitHub repository to the hosting provider.
3. **Configure Environment Variables**: Set the `NEXT_PUBLIC_API_URL` and any other required variables.
4. **Deploy**: Follow the provider-specific instructions to deploy the frontend.

For detailed deployment instructions, refer to the [Deployment Guide](./docs/Deployment_Guide.md).

## Contributing

Contributions are welcome! Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) file for guidelines on how to contribute to this project.

### Steps to Contribute

1. **Fork the Repository**
2. **Create a New Branch**
3. **Make Your Changes**
4. **Submit a Pull Request**

## License

This project is licensed under the [MIT License](./LICENSE.md). See the [LICENSE.md](./LICENSE.md) file for details.

## Contact

- **Author**: Atiq Israk
- **Email**: [atiq.israk@example.com](mailto:atiq.israk@example.com)
- **GitHub**: [Aliio-Inc](https://github.com/Aliio-Inc)

## Acknowledgements

- [Strapi](https://strapi.io/)
- [Next.js](https://nextjs.org/)
- [Shadcn](https://shadcn.com/)
- [Open Source Community](https://github.com/Aliio-Inc/strapi-next-news)

---

Thank you for checking out Next News! If you have any questions or feedback, feel free to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out directly.
