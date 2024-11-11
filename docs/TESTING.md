# Testing Guide for Next News

Ensuring the reliability and quality of **Next News** is paramount. This guide outlines the testing strategies, tools, and best practices for both the frontend and backend of the Next News project. By following these guidelines, you can maintain a robust and error-free application.

## Table of Contents

- [Introduction](#introduction)
- [Testing Strategy](#testing-strategy)
  - [Types of Testing](#types-of-testing)
    - [Unit Testing](#unit-testing)
    - [Integration Testing](#integration-testing)
    - [End-to-End (E2E) Testing](#end-to-end-e2e-testing)
    - [Performance Testing](#performance-testing)
    - [Security Testing](#security-testing)
- [Frontend Testing](#frontend-testing)
  - [Tools](#tools)
    - [Jest](#jest)
    - [React Testing Library](#react-testing-library)
    - [Cypress](#cypress)
  - [Setup](#setup)
    - [Installing Dependencies](#installing-dependencies)
    - [Configuring Jest](#configuring-jest)
  - [Writing Tests](#writing-tests)
    - [Unit Tests](#unit-tests)
    - [Integration Tests](#integration-tests)
    - [End-to-End Tests](#end-to-end-tests)
  - [Best Practices](#best-practices)
- [Backend Testing](#backend-testing)
  - [Tools](#tools-1)
    - [Jest](#jest-1)
    - [Supertest](#supertest)
  - [Setup](#setup-1)
    - [Installing Dependencies](#installing-dependencies-1)
    - [Configuring Jest](#configuring-jest-1)
  - [Writing Tests](#writing-tests-1)
    - [Unit Tests](#unit-tests-1)
    - [Integration Tests](#integration-tests-1)
  - [Best Practices](#best-practices-1)
- [Continuous Integration](#continuous-integration)
  - [GitHub Actions](#github-actions)
- [Running Tests](#running-tests)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)
- [Footer](#footer)

## Introduction

Testing is a critical component of software development that helps ensure your application behaves as expected. This guide covers the setup and implementation of various testing methodologies to maintain the integrity of the Next News project.

## Testing Strategy

### Types of Testing

#### Unit Testing

- **Purpose**: Verify the functionality of individual components or functions in isolation.
- **Scope**: Smallest testable parts of the application, such as utility functions or React components.

#### Integration Testing

- **Purpose**: Assess the interaction between different modules or services.
- **Scope**: Combined parts of the application, such as API endpoints interacting with the database.

#### End-to-End (E2E) Testing

- **Purpose**: Validate the complete flow of the application from the user's perspective.
- **Scope**: Entire application workflow, ensuring all parts work together seamlessly.

#### Performance Testing

- **Purpose**: Ensure the application performs well under expected load conditions.
- **Scope**: Response times, throughput, and resource utilization.

#### Security Testing

- **Purpose**: Identify vulnerabilities and ensure data protection.
- **Scope**: Authentication, authorization, data encryption, and protection against common threats.

## Frontend Testing

### Tools

#### Jest

- **Description**: A JavaScript testing framework used for unit and integration testing.
- **Features**:
  - Snapshot testing
  - Mocking capabilities
  - Code coverage reports

#### React Testing Library

- **Description**: A library for testing React components by simulating user interactions.
- **Features**:
  - Queries to select elements
  - Encourages testing based on user behavior

#### Cypress

- **Description**: An end-to-end testing framework that allows you to write tests that run in the browser.
- **Features**:
  - Real-time reloads
  - Time-travel debugging
  - Network traffic control

### Setup

#### Installing Dependencies

Navigate to your frontend project directory and install the necessary testing libraries.

```bash
cd next-news-frontend

# Install Jest and related packages
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @testing-library/user-event babel-jest

# Install Cypress for E2E testing
npm install --save-dev cypress
```

#### Configuring Jest

1. **Create Jest Configuration File**

   Create a `jest.config.js` file in the root of your frontend project.

   ```javascript
   // jest.config.js
   module.exports = {
     testEnvironment: "jsdom",
     setupFilesAfterEnv: ["<rootDir>/jest.setup.js"],
     moduleNameMapper: {
       "\\.(css|less|scss|sass)$": "identity-obj-proxy",
     },
   };
   ```

2. **Set Up Testing Environment**

   Create a `jest.setup.js` file to configure the testing environment.

   ```javascript
   // jest.setup.js
   import "@testing-library/jest-dom/extend-expect";
   ```

3. **Update `package.json` Scripts**

   Add test scripts to your `package.json`.

   ```json
   {
     "scripts": {
       "test": "jest",
       "test:watch": "jest --watch",
       "test:coverage": "jest --coverage",
       "cypress:open": "cypress open",
       "cypress:run": "cypress run"
     }
   }
   ```

### Writing Tests

#### Unit Tests

Focus on testing individual components and functions.

**Example: Testing the Button Component**

```javascript
// components/__tests__/Button.test.js
import { render, screen, fireEvent } from "@testing-library/react";
import Button from "../Button";

test("renders button with correct text", () => {
  render(<Button>Click Me</Button>);
  const buttonElement = screen.getByText(/Click Me/i);
  expect(buttonElement).toBeInTheDocument();
});

test("calls onClick handler when clicked", () => {
  const handleClick = jest.fn();
  render(<Button onClick={handleClick}>Click Me</Button>);
  const buttonElement = screen.getByText(/Click Me/i);
  fireEvent.click(buttonElement);
  expect(handleClick).toHaveBeenCalledTimes(1);
});
```

#### Integration Tests

Test the interaction between components and APIs.

**Example: Testing the Navbar Component with Theme Context**

```javascript
// components/__tests__/Navbar.test.js
import { render, screen, fireEvent } from "@testing-library/react";
import Navbar from "../Navbar";
import { ThemeProvider } from "../../context/ThemeContext";

test("renders Navbar with site title", () => {
  render(
    <ThemeProvider>
      <Navbar />
    </ThemeProvider>
  );
  const titleElement = screen.getByText(/Next News/i);
  expect(titleElement).toBeInTheDocument();
});

test("toggles theme when theme button is clicked", () => {
  render(
    <ThemeProvider>
      <Navbar />
    </ThemeProvider>
  );
  const themeButton = screen.getByRole("button");
  fireEvent.click(themeButton);
  expect(document.documentElement).toHaveClass("dark");
  fireEvent.click(themeButton);
  expect(document.documentElement).toHaveClass("light");
});
```

#### End-to-End Tests

Simulate user interactions and validate entire workflows.

**Example: Testing Article Navigation with Cypress**

1. **Initialize Cypress**

   ```bash
   npx cypress open
   ```

   This will open the Cypress Test Runner and create necessary folders.

2. **Write E2E Tests**

   Create a test file `cypress/integration/articles.spec.js`.

   ```javascript
   // cypress/integration/articles.spec.js
   describe("Articles", () => {
     it("Loads the homepage and displays articles", () => {
       cy.visit("/");
       cy.contains("Latest News").should("be.visible");
       cy.get("div.grid").within(() => {
         cy.get("div.border").should("have.length.greaterThan", 0);
       });
     });

     it("Navigates to an article page", () => {
       cy.visit("/");
       cy.get("a.text-blue-500").first().click();
       cy.url().should("include", "/articles/");
       cy.get("h1").should("be.visible");
     });
   });
   ```

3. **Run Cypress Tests**

   ```bash
   npx cypress run
   ```

### Best Practices

- **Write Clear and Descriptive Tests**: Ensure test cases are easy to understand and maintain.
- **Test User Behavior**: Focus on how users interact with the application rather than implementation details.
- **Maintain Test Isolation**: Each test should run independently without relying on the state of other tests.
- **Use Mocks and Stubs**: Mock external dependencies to focus tests on specific units.
- **Aim for High Coverage**: Strive for comprehensive coverage but prioritize critical paths.

## Backend Testing

### Tools

#### Jest

- **Description**: A JavaScript testing framework used for unit and integration testing in Node.js applications.
- **Features**:
  - Snapshot testing
  - Mocking capabilities
  - Code coverage reports

#### Supertest

- **Description**: A library for testing Node.js HTTP servers.
- **Features**:
  - Fluent API for making HTTP requests
  - Assertion support

### Setup

#### Installing Dependencies

Navigate to your Strapi backend project directory and install the necessary testing libraries.

```bash
cd next-news-backend

# Install Jest and related packages
npm install --save-dev jest supertest

# Optionally, install other testing utilities
npm install --save-dev @types/jest ts-jest
```

#### Configuring Jest

1. **Create Jest Configuration File**

   Create a `jest.config.js` file in the root of your backend project.

   ```javascript
   // jest.config.js
   module.exports = {
     testEnvironment: "node",
     setupFilesAfterEnv: ["<rootDir>/jest.setup.js"],
     moduleNameMapper: {
       "\\.(css|less|scss|sass)$": "identity-obj-proxy",
     },
   };
   ```

2. **Set Up Testing Environment**

   Create a `jest.setup.js` file to configure the testing environment.

   ```javascript
   // jest.setup.js
   jest.setTimeout(30000); // Increase timeout if needed
   ```

3. **Update `package.json` Scripts**

   Add test scripts to your `package.json`.

   ```json
   {
     "scripts": {
       "test": "jest",
       "test:watch": "jest --watch",
       "test:coverage": "jest --coverage"
     }
   }
   ```

### Writing Tests

#### Unit Tests

Focus on testing individual controllers, services, and utilities.

**Example: Testing the Article Service**

```javascript
// src/api/article/services/article.test.js
const { createArticle, getArticle } = require("./article");
const strapi = require("strapi"); // Mock Strapi instance

jest.mock("strapi", () => ({
  query: jest.fn(),
}));

describe("Article Service", () => {
  beforeEach(() => {
    strapi.query.mockClear();
  });

  test("createArticle creates a new article", async () => {
    const articleData = {
      title: "Test Article",
      content: "This is a test article.",
      published_at: "2024-05-01T08:00:00.000Z",
      author: 1,
      category: 1,
    };

    strapi.query.mockReturnValue({
      create: jest.fn().mockResolvedValue(articleData),
    });

    const result = await createArticle(articleData);
    expect(strapi.query).toHaveBeenCalledWith("api::article.article");
    expect(result).toEqual(articleData);
  });

  test("getArticle retrieves an article by ID", async () => {
    const article = {
      id: 1,
      title: "Test Article",
      content: "This is a test article.",
      published_at: "2024-05-01T08:00:00.000Z",
      author: { id: 1, name: "Author Name" },
      category: { id: 1, name: "Technology" },
    };

    strapi.query.mockReturnValue({
      findOne: jest.fn().mockResolvedValue(article),
    });

    const result = await getArticle(1);
    expect(strapi.query).toHaveBeenCalledWith("api::article.article");
    expect(result).toEqual(article);
  });
});
```

#### Integration Tests

Test the interaction between different parts of the backend, such as API endpoints and the database.

**Example: Testing the Articles API Endpoint**

```javascript
// src/api/article/controllers/article.test.js
const request = require("supertest");
const strapi = require("strapi"); // Mock Strapi instance

let server;

beforeAll(async () => {
  server = await strapi().load();
  await strapi().start();
});

afterAll(async () => {
  await strapi().stop();
});

describe("GET /api/articles", () => {
  it("should return a list of articles", async () => {
    const response = await request(server)
      .get("/api/articles?populate=*")
      .expect(200);

    expect(Array.isArray(response.body.data)).toBe(true);
    // Additional assertions based on your data structure
  });
});
```

### Best Practices

- **Isolate Tests**: Ensure each test runs independently without relying on external state.
- **Mock External Dependencies**: Use mocking to isolate the unit under test.
- **Use Test Databases**: Set up separate databases for testing to prevent data contamination.
- **Automate Tests**: Integrate tests into your CI/CD pipeline to run automatically on commits and pull requests.
- **Maintain High Coverage**: Strive for comprehensive test coverage, focusing on critical paths and functionalities.

## Continuous Integration

Integrating testing into your CI/CD pipeline ensures that tests run automatically on code changes, maintaining code quality and preventing regressions.

### GitHub Actions

Set up GitHub Actions to run tests on every push and pull request.

**Example: GitHub Actions Workflow**

Create a `.github/workflows/ci.yml` file in your repository.

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  frontend-tests:
    runs-on: ubuntu-latest
    name: Frontend Tests
    steps:
      - uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "16"

      - name: Install Dependencies
        run: |
          cd frontend
          npm install

      - name: Run Unit and Integration Tests
        run: |
          cd frontend
          npm test -- --coverage

      - name: Upload Coverage Report
        uses: actions/upload-artifact@v2
        with:
          name: coverage-report
          path: frontend/coverage

  backend-tests:
    runs-on: ubuntu-latest
    name: Backend Tests
    steps:
      - uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "16"

      - name: Install Dependencies
        run: |
          cd backend
          npm install

      - name: Run Tests
        run: |
          cd backend
          npm test -- --coverage

      - name: Upload Coverage Report
        uses: actions/upload-artifact@v2
        with:
          name: coverage-report
          path: backend/coverage
```

**Explanation:**

- **Trigger**: The workflow runs on pushes and pull requests to the `main` and `develop` branches.
- **Jobs**:
  - **frontend-tests**: Checks out the code, sets up Node.js, installs frontend dependencies, runs tests, and uploads coverage reports.
  - **backend-tests**: Checks out the code, sets up Node.js, installs backend dependencies, runs tests, and uploads coverage reports.

## Running Tests

### Frontend

- **Unit and Integration Tests**

  ```bash
  cd frontend
  npm test
  # or
  yarn test
  ```

- **End-to-End Tests**

  ```bash
  npm run cypress:open
  # or
  yarn cypress:open
  ```

### Backend

- **Unit and Integration Tests**

  ```bash
  cd backend
  npm test
  # or
  yarn test
  ```

## Troubleshooting

### Common Issues

- **Tests Failing Unexpectedly**

  - Ensure all dependencies are installed correctly.
  - Check for recent changes that might have introduced bugs.
  - Verify that environment variables are correctly set for testing.

- **Coverage Reports Not Generating**

  - Confirm that the testing framework is configured to collect coverage data.
  - Ensure the coverage directory is correctly specified in your CI workflow.

- **Cypress Not Opening**
  - Make sure Cypress is installed in your project.
  - Verify that the development server is running if required for E2E tests.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue**: Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page to report the problem.
- **Refer to Documentation**:
  - [Jest Documentation](https://jestjs.io/docs/getting-started)
  - [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/intro/)
  - [Cypress Documentation](https://docs.cypress.io/)
  - [Strapi Testing Guide](https://strapi.io/documentation/developer-docs/latest/development/testing.html)
- **Community Support**: Engage with the Next.js, Jest, and Strapi communities through forums and discussion boards.

## Additional Resources

- [Next.js Testing Documentation](https://nextjs.org/docs/testing)
- [Jest Official Documentation](https://jestjs.io/docs/getting-started)
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
- [Cypress Documentation](https://docs.cypress.io/)
- [Strapi Testing Documentation](https://strapi.io/documentation/developer-docs/latest/development/testing.html)
- [Supertest Documentation](https://github.com/visionmedia/supertest)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

## Footer

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly identifies the document as a testing guide for the Next News project, emphasizing its importance in maintaining application quality and reliability.

- **Table of Contents**: Organized list of sections, enabling users to navigate through the document easily.

- **Testing Strategy**:

  - **Types of Testing**: Outlines various testing methodologies such as Unit, Integration, E2E, Performance, and Security Testing, providing a comprehensive overview of the testing landscape.

- **Frontend Testing**:

  - **Tools**: Introduces Jest, React Testing Library, and Cypress as the primary tools for frontend testing, explaining their purposes and features.
  - **Setup**: Guides users through installing dependencies and configuring Jest for testing.
  - **Writing Tests**:
    - **Unit Tests**: Provides examples of testing individual components like the Button component.
    - **Integration Tests**: Demonstrates testing interactions between components and contexts, such as the Navbar with Theme Context.
    - **End-to-End Tests**: Shows how to use Cypress for simulating user interactions and verifying application workflows.
  - **Best Practices**: Emphasizes writing clear tests, focusing on user behavior, maintaining test isolation, using mocks, and achieving high coverage.

- **Backend Testing**:

  - **Tools**: Introduces Jest and Supertest for backend testing, detailing their roles in unit and integration testing.
  - **Setup**: Instructs on installing dependencies and configuring Jest for the backend.
  - **Writing Tests**:
    - **Unit Tests**: Example of testing service functions like creating and retrieving articles.
    - **Integration Tests**: Example of testing API endpoints using Supertest.
  - **Best Practices**: Highlights isolating tests, mocking dependencies, using test databases, automating tests, and maintaining high coverage.

- **Continuous Integration**:

  - **GitHub Actions**: Provides a sample GitHub Actions workflow to automate running frontend and backend tests on pushes and pull requests, ensuring code quality through automated testing.

- **Running Tests**:

  - **Frontend**: Commands to run unit, integration, and E2E tests.
  - **Backend**: Commands to run unit and integration tests.

- **Troubleshooting**:

  - **Common Issues**: Lists frequent problems such as failing tests, coverage report issues, and Cypress setup problems, along with potential solutions.
  - **Getting Help**: Directs users to GitHub Issues, official documentation, and community support for additional assistance.

- **Additional Resources**: Provides links to official documentation and resources for Next.js, Jest, React Testing Library, Cypress, Strapi, and GitHub Actions, enabling users to explore further.

- **Footer**: Includes essential project information, author details, website link, and contact information, ensuring users have access to support and additional resources.

Overall, the **Testing.md** file serves as a comprehensive guide for setting up and implementing testing strategies in the Next News project. It covers tools, setup procedures, writing effective tests, integrating testing into CI pipelines, and troubleshooting common issues, ensuring that developers can maintain a high-quality, reliable application.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this testing guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
