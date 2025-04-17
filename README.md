# **jasper**
### Development Project Manager for Linux

A command-line interface for managing development projects within Unix-based systems. 

jasper aims to simplify and automate the development process, providing standardized workflows, environment management, and project management capabilities.

It is also primarily a learning experience for me personally and for anyone else who might find it useful.

###### Yes, I know the name is just my name, but I like it, and I said it in the mirror to myself 100 times over and over again until I lost any meaning of it, therefore making it a perfect word to add meaning to.

---

## **Overview**

jasper streamlines development by providing tools for project setup, environment configuration, development tool integration, and common tasks such as Docker configuration, deployment, and version control.

---

## **Implementation Roadmap (Priority Order)**

### **Phase 1: Core Infrastructure**

1. **Installation System (`install.sh`)**
   - Create install script that:
     - Sets up system-wide directory (`/usr/local/jasper`)
     - Asks user to name projects directory
     - Configures projects directory (user's choice of `~/projects` or `~/jasper/projects`)
     - Places `jasper` executable in `/usr/local/bin`
     - Adds necessary entries to `.bashrc`

2. **Project Management Foundation (`jasper.sh`)**
   - Create main script with:
     - First-run setup (check/create `~/jasper/` if needed)
     - Project initialization capability
     - Directory structure creation
     - Basic command framework
     - User-specific configurations

3. **Configuration System**
   - Define configuration file formats
   - Implement loading/saving of configurations
   - Choose standard format for all configs (recommend YAML for readability)
   - Account management functionality for multi-user systems

### **Phase 2: Project Environment Management**

1. **Environment Variable Management**
   - CLI interface with CRUD operations for environment variables
   - Option to save globally or to a project
   - Project-scoped environment variables
   - Environment switching (dev/staging/prod)
   - Environment file templates
   - Standard format located in project's root directory for external tool compatibility

2. **Project Command Aliases**
   - CLI interface with CRUD operations for custom commands
   - Option to save globally or to a project
   - Project "activation" system ("entering" a project)
   - Command discovery and help system
   - Logging functionality for tracking execution history or errors

3. **Path Translation Utility**
   - WSL to Windows path conversion (e.g., `/home/jasper/jasper` to `\\wsl.localhost\Debian\home\jasper\jasper`)
   - Windows to WSL path conversion
   - Clipboard integration for path sharing

### **Phase 3: Development Tool Integration**

1. **Version Control Integration**
   - Git setup wizard with sensible defaults
   - GitHub/GitLab connection helpers
   - Common git workflow shortcuts

2. **Container Management**
   - Docker setup and configuration
   - Compile list of example Docker Compose file services for quick setups
   - Container management shortcuts

3. **Language/Runtime Support**
   - **Node.js**:
     - NVM integration for installing/updating Node.js
     - NPM/Yarn configuration and helpers
   - **Golang**:
     - Setup scripts for configuring Go development environments
   - **Hugo**:
     - Preconfigured setup for Hugo (static site generator) projects
   - **Deno**:
     - Setup scripts for Deno runtime

### **Phase 4: Advanced Features**

1. **Database Management**
   - PostgreSQL setup and management
   - Connection string management
   - Creation of dev/staging/prod databases
   - Backup/restore utilities

2. **Deployment Tools**
   - FTP/SFTP deployment scripts
   - SSH-based deployment
   - Environment-specific deployment configurations
   - Template-based deployment generation with project-specific values

3. **Documentation Generation**
   - Comment-based documentation extraction
   - Project documentation templates
   - Markdown generation
   - Auto-generate documentation from source code comments

4. **Frontend Development Tools**
   - Bundler configuration (Webpack/Vite)
   - SASS/CSS preprocessing
   - Frontend framework templates

5. **Import/Export System**
   - Project configuration portability
   - Team sharing capabilities
   - Backup/restore of project settings
   - Data format selection (JSON, YAML, XML, or CSV)

---

## **Directory Structure**

```
System-Wide (Global):
/usr/local/bin/jasper                  # Global executable
/opt/jasper/                           # Global configuration
  ├── config.yaml                      # System config with paths
  └── templates/                       # Project templates

User-Specific:
~/jasper/                              # User-specific directory
  ├── jasper.env                       # User-scope project-global environment variables
  ├── secret.jasper.env                # User-scope project-global encrypted environment variables
  ├── user.jasper                      # User-scope jasper code ? not sure if this is needed
  └── cache/                           # Cache for faster operations

Projects:
~/projects/ or ~/jasper/projects/      # Projects root (user choice)
  └── project1/                        # Individual project
      ├── .git/                        # Git repository
      ├── src/                         # Source code
      ├── docs/                        # Project documentation
      ├── jasper.env                   # Project environment variables
      ├── secret.jasper.env            # Project encrypted environment variables
      └── .jasper/                     # jasper project config (hidden)
          ├── env.dev.yaml             # Dev environment vars
          ├── env.prod.yaml            # Prod environment vars
          ├── commands.yaml            # Project commands
          ├── deployment.yaml          # Deployment config
          └── config.yaml              # Project settings
```

---

## **Additional Considerations**

1. **Security**
   - Secure storage for sensitive credentials
   - Environment variable encryption for production secrets
   - SSH key management
   - Ensure script respects user permissions for sensitive directories

2. **Performance**
   - Caching mechanisms for frequently used data
   - Lazy loading of project configurations
   - Minimal dependencies to ensure fast startup

3. **User Experience**
   - Comprehensive help system
   - Tab completion for commands
   - Color-coded output and progress indicators
   - Logging system with verbosity levels

4. **Extensibility**
   - Plugin architecture for custom tools
   - Hook system for project events
   - API for external tool integration

5. **Cross-WSL Distribution Support**
   - Test on Ubuntu, Debian, and other common WSL distros
   - Handle distribution-specific package management

6. **Testing Framework**
   - Unit tests for core functionality
   - Integration tests for tool interactions
   - Test project templates
   - Automated testing for interactions with external tools

---

## **Command Structure Suggestion**

```
jasper [global options] <command> [command options] [arguments...]

Commands:
  init        Initialize a new project
  enter       Activate a project environment
  env         Manage environment variables
  cmd         Manage project commands
  tool        Install/configure development tools
  deploy      Deploy project
  path        Convert between WSL and Windows paths
  config      Configure jasper settings
  help        Show help information
```

---

## **Next Steps Before Starting**

1. **Finalize the User Experience**:
   - Clarify how users will interact with the system. For instance:
     - How will the user choose the project directory location (`~/projects` vs. `~/jasper/projects`) during installation?
     - How will users input configuration details (e.g., Git setup, environment variables)?

2. **Define Configuration File Formats**:
   - Decide on the format for storing configurations, environment variables, and project-specific data (e.g., JSON, YAML).

3. **Error Handling and Logging**:
   - Define how the tool will handle errors and log information. This is crucial for debugging and providing feedback to users.

4. **Documentation**:
   - Plan how to generate, store, and update documentation for each project and the tool itself. Consider implementing a way to auto-generate documentation from source code comments.

5. **Test Automation**:
   - Consider how you will automate testing for the tool, especially if it needs to interact with different environments or external tools like Docker, Node, or Git.

6. **Security and Permissions**:
   - Ensure the script respects user permissions, especially when accessing or modifying sensitive directories (e.g., home directories, `~/.git`).

7. **Command Aliases Storage**:
   - Determine where command aliases will be stored (e.g., home jasper folder or system jasper folder).

---

This roadmap provides a structured approach to building jasper, focusing on establishing core functionality first before expanding to more advanced features. The modular design allows for incremental development and testing.
