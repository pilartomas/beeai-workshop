---
title: BeeAI Workshop Pre-work
description: Preparation for the BeeAI Workshop
logo: images/ibm-blue-background.png
---

# Pre-work

## ACP

### Prerequisites to get started with ACP

#### Python '>=3.11

  - Go to [python.org/downloads](https://www.python.org/downloads/)
  - Download the version for your operating system (Windows, macOS, or Linux)

     > Important: During installation, make sure to check the box that says `Add Python to PATH` or manually if you skip this step

  - To verify installation type `python --version`

#### [Visual Studio Code](https://ibm.github.io/opensource-ai-workshop/pre-work/#installing-visual-studio-code) (Recommended)

  - You can use any IDE, but this workshop assumes you're using VS Code
  - If this is your first time using VS Code, make sure to install the Python extension from the extension marketplace

#### uv

  - uv is recommended for this workshop, but you can use uv, pip, or another package manager if you're more comfortable with them.
  - If you’re unfamiliar with uv, check out [this uv primer](https://agentcommunicationprotocol.dev/introduction/uv-primer) for installation instructions

### ACP Setup Prior to Starting the Workshop Code

1. Open VS Code and navigate to the directory where you want to create your new ACP project

2. Initialize a new project by running the following command in the terminal. This creates a new project folder named my_acp_project and sets it up with uv.

   ```shell
   uv init --python '>=3.11' my_acp_project 
   ```

3. Navigate into your new project directory

   ```shell
   cd my_acp_project
   ```

4. Add the ACP SDK as a dependency

   ```shell
   uv add acp-sdk
   ```

## BeeAI Platform

### Prerequisites to get started with BeeAI Platform

- [Homebrew](https://brew.sh/) (for macOS or Linux)
   - If you don’t already have Homebrew installed, run the following command in your terminal and follow the instructions to update your shell environment:

     ```shell
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

- [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) (for Windows users)

   - [Windows WSL2 setup instructions](https://docs.beeai.dev/introduction/installation#windows-wsl2-setup-instructions)

- LLM API Key or Ollama?

### BeeAI Platform setup prior to starting the workshop code

> Note: If using a Windows, open WSL2 by right-clicking the Start menu, selecting a terminal (e.g., PowerShell or Windows Terminal), and typing the `wsl` command. From there, run all the following installation commands inside the WSL shell, not the Windows shell.

1. Install BeeAI using Homebrew:

   ```shell
   brew install i-am-bee/beeai/beeai
   ```

1. Start the BeeAI background service:

   ```shell
   brew services start beeai
   ```

### Already have BeeAI installed? Update and restart it

   ```shell
   brew upgrade beeai
   brew services restart beeai
   ```

### Local Prerequisites

- Git
- Python 3.11 or 3.12

### Clone the BeeAI workshop repository

Clone the workshop repo and cd into the repo directory.

```shell
git clone https://github.com/IBM/beeai-workshop.git
cd beeai-workshop
```
