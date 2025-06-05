---
title: BeeAI Workshop Lab 2
description: Create a ticket agent with triage and response
logo: images/ibm-blue-background.png
---

# Create a ticket agent with triage and response

In this lab, we'll create ticket agent that uses the triage agent and the response agent in a single workflow.

## Steps

1. Prerequisites

    * Stop the agents from Lab 1 (CTRL-C in each terminal window)
    * If not already done for Lab 1 set up the .env (see Lab 1)

2. Run the ticket (triage and response) agent using port 8000

    ```shell
    uv run src/agent.py
    ```

3. Use your browser to try the FastAPI interface

    * Browse to [http://localhost:8000/docs](http://localhost:8000/docs)
    * Pull down `GET` **/agents** *List Agents*
    * Hit the `Try it out` button and then click `Execute`

    > --- Expected results ---
    >
    > Under `Responses` you should see all 3 agents listed!
    >
    > * Try running the curl command (in a new terminal window)
    >
    >   ```shell
    >   curl -X 'GET' 'http://localhost:8000/agents' -H 'accept: application/json'
    >   ```

4. Invoke the triage agent

    * Go back to the main FastAPI page
    * Pull down `POST /runs Create Run`
    * Pull down `POST` **/runs** *Create Run*
    * Hit the `Try it out` button
    * In the `Request body`:

      * Find **"agent_name"** and change the value from "string" to **"TicketWorkflow"**
      * Find **"content"** and change the value from "string" to:

        ```text
        "Hi there, this is Jane Doe. Ever since yesterday your ProPlan won't let me export reports. This is blocking my quarter-end close—please fix ASAP or refund the month.AccountNumber: 872-55"
        ```

      * Remove the **"content_url"** line
      * Find **"mode"** and change the value from "sync" to **"stream"**

    * Click `Execute`

    > --- Expected results ---
    >
    > The TicketWorkflow, takes user input for the triage agent, sends the triage
    > results to the response agent, and responds to the user with the friendly response.