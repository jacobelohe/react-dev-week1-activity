
**Files:**

*   **`index.html`:**

```html
<!DOCTYPE html>
<html>
<head>
  <title>TypeScript Intro</title>
</head>
<body>
  <h1>Welcome to Bookworm's Paradise</h1>
  <div id="book-list"></div>

  <script src="dist/bundle.js"></script>
</body>
</html>
```

*   **`src/main.js`:**

```javascript
// --- Starter JavaScript Code ---

// A simple Book class (using constructor function in JS)
function Book(title, author, year) {
  this.title = title;
  this.author = author;
  this.year = year;
}

// Function to display book information
function displayBook(book) {
  const bookList = document.getElementById("book-list");
  const bookDiv = document.createElement("div");
  bookDiv.innerHTML = `
    <h2>${book.title}</h2>
    <p>By ${book.author}, ${book.year}</p>
  `;
  bookList.appendChild(bookDiv);
}

// Create some book objects
const book1 = new Book("The Hobbit", "J.R.R. Tolkien", 1937);
const book2 = new Book("The Lord of the Rings", "J.R.R. Tolkien", 1954);

// Display the books on the webpage
displayBook(book1);
displayBook(book2);

// --- Tasks (Converting to TypeScript) ---

// Task 1: Add type annotations to the function parameters and return types.
// Task 2: Convert the Book function to a TypeScript class.
// Task 3: Create an interface for a "Review" object (with properties like bookId, rating, comment).
// Task 4: Add a function to add a review to a book (you can simulate this with an array for now).
// Task 5: Add type annotations to the new variables and functions that you created in prior steps.
```

**Part 1: Convert to TypeScript**

1.  **Rename `main.js` to `main.ts`:** Change the file extension to `.ts` to indicate that it's a TypeScript file.

2.  **Add Type Annotations:**
    *   Add type annotations (`string`, `number`) to the parameters of the `Book` constructor function and the `displayBook` function.
    *   Add return type annotations where appropriate.

3.  **Convert to a Class:**
    *   Convert the `Book` constructor function to a TypeScript `class` with a constructor and properties.

4.  **Create an Interface:**
    *   Define an interface called `Review` with properties like `bookId` (`number`), `rating` (`number`), and `comment` (`string`).

5.  **Add a Function:**
    *   Add a function called `addReview` (or similar) that takes a `bookId`, `rating`, and `comment` as parameters. For now, you can simulate adding a review by pushing an object to a global array. Make sure to use the `Review` interface.

6.  **Add Types to New Code:**
    *   Add type annotations to the parameters and return type of `addReview` and any other variables you introduce.


**Part 2: Set up TypeScript Configuration**

1.  **Initialize npm Project:**
    *   Open your terminal and navigate to your project directory (`my-project`).
    *   Run `npm init -y` to create a `package.json` file.

2.  **Install TypeScript:**
    *   Run `npm install --save-dev typescript` to install TypeScript as a development dependency.

3.  **Create `tsconfig.json`:**
    *   Run `npx tsc --init --project .` to generate a `tsconfig.json` file in your project root. This file will configure the TypeScript compiler.
        *   You can use the `--project .` or just use `npx tsc --init`
    *   **Modify `tsconfig.json`:** Open `tsconfig.json` and make the following changes (these are just basic suggestions):

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

**Part 3: Set up Webpack**

1.  **Install Webpack and Related Packages:**
    *   Run `npm install --save-dev webpack webpack-cli ts-loader` to install Webpack, the Webpack CLI, and `ts-loader` (which allows Webpack to handle `.ts` files).

2.  **Create `webpack.config.js`:**
    *   Create a new file named `webpack.config.js` in your project root.
    *   Add the following configuration:

```javascript
const path = require('path');

module.exports = {
  entry: './src/main.ts',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.ts$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: ['.ts', '.js'],
  },
  mode: 'development',
  devtool: 'inline-source-map'
};
```

**Part 4: Update `package.json`**

1.  **Add a Build Script:**
    *   Open your `package.json` file and add a `build` script to the `scripts` section:

```json
"scripts": {
  "build": "webpack"
}
```

**Part 5: Build and Run**

1.  **Build the Project:**
    *   In your terminal, run `npm run build`. This will use Webpack to bundle your TypeScript code (transpiled to JavaScript) into `dist/bundle.js`.

2.  **Update `index.html`:**
    *   Make sure your `index.html` file's `<script>` tag is pointing to the correct location of the bundled JavaScript file (it should be `dist/bundle.js`):

```html
<script src="dist/bundle.js"></script>
```

3.  **Run in Browser:**
    *   Open `index.html` in your browser. You should see the output from your TypeScript code (the book list).

**Explanation:**

*   **`webpack.config.js`:**
    *   **`entry`:** Specifies the entry point of your application (your main TypeScript file).
    *   **`output`:** Specifies where the bundled JavaScript file should be placed (`dist/bundle.js`).
    *   **`module.rules`:** Defines how different file types should be handled. Here, we configure `ts-loader`