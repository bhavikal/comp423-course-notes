# Setting Up a Dev Container for Go

* Primary author: [Bhavika Lingutla](https://github.com/bhavikal)
* Reviewer: [Shayna Patel](https://github.com/shaynapat3l)

!!! note
    This tutorial reuses instructions from the [COMP 423 MkDocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/).

### Introduction

After completing this tutorial, you will learn how to:

* Set up a basic Go Development Container in VS Code to streamline development.
* Initialize and configure a GitHub repository.
* Gain insight into the tools and practices used in open-source and professional software projects.

### Prerequisites

Before starting, make sure you have:

1. **A GitHub account**: Sign up at [GitHub](https://github.com).
2. **Git**: Install from [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
3. **Visual Studio Code (VS Code)**: Download and install from [here](https://code.visualstudio.com/).
4. **Go VSCode Plugin**: Install from [here](https://marketplace.visualstudio.com/items?itemName=golang.go).
5. **Docker installed**: Required to run the dev container. [Get Docker here](https://www.docker.com/products/docker-desktop).
6. **Knowledge of command-line basics**.

# Part 1. Project Setup: Creating the Repository

## Step 1: Create a Local Directory and Initialize Git

1. Open your terminal.

2. Create a new directory for your project and change into it:
```
mkdir go-dev-container-tutorial
cd go-dev-container-tutorial
```

3. Initialize a new Git repository:
```
git init
``` 

4. Create a README file:
```
echo "# Hello World in Go" > README.md
echo "To view the entire tutorial, visit my Course Notes site at https://github.com/bhavikal/comp423-course-notes/blob/main/docs/tutorials/go-setup.md." >> README.md
git add README.md
git commit -m "Initial commit with README"
```

## Step 2: Create a Remote Repository on GitHub

1. Log in to your GitHub account and go to the [Create a New Repository](https://github.com/new) page.

2. Fill in the details of the repository as shown below:

* **Repository Name**: go-dev-container-tutorial
* **Description**: "A tutorial on how to set up a dev container using Go."
* **Visibility**: Public

3. Do not initialize the repository with a README, .gitignore, or license.

4. Click **Create Repository**

## Step 3: Link your Local Repository to GitHub

1. Add the GitHub repository as a remote:
```
git remote add origin https://github.com/<your-username>/go-dev-container-tutorial.git
```
Replace ```<your-username>``` with your GitHub username.

2. Check your default branch name with the subcommand ```git branch```. If it is not ```main```, rename it to ```main``` with the following command: ```git branch -M main```. 

3. Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```
4. In your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote.
!!!tip
    You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

# Part 2. Setting up the Development Environment

## Step 1. Add Development Container Configuration

1. In VS Code, open the go-dev-container-tutorial directory. You can do this by going to: File > Open Folder

2. Install the **Dev Containers** extension for VS Code.

3. Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuration directory:
```
.devcontainer/devcontainer.json
```
The ```devcontainer/devcontainer.json``` file outlines the configuration for your development environment. The following is specified:
* ```name```: A descriptive name for your dev container.
* ```image```: The Docker image to use, in this case, the latest version of a Go environment.
* ```customizations```: Adds useful configurations to VS Code, like installing the Python extension. 

Add the following to your .devcontainer/devcontainer.json file:

```
{
  "name": "Go Dev Container",
  "image": "mcr.microsoft.com/devcontainers/go:1.20",
  "customizations": {
    "vscode": {
      "settings": {
        "go.gopath": "/go",
        "go.goroot": "/usr/local/go"
      },
      "extensions": [
        "golang.go"
      ]
    }
  }
}
```

## Step 2. Reopen the Project in a VSCode Dev Container

Reopen the project in the container by pressing ```Ctrl+Shift+P``` on Windows or ```Cmd+Shift+P on Mac```, typing in "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal within VSCode, and try running ```go version``` to see your dev container is running a recent version of Go without much effort!

# Part 3: Writing a Go Program

## Step 1: Initialize a Go Module

1. **Initialize a Go module**:
```
go mod init github.com/<your-username>/go-hello-world
```
This sets up Go's dependency management system for your project. Make sure to replace ```<your-username>``` with your GitHub username.

## Step 2: Write a Hello World Program

1. **Create a ```main.go``` file in your root directory**:
```
package main
import "fmt"
func main() {
    fmt.Println("Hello COMP423")
}
```

2. **Run or build the program**:
!!!note
    There are two ways to run our Hello World program. The first is by using the run subcommand, and the second is by using the build subcommand. If you choose to use the build command, make sure to run the built binary as well.

**Run the program**:
```
go run main.go
```
This compiles and runs the Go program, indicating that it works.

OR

**Build the program**:
```
go build -o bin/hello-world
```
This compiles the program into an executable binary file. Build is similar to gcc, as we learned in COMP 211.

**Run the built binary**:
```
./bin/hello-world
```
This runs the compiled binary, demonstrating how to build and run Go programs.

## Step 3: Push Changes and Deploy

1. **Stage your changes**:
```
git add .
```

2. **Commit your changes**:
```
git commit -m "Go Hello World program"
```

3. **Push your changes to GitHub**:
```
git push origin main
```