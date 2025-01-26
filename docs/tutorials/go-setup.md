# Setting Up a Dev Container for Go

- **Primary Author:** [Sujay Patel](https://github.com/SUJP123)  
- **Reviewer:** [Ansh Desai](https://github.com/anshdesai04)

---

## Introduction

This guide walks you through setting up a basic Go project while using a development container and a Git repository. This project assumes no prior experience to actually using Go and will serve as a beginner friendly tutorial in which the goal is to simply print “Hello, COMP423.”

## Prerequisites

Ensure the following tools are installed before starting:

1. [VS Code](https://code.visualstudio.com/docs/setup/setup-overview)  
    - [VS Code Dev Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)  
2. [Docker](https://docs.docker.com/desktop/setup/install/mac-install/)  
3. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)  

Once you have these tools, you’re ready to begin!

## 1. Creating a Project Directory and Initializing Git

1. Open your terminal and run the following commands with your desired project name (here we use "hello-comp"):

    
    `mkdir hello-comp`  
    `cd hello-comp`  
    `git init`  
    
2. Open your project in VS Code to proceed with the tutorial.

## 2. Adding a GitHub Repository

1. On GitHub, create a new remote repository with public visibility.  
2. In your project terminal, link the local repository to GitHub:

```
    git remote add origin https://github.com/<username>/<repository-name>
```

Replace `<username>` and `<repository-name>` with your GitHub username and the repository’s name.

## 3. Setting Up a Dev Container

 1. Create a `.devcontainer` directory within your project:

    `mkdir .devcontainer`  

 2. Inside `.devcontainer`, create a `devcontainer.json` file:  

    `touch .devcontainer/devcontainer.json`  

 3. Add the following configuration to the `devcontainer.json` file:  

```
    {
        "name": "Go Dev Container",
        "image": "mcr.microsoft.com/vscode/devcontainers/base:ubuntu",
        "features": {
            "ghcr.io/devcontainers/features/go": {}
        },
        "customizations": {
            "vscode": {
            "extensions": [
                "golang.go"
            ]
            }
        },
        "mounts": [
            "source=/var/run/docker.sock,target=/var/run/docker.sock,type=bind"
        ]
    }
```
 4. In VS Code, click the `Reopen in Container` button that appears. If it doesn't appear,
 try holding down `Command-Shift` and pressing `p` twice and type in `Dev Containers: Reopen in Container` at the top of the VS Code page.

 5. Verify that Go is installed by running the following:

    `go version`

    - Your terminal should read something similar to this:  
    `go version go1.23.5 linux/arm64`

## 4. Starting the Go Project

1. Inside your project's dev container, run the following to create a go.mod file:  
    `go mod init github.com/<username>/<repository-name>`

    Replace `<username>` and `<repository-name>` with your GitHub username and the repository’s name.

2. Create a file called main.go in your projects root directory:

    `touch main.go`

3. Type the following code in your `main.go` file:

```
    package main

    import "fmt"

    func main() {
        fmt.Println("Hello, COMP423.”)
    }
```

## 5. Compiling and Running the Project

1. Compile the project and run the executable file with the following command:

    `go run main.go`

    The `run` command will compile and execute the code without additionally creating a binary file. It is the equivalent to running `go build -o <file-name>` and `./<file-name>` without having to create `<file-name>` itself. You may think of the `go build` command as similar to `gcc` as they both function to compile code into an executable file.

2. So alternatively, you may run the following commands:
    
    `go build -o "go-project"`

    `./go-project`

3. You should see the following output:

    `Hello, COMP423.`

## 6. Pushing Your Hard Work to Github

1. Configure your username and password for git if not done already:

    `git config user.name --global "your-github-username"`  
    `git config user.email --global "your-email"`

2. Add a `README` file if desired:

    `echo "My First Go Project" > README.md`

3. Stage your files:

    `git add .`

4. Commit your staged files:

    `git commit -m "your-commit-message"`

5. Push your files:
    `git push -u origin main`

    - If you're using an older version of git, your branch may be named `master` instead of `main`. You can change it with the following command:
        `git branch -M main`


Congrats on completing your first Go Project!