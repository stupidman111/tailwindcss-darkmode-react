# Dark Mode Configuration with Tailwind CSS

This guide walks you through setting up Dark Mode in a React project using TailwindCSS.

## Prerequisites

1. A React project built with [Vite]().
2. Tailwind CSS installed and configured.

- If not, follow the [TailwindCSS with Vite]() installation guide.

## Steps to Configure Dark Mode

### Step 1: Update tailwind.config.js

Update your tailwind.config.js file as follows:

```js
export default {
  darkMode: ["selector"],
  //...
};
```

### Step2: Implement Dark Mode Toggle in React

Create a simple React component to manage Dark Mode state. The dark mode state will persist in localStorage to save user preferences.

```react
import React, { useState, useEffect } from 'react';

function App() {
  const [darkMode, setDarkMode] = useState(() => {
    // Retrieve the user's dark mode preference from localStorage
    return localStorage.getItem('darkMode') === 'true';
  });

  const toggleDarkMode = () => {
    setDarkMode((prev) => {
      const newMode = !prev;
      localStorage.setItem('darkMode', newMode); // Save preference
      return newMode;
    });
  };

  useEffect(() => {
    // Apply the "dark" class to the <html> element based on the state
    if (darkMode) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  }, [darkMode]);

  return (
    <div className="min-h-screen bg-white dark:bg-gray-900 text-black dark:text-white flex flex-col items-center justify-center">
      <h1 className="text-4xl mb-4">Hello, Tailwind CSS Dark Mode!</h1>
      <button
        onClick={toggleDarkMode}
        className="px-4 py-2 bg-blue-500 dark:bg-blue-700 text-white rounded"
      >
        {darkMode ? 'Switch to Light Mode' : 'Switch to Dark Mode'}
      </button>
    </div>
  );
}

export default App;
```
