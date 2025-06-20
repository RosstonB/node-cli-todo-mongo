# Node CLI Todo MongoDB

A command-line todo application built with Node.js and MongoDB. Manage your tasks directly from the terminal with a simple and intuitive interface.

## Features

- ✅ Create new todos with name and description
- 📖 Read and display all todos
- ✏️ Update existing todos (name, description, or status)
- 🗑️ Delete todos by code
- 🔄 Auto-completion when status is marked as "completed"
- 🎨 Colorful terminal output with loading spinners
- 🗄️ MongoDB integration for persistent storage

## Prerequisites

- Node.js (v14 or higher)
- MongoDB (local installation or MongoDB Atlas)

## Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd node-cli-todo-mongo
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

1. Copy the example environment file:

   ```bash
   cp .env.example .env
   ```

2. Edit the [.env](.env) file and add your MongoDB connection string:

   ```
   MONGO_URI=mongodb://localhost:27017/node-cli-todo-mongo
   ```

   For MongoDB Atlas, use:

   ```
   MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/node-cli-todo-mongo
   ```

### 4. Global Installation (Optional)

To use the `todo` command globally, install the package:

```bash
npm install -g .
```

Or link it for development:

```bash
npm link
```

## Usage

The application provides a `todo` command with four main operations:

### Add New Todos

```bash
todo add
```

This will prompt you to:

- Enter the task name
- Enter the task description
- Choose whether to add more tasks

### Read All Todos

```bash
todo read
```

Displays all existing todos with their:

- Todo Code (unique identifier)
- Name
- Description

### Update a Todo

```bash
todo update
```

This will:

- Prompt for the todo code
- Allow you to update name, description, and status
- Automatically delete the todo if status is set to "completed"

### Delete a Todo

```bash
todo delete
```

Prompts for the todo code and removes the specified todo from the database.

## CLI Package Configuration

The application is configured as a CLI tool in [package.json](package.json) using the `bin` field:

```json
"bin": {
  "todo": "index.js"
}
```

This configuration:

- Maps the `todo` command to the [index.js](index.js) file
- Makes the application executable as a global command when installed
- Uses the shebang `#!/usr/bin/env node` in [index.js](index.js) to run with Node.js

## Project Structure

```
├── commands/           # Command implementations
│   ├── addTask.js     # Add new todos
│   ├── deleteTask.js  # Delete todos
│   ├── readTask.js    # Read all todos
│   └── updateTask.js  # Update existing todos
├── db/
│   └── connectDB.js   # Database connection utilities
├── schema/
│   └── TodoSchema.js  # Mongoose schema definition
├── index.js           # Main CLI entry point
├── package.json       # Dependencies and CLI configuration
├── .env.example       # Environment template
└── README.md
```

## Dependencies

- **commander**: CLI framework for command parsing
- **inquirer**: Interactive command-line prompts
- **mongoose**: MongoDB object modeling
- **chalk**: Terminal string styling
- **ora**: Elegant terminal spinners
- **nanoid**: Unique ID generator for todo codes
- **dotenv**: Environment variable management

## Todo Schema

Each todo has the following structure:

- `name`: Task name (required)
- `detail`: Task description (required)
- `status`: "pending" or "completed" (default: "pending")
- `code`: Unique 10-character identifier (auto-generated)
- `timestamps`: Created and updated dates (auto-managed)

## Development

To run the application locally without global installation:

```bash
node index.js <command>
```

For example:

```bash
node index.js add
node index.js read
```

## License

ISC
