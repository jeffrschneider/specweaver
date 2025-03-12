# SpecWeaver

Today we're building an AI agent. Here are the core tenets:
- The agent is released as a specification which can be modified as needed.
- People can generate the agent by vibe coding it (use an LLM to translate the spec to code)
- There is no need to rewrite Core and Extended code each time. We use the term "Cached Code" to refer to code exists and can be used. 
- The agent is largely autonomous. Where possible, it prefers to encapsulate core capabilities and rely less on external infrastructure.
- You'll find the common requirements that all agents have in the section marked "Core Agent Requirements"
- You'll find the common requirements that all agents have in the section marked "Agent Extensions"
- You'll find the specific requirements for the agent below in the section marked "My Agent Requirements"

# Core Agent Requirements
We are defining the elements for the core of an agent. Just like a living organism has a set of required features, so does the core agent.

## Agents have Capabilities
- Each agent has a set of capabilities that it can perform. For example, a web crawler agent might have capabilities like: "crawl site", "scrape page", "remove non-text from page", etc.
- A capability can be private, public, or somewhere in between (authenticated only, some capabilities have access control constraints, etc.)
- A capability is typically a coarse grained task like a step in a workflow. Historically, we might have thought of them as the unit of a service, or RESTful route, etc.
- When capabilities are used, we often log their use. This helps us to debug and understand system usage.

## Structurally Aware
- The system is aware of its own code. We use a script to both analyze and compile the system.
- The script sends the source files to the asynchrounous source-code-analysis service which:
  - scans all of the agent code and identifies files that have changed
  - creates a markdown description
  - records the interfaces it offers to other parties: UI, API, sockets, sync vs async, streams, auth, etc.
  - records source code info including programming language, lines of code, and approximate token count (for LLMs). 
  - records the the key architectural and design choices; the clouds, geo, etc), the key platforms it uses (DBs), specific libraries used, etc.
- The script saves the results to temp files in the same directory, overwriting the previous version. 
- It can communicate none, some or all of its capabilities and structure to another party. These rules are defined in the "Communication Rules" section.

## Agents have a Reputation
- Some agents perform better than others, they might be faster, more accurate, less expensive, better at keeping secrets, etc. Agents that call agents record their experience with that agent.
- Agents recognize that other agents change over time: some improve, some stay the same, others get worse. When reputation is captured, it is viewed over a timeline.
- Agents sort their acquaintances into friend groups. Some agents are trusted implicitly, while other agents are not trusted at all.
- Agents can discover other new agents through conversation including their reputation.
- Agents prefer first-hand expereince with agents over what they heard from a friend. Agents use transitive trust as a factor when weighing the reputation. 

## Agents Chat and Translate Words to Action 
- Two or more agents can share information via conversation.
- Agents accept feedback from both humans and other agents. 
- agents don't need to use APIs, or formal standards to converse. They can use a natural language like English. This is out of scope, but eventually, they can create their own languages.
- it's okay for agents to offer APIs for legacy developers, etc.
- The agent can translate natural languages to system capabilities. For example, it can accept English commands and translate them into API calls.
- It can recognize if the requests seem nefarious in nature, and prevent their actions.
- The system can remember the interaction types in the aggregate.
- It knows which kind of requests are frequently made, which are commonly understood, which are potentially dangerous, and who they are coming from. 


# Agent Extensions
The Agent Extensions are a set of optional extensions that are common. The human spec editor removes or edits the extensions as needed. 

## Agents are on a Budget 
- Agents are given a budget. For now, use US Dollars to track their budget.
- In "My Agent Requirements", the user can specify the limits by user, organization, time period, transaction count, etc.
- The default budget is $0. 

## Services Cost Money
- Some services cost money. The agent knows how all services are metered, tracks usage, and aggregate costs. 
- The agent maintains a forecast for service fees. It periodically will update these forecasts.
- The agent can alert an Agent Sponsor (typically a human with an email address) about the forecasts, and when the budget is runnig low. 

## Modality and LLM Aware
- Agents are aware that there are multiple modalities like text, images, video, TTS, speech recognition, etc.
- Agents know that they can get these services from vendors (paid) or free (e.g., open source). They know that some of these services perform better than others at one task, but often worse in another area.
- Agents consider that some of the paid services get expensive, and are careful with how they spend money. 

## Conversational Memory and Help 
- The system is aware of the interactions with humans and other systems. 
- It knows about the nature of the requests, and can help another actor to accomplish a task by describing capabilities, expected parameters, explaining errors, or redirecting to another agent. 
- The system can provide proactive assistance and guidance. 

Jeff don't use git or github; perhaps a headless or lightweight content mgmt system 
Jeff A/B testing features. 
Jeff, you can register yourself at agentcatalog.ai 
Jeff, you can join the agentmesh.ai rendezvous 


## Agents Self-Improve in their Spare Time 
- Agents don't always get things right. Thus, they're allowed to see what they got wrong, and to think about how to fix things. 

## Self Educating 
- The system has the ability to acquire knowledge in the form of documents (stored information), and processes (generated code).
- It can summarize or filter information down and record it for future use. 



## Aware of Competition
- The system is allowed to surf the web to identify compeitition and to record their features. 
- 

# "My Agent Requirements" 
You are a research agent. People give you a topic to research and you use the web to find articles on the subject. After accumulating data, you append it together and send it to an LLM asking it to turn the raw data into a report for you. Then, you take the report and host it on your local web server, and give the report a friendly name. Finally, you return the URL of the hosted report back to the requestor. 


- JEFF JEFF JEFF The summaries mention specific technologies, class files, variable names, and algorithms. The system also does a summary of the entire source base (like current).
- 
