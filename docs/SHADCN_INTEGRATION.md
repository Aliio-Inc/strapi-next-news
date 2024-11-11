# Shadcn Integration Guide for Next News

Integrating **Shadcn** into **Next News** enhances the frontend with a set of modern, accessible, and customizable UI components. This guide provides step-by-step instructions to seamlessly incorporate Shadcn into your Next.js project, ensuring a consistent and polished user interface.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [1. Install Required Dependencies](#1-install-required-dependencies)
  - [2. Set Up Tailwind CSS](#2-set-up-tailwind-css)
  - [3. Install Shadcn UI Components](#3-install-shadcn-ui-components)
- [Configuration](#configuration)
  - [1. Configure Tailwind CSS](#1-configure-tailwind-css)
  - [2. Configure Shadcn](#2-configure-shadcn)
- [Usage](#usage)
  - [1. Importing Shadcn Components](#1-importing-shadcn-components)
  - [2. Using Shadcn Components](#2-using-shadcn-components)
- [Customization](#customization)
  - [1. Theming](#1-theming)
  - [2. Extending Components](#2-extending-components)
- [Best Practices](#best-practices)
  - [1. Accessibility](#1-accessibility)
  - [2. Consistent Styling](#2-consistent-styling)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)

## Prerequisites

Before integrating Shadcn into your project, ensure you have the following:

- **Next.js Project**: Existing setup of Next.js (v12 or later) in **Next News**.
- **Node.js**: Installed (v14 or later).
- **npm** or **Yarn**: Package manager for installing dependencies.

## Installation

### 1. Install Required Dependencies

Shadcn relies on Tailwind CSS and other essential packages. Begin by installing these dependencies.

```bash
# Navigate to the frontend directory
cd frontend

# Install Tailwind CSS and its dependencies
npm install -D tailwindcss postcss autoprefixer

# Initialize Tailwind CSS configuration
npx tailwindcss init -p
```

### 2. Set Up Tailwind CSS

Configure Tailwind CSS by updating the `tailwind.config.js` file.

```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}", // Include if using the App directory
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Create a `globals.css` file if it doesn't exist and include the Tailwind directives.

```css
/* styles/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Ensure that `globals.css` is imported in your `_app.js` or `_app.tsx` file.

```javascript
// pages/_app.js or pages/_app.tsx
import "../styles/globals.css";

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

export default MyApp;
```

### 3. Install Shadcn UI Components

Shadcn provides a collection of UI components built with Radix UI and Tailwind CSS.

#### Option 1: Manual Installation

1. **Clone Shadcn UI Components**

   You can manually copy the components from [Shadcn UI](https://github.com/shadcn/ui) repository.

   ```bash
   git clone https://github.com/shadcn/ui.git
   ```

2. **Copy Components**

   Copy the desired components into your project's `components` directory.

   ```bash
   cp -R ui/components/* ../frontend/components/
   ```

3. **Install Peer Dependencies**

   Shadcn components may require additional dependencies like `@radix-ui/react-*`.

   ```bash
   npm install @radix-ui/react-icons
   ```

#### Option 2: Using Shadcn CLI

1. **Install Shadcn CLI**

   Shadcn provides a CLI tool to streamline component integration.

   ```bash
   npm install -g shadcn
   ```

2. **Initialize Shadcn in Your Project**

   ```bash
   shadcn init
   ```

   Follow the prompts to select the components you wish to install.

## Configuration

### 1. Configure Tailwind CSS

Ensure that Tailwind CSS is correctly set up to work with Shadcn components.

```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}", // Include if using the App directory
  ],
  theme: {
    extend: {
      // Extend the theme as needed
    },
  },
  plugins: [
    require("@tailwindcss/forms"), // Optional: For better form styling
    require("@tailwindcss/typography"), // Optional: For better typography
  ],
};
```

### 2. Configure Shadcn

Shadcn components may require specific configurations or theming adjustments. Refer to the Shadcn documentation for detailed customization options.

```javascript
// Example: Adding custom colors in tailwind.config.js
module.exports = {
  // ...existing configuration
  theme: {
    extend: {
      colors: {
        primary: "#1E40AF",
        secondary: "#9333EA",
      },
    },
  },
  // ...existing configuration
};
```

## Usage

### 1. Importing Shadcn Components

Import Shadcn components into your React components as needed.

```javascript
// Example: Importing a Button component
import { Button } from "../components/Button";

function HomePage() {
  return (
    <div className="flex justify-center items-center min-h-screen">
      <Button variant="primary">Click Me</Button>
    </div>
  );
}

export default HomePage;
```

### 2. Using Shadcn Components

Utilize Shadcn components within your pages and components to build a consistent UI.

```javascript
// Example: Using a Modal component
import { useState } from "react";
import {
  Modal,
  ModalContent,
  ModalHeader,
  ModalFooter,
} from "../components/Modal";
import { Button } from "../components/Button";

function ExampleModal() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <>
      <Button onClick={() => setIsOpen(true)}>Open Modal</Button>
      <Modal isOpen={isOpen} onClose={() => setIsOpen(false)}>
        <ModalContent>
          <ModalHeader>Modal Title</ModalHeader>
          <div className="py-4">
            <p>This is the modal content.</p>
          </div>
          <ModalFooter>
            <Button onClick={() => setIsOpen(false)}>Close</Button>
          </ModalFooter>
        </ModalContent>
      </Modal>
    </>
  );
}

export default ExampleModal;
```

## Customization

### 1. Theming

Customize the appearance of Shadcn components by modifying Tailwind CSS configurations or overriding component styles.

```css
/* Example: Custom button styles in globals.css */
.btn-primary {
  @apply bg-primary text-white hover:bg-primary-dark;
}

.btn-secondary {
  @apply bg-secondary text-white hover:bg-secondary-dark;
}
```

### 2. Extending Components

Extend existing Shadcn components or create new ones to fit your project's specific needs.

```javascript
// Example: Extending the Button component
import { Button as ShadcnButton } from "../components/Button";

export function Button({ children, ...props }) {
  return (
    <ShadcnButton className="rounded-md shadow-md" {...props}>
      {children}
    </ShadcnButton>
  );
}
```

## Best Practices

### 1. Accessibility

- **ARIA Attributes**: Ensure all interactive components include appropriate ARIA attributes.
- **Keyboard Navigation**: Verify that all components are accessible via keyboard.
- **Focus Management**: Manage focus states within components like modals and dropdowns to enhance user experience.

### 2. Consistent Styling

- **Tailwind Classes**: Use consistent Tailwind CSS utility classes across components to maintain uniform styling.
- **Component Variants**: Utilize component variants (e.g., `variant="primary"`) to enforce consistency in UI elements.

## Troubleshooting

### Common Issues

- **Styles Not Applying**:

  - Ensure that Tailwind CSS is correctly configured and imported in your project.
  - Verify that the Shadcn components are correctly imported and used within your React components.

- **Missing Dependencies**:

  - Check that all peer dependencies required by Shadcn components (e.g., `@radix-ui/react-icons`) are installed.

- **Build Errors**:
  - Review the terminal logs for detailed error messages.
  - Ensure that your `tailwind.config.js` includes all necessary paths in the `content` array.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue**: Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page to report the problem.
- **Shadcn Documentation**: Refer to the [Shadcn UI Documentation](https://ui.shadcn.com/docs) for detailed guidance.
- **Community Support**: Engage with the Next.js and Shadcn communities through forums and discussion boards.

## Additional Resources

- [Shadcn UI Documentation](https://ui.shadcn.com/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Radix UI Documentation](https://www.radix-ui.com/docs/primitives/overview/introduction)
- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://reactjs.org/docs/getting-started.html)

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly identifies the document as a guide for integrating Shadcn into the Next News project, emphasizing the benefits of enhanced UI components.
- **Table of Contents**: Provides an organized structure, allowing users to quickly navigate to specific sections such as installation, configuration, usage, customization, best practices, troubleshooting, and additional resources.

- **Prerequisites**: Lists the necessary tools and setup required before starting the integration, ensuring that users are adequately prepared.

- **Installation**:

  - **Install Required Dependencies**: Guides users through installing Tailwind CSS and its dependencies, which are essential for Shadcn.
  - **Set Up Tailwind CSS**: Details the configuration of Tailwind CSS, ensuring it scans the correct directories and includes necessary directives.
  - **Install Shadcn UI Components**: Provides two options for installing Shadcn components—manual installation by cloning and copying components or using the Shadcn CLI for streamlined integration.

- **Configuration**:

  - **Configure Tailwind CSS**: Explains how to extend Tailwind's theme and add plugins to support enhanced styling.
  - **Configure Shadcn**: Offers guidance on customizing Tailwind configurations to align with Shadcn's theming requirements.

- **Usage**:

  - **Importing Shadcn Components**: Demonstrates how to import Shadcn components into React components within the Next.js project.
  - **Using Shadcn Components**: Provides examples of utilizing Shadcn components like Buttons and Modals in practical scenarios.

- **Customization**:

  - **Theming**: Shows how to customize the appearance of Shadcn components by modifying Tailwind CSS configurations.
  - **Extending Components**: Guides users on extending existing Shadcn components or creating new ones to fit specific project needs.

- **Best Practices**:

  - **Accessibility**: Emphasizes the importance of making UI components accessible by using ARIA attributes, ensuring keyboard navigation, and managing focus states.
  - **Consistent Styling**: Advises on maintaining uniform styling across components using Tailwind CSS utility classes and component variants.

- **Troubleshooting**:

  - **Common Issues**: Identifies frequent problems such as styles not applying, missing dependencies, and build errors, providing solutions to each.
  - **Getting Help**: Directs users to appropriate channels for additional support, including GitHub Issues and official documentation.

- **Additional Resources**: Lists relevant documentation and resources for further learning and reference, aiding users in deepening their understanding and troubleshooting independently.

- **Footer**: Includes essential project information, author details, website link, and contact information, ensuring users have access to support and additional resources.

Overall, the **Shadcn_Integration.md** file serves as a comprehensive guide to help developers integrate Shadcn UI components into the Next News project effectively. It covers all necessary steps from installation to customization, emphasizing best practices and providing solutions to common issues. This ensures that the integration process is smooth, the UI remains consistent and accessible, and the project maintains high standards of quality and performance.
