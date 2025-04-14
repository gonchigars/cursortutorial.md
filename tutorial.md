# Practical Guide: Full Stack Development with Cursor & AI

## Getting Started

### Setting Up Your Environment
1. **Install Cursor**
   - Go to [cursor.com](https://cursor.com)
   - Download the appropriate version for your OS
   - Run the installer and follow the prompts
   - Start Cursor and activate the free Pro trial

2. **Configure Your Workspace**
   - Open a new or existing project folder
   - Navigate the interface: file explorer (left), editor (center), terminal (bottom)
   - Open the AI Chat panel with `Ctrl/Cmd + L` if not visible
   - Configure settings at File > Preferences > Cursor Settings

3. **Set Up AI Models**
   - Choose your preferred model in the AI chat panel dropdown
   - Recommended: Claude 3.5 Sonnet for most coding tasks
   - Consider Claude 3.7 Sonnet for complex design tasks
   - Ensure your API keys are correctly configured if required

## Basic Workflow

### Creating a New Project
1. **Project Initialization**
   - Open the terminal with "Terminal > New Terminal"
   - Use the Agent mode in the AI panel
   - Prompt: "Please create a new [type] project using [technologies]"
   - Example: "Please create a basic landing page using React and Tailwind CSS with Vite"
   - Review and run the suggested commands

2. **Define Project Structure**
   - Prompt: "Help me set up a proper file structure for this project"
   - Specify any preferences for organization
   - Have the AI create necessary configuration files
   - Example: "Create appropriate config files for ESLint, Prettier, and Tailwind"

3. **Version Control Setup**
   - Initialize Git repository if needed
   - Create .gitignore and README.md files
   - Prompt: "Create a comprehensive .gitignore file for a [your stack] project and a basic README"

## Front-End Development

### Building UI Components
1. **Create Component Structure**
   - Prompt: "Let's create the following components for our app: [list components]"
   - Be specific about component hierarchy
   - Example: "Create Header, Footer, Hero, Features, and Pricing components"

2. **Styling Components**
   - Specify desired styling approach
   - Prompt: "Style the Header component using Tailwind with a responsive design"
   - Use screenshots as reference when possible
   - Example with image: "Make the layout look similar to this design [attach image]"

3. **Adding Interactivity**
   - Define interactions clearly
   - Prompt: "Add a dropdown menu to the Header that appears on mobile"
   - Specify state management approach if needed
   - For complex interactions, break down into steps

4. **Troubleshooting UI Issues**
   - Be specific about the problem
   - Prompt: "The dropdown menu isn't working on mobile. Here's the error: [paste error]"
   - Use the "Fix and Chat" feature for quick fixes
   - Consider "restore checkpoint" if changes make things worse

## Back-End Development

### Setting Up the Server
1. **Initialize Backend**
   - Prompt: "Create an Express.js server with the following routes: [list routes]"
   - Specify folder structure preferences
   - Example: "Set up a server folder with controllers, routes, and middleware directories"

2. **Database Integration**
   - Choose and specify your database
   - Prompt: "Set up MongoDB connection with Mongoose and create the following schemas: [list schemas]"
   - Have AI generate sample data for testing

3. **Authentication System**
   - Specify auth requirements
   - Prompt: "Implement JWT authentication with login, register, and password reset endpoints"
   - Ask for security best practices

4. **API Endpoints**
   - List all required endpoints clearly
   - Prompt: "Create CRUD endpoints for the User and Product resources"
   - Specify validation requirements
   - Example: "Add validation to ensure emails are unique and passwords are strong"

## Implementing Test-Driven Development

### Setting Up Testing Framework
1. **Initialize Testing Environment**
   - Prompt: "Set up Jest and React Testing Library for our front-end tests"
   - For backend: "Configure testing environment with Jest and Supertest"
   - Have AI create test config files

2. **Writing Tests First**
   - Prompt: "Write tests for a User component that displays user information and has an edit button"
   - Specify expected behavior clearly
   - Example: "The component should render user's name, email, and have an edit button that shows a form when clicked"

3. **Implementing Features To Pass Tests**
   - After tests are written, prompt: "Now implement the User component to pass these tests"
   - Review the implementation
   - Run tests to verify

4. **Test-Fix Cycle**
   - If tests fail, share specific errors
   - Prompt: "The test for edit button click is failing with this error: [paste error]"
   - Let AI suggest fixes or improvements

## Task Management for Complex Projects

### Setting Up TaskMaster
1. **Installation**
   ```
   npm install -g taskmaster-ai
   ```

2. **Project Initialization**
   - Create your project folder and navigate to it
   - Run: `taskmaster init`
   - Fill in project name and description
   - Configure API keys as guided in the `.env.example` file

3. **Creating a PRD (Product Requirements Document)**
   - Create `scripts/prd.txt` file
   - Use this prompt: "Help me create a PRD for [your project]"
   - Have AI detail core features, requirements, and constraints
   - Example: "Create a PRD for a task management application with team collaboration features"

4. **Breaking Down the PRD into Tasks**
   - Run: `taskmaster parse prd scripts/prd.txt`
   - Review generated tasks: `taskmaster list`
   - Analyze complexity: `taskmaster analyze complexity`
   - Generate complexity report: `taskmaster complexity report`

5. **Managing Task Implementation**
   - Start AI implementation with: "Let's start implementing the app based on tasks we created using taskmaster"
   - Let AI check next tasks: "Check the next most important task to implement"
   - For complex tasks, break them down further: Use the prompt from complexity report
   - After completing a task: `taskmaster update [ID] --status=done`

### Using Cursor.rules for Task Management
1. **Create Basic Task Tracking Rule**
   - Create a file named `cursor.rules` in your project root
   - Add this rule: "Always refer to task.md to keep track of tasks. Mark tasks as completed when finished."

2. **Initialize Tasks File**
   - Create a task.md file
   - Prompt: "Help me break down building [project] into small tasks and add them to task.md"
   - AI will generate a list of tasks in the file

3. **Using Tasks During Development**
   - Before implementing, prompt: "Let's implement the next task from task.md"
   - After completing a task: "Mark the [task name] as completed in task.md"
   - When adding new requirements: "Add these new tasks to task.md: [list tasks]"

## Advanced Context Management

### Effective File Tagging
1. **Tagging Relevant Files**
   - Use the @ symbol followed by filename
   - Example: "Let's modify the header component @components/Header.jsx to include a search bar"
   - For multiple files: "@components/Header.jsx and @components/Navbar.jsx need to be updated to use the new theme"

2. **Using Documentation Context**
   - Use @Doc followed by library name
   - Example: "@Doc React to help implement context API for user authentication"
   - For web search: "@web for latest best practices in React server components"

3. **Managing Conversation Context**
   - Start new chats for new features
   - Use "New chat with summary" for related but different tasks
   - Reference previous conversations: "Based on our previous chat about authentication..."

### Working with Large Codebases
1. **Breaking Down Large Files**
   - Prompt: "Help me refactor @services/api.js into smaller modules"
   - Be specific about what to extract
   - Example: "Let's extract all user-related functions into a separate users.js file"

2. **Understanding Existing Code**
   - Prompt: "Explain what @utils/helpers.js does in detail"
   - For focused explanation: "Explain this function in @components/DataTable.jsx line 120-150"
   - Have AI suggest improvements: "Any suggestions to improve the performance of this code?"

## Troubleshooting

### Debugging Errors
1. **Sharing Detailed Error Information**
   - Copy the full error stack
   - Provide context: "I'm getting this error when trying to submit the form: [paste error]"
   - Tag relevant files: "@components/Form.jsx has this error when submitting"

2. **Using The Beaver Method**
   - Prompt: "Add detailed console logs to @services/auth.js to help debug the login issue"
   - Run the code with logs
   - Share the log output: "Here are the logs I'm seeing: [paste logs]"
   - Let AI interpret the logs and suggest fixes

3. **When You're Stuck**
   - Try the "radical" approach: "Let's try a radically different approach to solving this authentication issue"
   - Ask for alternative solutions: "What are 3 different ways we could implement this feature?"
   - If still stuck, review fundamentals: "Explain the core concepts I need to understand to fix this issue"

### Creating Self-Improving Rules
1. **Detecting Patterns in Errors**
   - After resolving an issue, prompt: "Based on this error, create a cursor rule to prevent similar issues"
   - Example: "Create a rule to ensure we always check for null values before accessing object properties"

2. **Adding Rules to cursor.rules**
   - Have AI generate the rule
   - Add it to your cursor.rules file
   - Test it on similar problems

## Real-World Project Examples

### Building a Social Media Dashboard
1. **Planning Phase**
   - Create PRD for features (user profiles, posts, analytics)
   - Set up TaskMaster to break down tasks
   - Establish tech stack (React, Node.js, MongoDB)

2. **Implementation Steps**
   - Follow task dependencies order
   - Implement authentication first
   - Build UI components with proper tests
   - Create backend API endpoints
   - Connect frontend and backend
   - Test thoroughly

### E-Commerce Platform
1. **Core Features**
   - User authentication
   - Product catalog
   - Shopping cart
   - Checkout process
   - Order management

2. **Implementation Approach**
   - Set up database schemas first
   - Create API endpoints
   - Implement frontend components
   - Connect payment processing
   - Add admin dashboard
   - Test and optimize

### Multiplayer Drawing Game (TaskMaster Example)
1. **Setup**
   - Initialize NextJS project
   - Install TaskMaster
   - Create detailed PRD for game mechanics

2. **Implementation Steps**
   - Break down game into components (lobby, canvas, scoring)
   - Implement real-time functionality with WebSockets
   - Add drawing tools with HTML5 Canvas
   - Integrate GPT-4V for image analysis
   - Test multiplayer functionality
   - Deploy and monitor

## Best Practices Checklist

### Effective AI Collaboration
- [ ] Be specific about technologies and requirements
- [ ] Break complex tasks into smaller steps
- [ ] Provide examples when possible
- [ ] Tag relevant files for context
- [ ] Start new chats for new features
- [ ] Tell AI what works and what needs changing
- [ ] Review code before accepting changes

### Code Quality
- [ ] Follow consistent naming conventions
- [ ] Implement tests for critical features
- [ ] Document code and features
- [ ] Check for security vulnerabilities
- [ ] Optimize performance for key operations
- [ ] Refactor regularly to maintain clean code
- [ ] Use cursor.rules to maintain standards

### Project Management
- [ ] Use TaskMaster or task.md to track progress
- [ ] Implement features in proper dependency order
- [ ] Break down complex tasks
- [ ] Set clear acceptance criteria for features
- [ ] Document implementation decisions
- [ ] Create self-improving cursor rules

## Resources and References
- [Cursor Documentation](https://cursor.com/docs)
- [TaskMaster GitHub Repository](https://github.com/taskmaster-ai)
- [Claude Documentation](https://docs.anthropic.com)
- [React Documentation](https://reactjs.org)
- [Express Documentation](https://expressjs.com)
- [Jest Testing Framework](https://jestjs.io)

---

This practical guide provides a step-by-step approach to developing full-stack applications with Cursor and AI assistance. Adapt these workflows to your specific project needs and preferences.
