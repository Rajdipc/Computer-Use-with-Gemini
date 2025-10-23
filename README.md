# Gemini Computer Use: Web Automation Agent

This repository contains a Python script that demonstrates how to build a simple web automation agent using the Gemini Computer Use model from Google's Generative AI SDK. The agent can understand natural language prompts, "see" a web page via screenshots, and interact with it using mouse and keyboard actions.

The example uses Playwright to create a controlled browser environment and automates tasks like navigating websites and interacting with UI elements based on a user's goal.


## What is Computer Use model and tool?

The Gemini 2.5 Computer Use model and tool lets you enable your applications to interact with and automate tasks in the browser. Using screenshots, the computer use model can infer information about a computer screen, and perform actions by generating specific UI actions like mouse clicks and keyboard inputs. Similar to function calling, you need to write the client-side application code to receive the Computer Use model and tool function call and execute the corresponding actions.

Check: https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use


## Overview

The core of this project is the "agent loop," a cycle where the agent:
1.  **Observes:** Takes a screenshot of the current web page.
2.  **Thinks:** Sends the user's goal and the screenshot to the Gemini model, which then decides on the next action (e.g., click a button, type text).
3.  **Acts:** Executes the action suggested by the model using Playwright.

This loop continues until the user's goal is achieved. The script first walks through a single turn of this loop and then implements a complete, multi-turn agent.

## Features

- **Natural Language Control:** Give high-level goals to the agent in plain English (e.g., "Find me a flight from SF to Hawaii").
- **Vision-Enabled:** The agent uses screenshots to understand the current state of the user interface.
- **Agentic Loop:** Implements a continuous `(observe, think, act)` loop to perform multi-step tasks.
- **Function Calling:** Uses Gemini's function calling capabilities to translate its intent into concrete browser actions.
- **Secure & Headless:** Runs in a sandboxed, headless browser environment for safety and automation.

## Prerequisites

Before you begin, ensure you have the following:

- Python 3.9+
- A Google Cloud project with the Vertex AI API enabled.
- Authenticated your environment with Google Cloud. For local development, you can run:
  ```sh
  gcloud auth application-default login
  ```

## Installation

1.  **Clone the repository or download the script.**

2.  **Install the required Python libraries:**
    ```sh
    pip install google-genai playwright
    ```

3.  **Install Playwright browsers.** This command downloads the browser binaries required by Playwright.
    ```sh
    playwright install
    ```
    On Linux, you may also need to install OS dependencies:
    ```sh
    playwright install-deps
    ```

## Configuration

Open the script and update the `PROJECT_ID` variable with your Google Cloud project ID:

```python
# ...

# fmt: off
PROJECT_ID = "[your-project-id]"  # @param {type: "string", placeholder: "[your-project-id]", isTemplate: true}
# ...
```

## Usage

The script is designed to be run in an environment that supports top-level `await`, such as a Jupyter notebook or IPython. However, you can also run it as a standard Python script by making a small modification.

