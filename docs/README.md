---
title: BeeAI Workshop
description: Learn how to use and demo BeeAI
logo: images/ibm-blue-background.png
---

# Introduction

Welcome to our workshop! In this workshop we'll be using the open-sourced [BeeAI](https://beeai.dev) for a number of use cases that
demonstrates the value of [generative AI](https://developer.ibm.com/generative-ai-for-developers).

In this workshop you will:

Lab 1:

* Create an ACP agent using the BeeAI Framework and ACP SDK
* Create an ACP agent using the PydanticAI framework and ACP SDK
* Invoke your ACP agents using a curl command or the OpenAPI UI

Lab 2:

* Run the BeeAI Platform and see your agents auto-register
* Invoke your agents using the BeeAI Platform UI

Lab 3:

* Create a new agent to orchestrate the 2 existing agents
* for the 2 existing agents change the ports? (done earlier)
* add client function that calls the agents from different servers.
Open questions 1 file or 3 separate ones
* Add from repo?

How to Register an ACP agent to the BeeAI Platform (so you can test, run, and share your agent)

How to use your agent on the BeeAI platform

Scenario:

You will build a customer service triage process where a ticket comes in and
an ACP agent categorizes the ticket and extracts key insights from it.
Then it will hand it off to another ACP Agent that crafts a tone-specific response
to the customer.

## Agenda

|                                                  |                                                      |
|:-------------------------------------------------|:-----------------------------------------------------|
| [Lab 0: Pre-work](pre-work/README.md)            | Pre-work for the workshop                            |
| [Lab 1: Create agents with ACP](lab-1/README.md) | Create and invoke ACP agents                         |
| [Lab 2: Use the BeeAI Platform](lab-2/README.md) | Run the BeeAI Platform and use your agents in the UI |
| [Lab 3:](lab-3/README.md)                        | Learn how to...                                      |
| [Lab 4:](lab-4/README.md)                        | Learn how to...                                      |

## Technology Used

The technology used in the workshop is as follows:

* TODO: links
* ACP
* BeeAI Framework
* BeeAI Platform
* uv
* FastAPI / OpenAPI
* MCP?
* Models used?
* Providers used?
