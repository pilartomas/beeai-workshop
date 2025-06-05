---
title: BeeAI Workshop Lab 1
description: Create and invoke ACP agents
logo: images/ibm-blue-background.png
---

# Create and invoke ACP agents

In this lab, you will create 2 agents using the ACP SDK (the Python code is provided).
One agent is written using the BeeAI Framework.  The other agent is written using PydanticAI.
We are using 2 frameworks to illustrate how easy it is to make any agent ACP-compatible.

* Agent 1 (BeeAI Framework): "Triage Agent" – categorizes the ticket (e.g. billing, tech, complaint) and extracts key facts in a structured way (e.g. using tags, severity, sentiment).
* Agent 2 (PydanticAI): "Response Agent" – takes the structured summary and crafts a tone-specific response (e.g. empathetic for complaints, efficient for billing).

## Steps

1. Prerequisites

    The described commands assume you are running from the beeai-workshop directory
    of your cloned repo. This was already done if you did the pre-work.

    ```shell
    git clone https://github.com/IBM/beeai-workshop.git
    cd beeai-workshop
    ```

2. Install the dependencies

    ```shell
    uv sync
    ```

3. Set up your .env file with your OpenAI API Key

   * Copy the `env.template` file to `.env`.

     ```shell
     cp env.template .env
     ```

   * Edit the `.env` file to add your OpenAI API key.  The file should look like below
   (the API key in example is fake and shorter than a real one). The OPENAI_BASE_URL shown is for groq.

     ```shell
     # Example for groq:
     OPENAI_API_KEY=<your-groq-api-key>
     OPENAI_BASE_URL=https://api.groq.com/openai/v1
     MODEL_NAME=meta-llama/llama-4-scout-17b-16e-instruct
     ```

4. Run the ticket triage agent (defaults to run on port 8000)

    ```shell
    uv run src/ticket_triage_agent.py
    ```

5. Run the ticket response agent using port 8001

    ```shell
    PORT=8001 uv run src/ticket_response_agent.py
    ```

6. Use your browser to try the FastAPI interface

    * Browse to [http://localhost:8000/docs](http://localhost:8000/docs)
    * Pull down `GET` **/agents** *List Agents*
    * Hit the `Try it out` button and then click `Execute`

    > --- Expected results ---
    >
    > Under `Responses`:
   >
    > * Under `Response body`, the result shows just one agent named `ticket_triage_agent` (the second agent is not running on port 8000).
    > * Under `Curl`, you get the curl command that you can run in a terminal (instead of using the UI)
    > * Try running the curl command (in a new terminal window)
    >
    >   ```shell
    >   curl -X 'GET' 'http://localhost:8000/agents' -H 'accept: application/json'
    >   ```

7. Invoke the triage agent

    * Go back to the main FastAPI page
    * Pull down `POST` **/runs** *Create Run*
    * Hit the `Try it out` button
    * In the `Request body`:

      * Find **"agent_name"** and change the value from "string" to **"ticket_triage_agent"**
      * Find **"content"** and change the value from "string" to:

        ```text
        "Hi there, this is Jane Doe. Ever since yesterday your ProPlan won't let me export reports. This is blocking my quarter-end close—please fix ASAP or refund the month.AccountNumber: 872-55"
        ```

      * Remove the **"content_url"** line
      * Find **"mode"** and change the value from "sync" to **"stream"**

    * Click `Execute`

   > --- Expected results ---
   >
   > Under `Responses`:
   > * Under `Response body`, the result shows just one agent named `ticket_triage_agent` (the second agent is not running on port 8000).
   > * Under `Curl`, you get the curl command that you can run in a terminal (instead of using the UI)
   > * Try running the curl command (in a new terminal window)

8. Invoke the response agent

   * Try this curl command (notice the port is **8001**)

     ```shell
     curl -N -X POST http://localhost:8001/runs \
     -H "Content-Type: application/json" \
     -H "Accept: text/event-stream" \
     -d '{"agent_name":"ticket_response_agent","input":[{"parts":[{"content":"{\"category\":[\"Technical\"],\"customer_name\":\"Jane Doe\",\"account_id\":\"872-55\",\"product\":\"ProPlan\",\"issue_summary\":\"ProPlan product is throwing \\\"Error 500\\\" when exporting reports since yesterday, blocking quarter-end close.\",\"severity\":\"high\",\"sentiment\":\"negative\",\"incident_date\":\"2024-06-11\"}","content_encoding":"plain","content_url":null}]}],"mode":"stream"}'
     ```

   > --- Expected results ---
   >
   > In the response body, you should see an appropriate human-like ticket agent response

   * (OPTIONAL) Try repeating the FastAPI steps but this time use port 8001 to see the API for the response agent API

     > Note: The input format is tricky so maybe just compare the schema with the above curl. We'll make this much easier in the next lab.
     >
     > Hint:
     >
     > ```json
     > "content": "{\"category\":[\"Technical\"],\"customer_name\":\"Jane Doe\",\"account_id\":\"872-55\",\"product\":\"ProPlan\",\"issue_summary\":\"ProPlan product is throwing \\\"Error 500\\\" when exporting reports since yesterday, blocking quarter-end close.\",\"severity\":\"high\",\"sentiment\":\"negative\",\"incident_date\":\"2024-06-11\"}",
     > ```
