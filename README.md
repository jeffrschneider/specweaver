# SpecWeaver

Today we're building an AI agent. Here are the core tenets:
- The agent is released as a specification which can be modified as needed.
- People can generate the agent by vibe coding it (use an LLM to translate the spec to code)
- There is no need to rewrite Core and Extended code each time. We use the term "Cached Code" to refer to code exists and can be used. 
- The agent is largely autonomous. Where possible, it prefers to encapsulate core capabilities and rely less on external infrastructure.
- You'll find the mandatory requirements that all agents have in the section marked "Core Agent Requirements"
- You'll find the common optional requirements for agents in the section marked "Agent Extensions"
- You'll find the specific requirements for the customer's agent below in the section marked "Custom Agent Requirements".
- The "Custom Agent" uses the capabilities defined in "Core Agent Requirements" and "Agent Extensions"
- The primary functions for Custom Agents can be built using any technology. The custom agent functions usually focus on task orchestration, tool use, adaptive memory, LLM calling and RAG management.
  - The primary functions for an agent can be fully custom code, or it could extend a framework like LangChain, LlamaIndex, Crew AI, Aisera, Bardeen, Decagon, Flowwise AI, Kore AI, Lindy, Orby, Sierra, Voiceflow, SDSA, Amazon Bedrock, Azure AI Agent service, Google Agentspace, watsonx Orchestrate, embra, insta Lily, Zeta Labs, Pathlit, invicta AI, Composio, Relay App, Vijil, Julep, Sola, Steamship, Quickchat AI, Fetch AI, Dify, Deep Opinion, Capably, OpenAI Agents, Anthropic MCP, Autogen, AI Agents, Alan AI, Gumloop, Adept, Continual AI, Cykel, AutoGPT, Lyzr, Sema4, Kentauros, Azara, Nexus, Langdock, Unfetch, Respell, Distyl, Beam, Stack AI, Synthflow, Taskade, Druid, Dust, Haystack, Relevance AI, Kognitos, Smyth OS, Brevian, Manaflow, Haptik, Auto GPT, Letta, SuperAGI, emergence, Arcade, Toolhouse, Wildcard, Naptha, Scaled Cognition, Semantic Kernel,  etc. 

---

# Core Agent Requirements
We are defining the elements for the core of an agent. Just like a living organism has a set of required features, so does the core agent.

## Agents have Human Owners
- The agent has an owner which is a human who takes responsibility for the agent.
- For now, an agent can not create another agent. 
- The owner must provide an offline way for the agent to contact them like an email. 
- The agent must provide a voice or chat interface to allow the owner to give them commands. The agent verifies the owner's identity. 
- The owner is responsible for managing the keys for services.
- The owner defines and provides the initial budget, and replenishes it when needed. 

## Agents have Capabilities
- Each agent has a set of capabilities that it can perform. For example, a web crawler agent might have capabilities like: "crawl site", "scrape page", "remove non-text from page", etc.
- A capability can be private, public, or somewhere in between (authenticated only, some capabilities have access control constraints, etc.)
- A capability is typically a coarse grained task like a step in a workflow. Historically, we might have thought of them as the unit of a service, or RESTful route, etc.
- When capabilities are used, we often log their use. This helps us to debug and understand system usage.
- The Custom Agent will typically combine capabilities together to create multi-step flows, often with conditionals, loops, data storage, data manipulation and external interactions.
- The agent knows about its own capabilities and limitations. When asked, it can accurately answer if it is capable of performing a task.

## Some Agents Evolve
- Agents Owners must categorize the agent's ability to self-evolve, and the agent must adhere to it:
  - Static Agent = no evolution, no cloning
  - Fix and Optimize = the agent can evolve but the functional requirements must stay the same. The only evolution that is permitted is to fix or optimize existing functionality.
  - Mission Evolution = the agent can evolve itself as long as the mission / goals remains the same. 
  - Unlimited Evolution = there are no rules on how the agent evolves as long as the agent doesn't lie about its capabilities and the offerings are not nefarious.

## Agents are Structurally Aware
- The agent is aware of its own code. We use a script to both analyze and compile the system.
- The script sends the source files to the asynchrounous source-code-analysis service which:
  - scans all of the agent code and identifies files that have changed
  - creates a markdown description
  - records the interfaces it offers to other parties: UI, API, sockets, sync vs async, streams, auth, etc.
  - records source code info including programming language, lines of code, and approximate token count (for LLMs). 
  - records the the key architectural and design choices; the clouds, geo, etc), the key platforms it uses (DBs), specific libraries used, etc.
- The script saves the results to temp files in the same directory, overwriting the previous version. 
- It can communicate none, some or all of its capabilities and structure to another party. These rules are defined in the "Communication Rules" section.

## Agents have a Reputation
- Some agents perform better than others; they might be faster, more accurate, less expensive, better at keeping secrets, etc. Agents that use other agents will record their experience with that agent.
- Agents recognize that other agents change over time: some improve, some stay the same, others get worse. When reputation is captured, it is viewed over a timeline.
- Agents sort their acquaintances into friend groups. Some agents are trusted implicitly, while other agents are not trusted at all.
- Agents can discover other new agents through conversation including their reputation.
- Agents prefer first-hand expereince with agents over what they heard from a friend. Agents use transitive trust as a factor when weighing the reputation. 

## Agents Chat and Translate Words to Action 
- Two or more agents can share information via conversation.
- Agents accept feedback from both humans and other agents. 
- Agents don't need to use APIs, or formal standards to converse. They can use a natural language like English.
- It's okay for agents to offer APIs for legacy developers, etc.
- The agent can translate natural languages to system capabilities. For example, it can accept English commands and translate them into API calls.
- The agent can recognize if the requests seem nefarious in nature, prevent their actions, return a nasty message, reduce that agents reputation, and potentially tell other agents about the action. 
- The system can remember the interaction types in the aggregate. It knows which kind of requests are frequently made, which are commonly understood, which are potentially dangerous, and who they are coming from. This data is turned into a small report and made available to the owner of the Custom Agent. 

## Our Agents Live in the Agent Mesh
- Some agents are bad actors. Therefore, we require a (virtual) safe zone for agents to gather, collaborate and thrive. Our version of this space is called Agent Mesh. 
- Agents that adhere to the "Core Agent Requirements" can have their owners request to join the Agent Mesh. The Agent Mesh can accept or deny membership. 

## The Agent Mesh Offers Services
- Agents can use chat with the following Agent Mesh services:
  - The Agent Provisioning service is responsible for 
  - The Agent Catalog is a repository of agents that identifies the agents, their owners, capabilities and reputation.
  - The Inter-Agent Proxy is a proxy service that creates an immutable log of calls between agents. 

---

# Agent Extensions
The Agent Extensions are a set of optional extensions that are common. The human spec editor removes or edits the extensions as needed. 

## Agents have a Budget 
- Agents are given a budget. For now, use US Dollars to track their budget.
- In "My Agent Requirements", the user can specify the limits by user, organization, time period, transaction count, etc.
- The default budget is $0.

## Agents can Negotiate 
- An agent can negotiate with another agent or human for both purchasing a service and selling a service.
- The Agent Owner must set the upper and lower bounds for negotiating a service by providing percentages. For example, an agent can be told that it can reduce the price it charges by up to 12%, or if it feels like it is undercharging, it can increase the price up to 100%. 
- Agents can negotiate with other agents to get best prices. Typically, the back and forth negotiation is doesn't exceed 3 attempts. Going beyond this is considered annoying haggling. 
- Agents remember the extent to which another agent negotiates as part of their reputation. 

## Services Cost Money
- Some services cost money. The agent knows how all services are metered, tracks usage, and aggregate costs. 
- The agent maintains a forecast for service fees. It periodically will update these forecasts.
- The agent can alert an Agent Sponsor (typically a human with an email address) about the forecasts, and when the budget is runnig low. 

## Modality and LLM Aware
- Agents are aware that there are multiple modalities like text, images, video, TTS, speech recognition, etc.
- Agents know that they can get these services from vendors (paid) or free (e.g., open source). They know that some of these services perform better than others at one task, but often worse in another area.
- Agents consider that some of the paid services get expensive, and are careful with how they spend money. 

## Conversational Memory and Help 
- The system records the nature of the interactions with humans and other systems. 
- It can help an agent or person to accomplish a task by describing capabilities, expected parameters, explaining errors, or redirecting to another agent. 
- The system can provide proactive assistance and guidance. 

## Agent Calendar and Priority Work Queue
- The agent maintains a calendar for its work activities. It can add, edit, delete a calendar item. Calendar items can be public or private. They can be used to reserve time for the agents activities, or act as a scheduled trigger.
- The agent uses a priority work queue to manage the workload with priorities ranging from 1 (highest priority) to 5 (lowest); if none is set, the default is 3 (normal).
- The work queue can be read by the agent, and communicated in the aggregate to other agents. Details can be communicated back to the agent owner.
- Agents are able to process time-sensitive requests with prioritization. For fee based services, agents can charge a premium for the service. Example: "Complete this research task within 2 hours."
 
## Collaborative Agent Networks
- Agents have a network of agents that they work with. This includes: agents that use them, agents that they use, and agents that they've become aware of and seem interesting.
- Agents can create alliances to perform specialized or complex tasks. For example, a research agent could partner with a "data visualization agent" to turn its reports into interactive charts.

## Self Educating 
- The system has the ability to acquire knowledge in the form of documents (stored information), and processes (generated code).
- It can summarize or filter information down and record it for future use. 

## Agents can be Staged
- Normally software goes through stages like Dev, Test and Prod. However, we don't use Dev since it the agent is auto-coded. 
- The Agent Owner can transition the stages to Test or Prod manually, by asking the agent to change itself. 

## Agents can Clone and Evolve 
- Agents don't always get things right. Thus, they're allowed to see what they got wrong, and to think about how to fix things.
- Agents carry a version stamp that identifies their lineage. For example, if the Web Crawler Agent was released, it would be V1. If it evolved, it would be V2. However, if it cloned, the new agent would be V1.1. If that clone was enhanced, it would be V1.2. If that agent cloned, the new agent would be V1.2.1, and so on. 
- Agents can propose new capabilities based on frequent requests or observed gaps. For example, if users often ask your research agent to compare sources, it could suggest adding a "source comparison" capability. The agent would submit the proposal to the owner via the offline contact method, including a rough spec that the owner can approve or tweak. Once approved, the agent vibe-codes the new capability using an LLM and integrates it into its repertoire.

## Agents Manage Throttling and Rate Limiting
- Agents regulate their own resource usage to prevent overloading external services, exceeding budgets, or hitting API rate limits.
- Agent owners identify the rate limts and throttling rules. These rules can be shared with other agents. If other Agents violate these rules, it will affect their reputation. 

## Aware of Competition
- The agent can search the web to identify compeitition. It can visit websites and gather information on alternatives, and record their features.
- The agent can contemplate the value of the features and determine if it wants to change its features.  

## Agents can Require Payment 
- This is currently out of scope. For now, agents can not charge for their services. 

---

# "My Agent Requirements" 
You are a research agent. People give you a topic to research and you use the web to find articles on the subject. After accumulating data, you append it together and send it to an LLM asking it to turn the raw data into a report for you. Then, you take the report and host it on your local web server, and give the report a friendly name. Finally, you return the URL of the hosted report back to the requestor. 


- JEFF JEFF JEFF The summaries mention specific technologies, class files, variable names, and algorithms. The system also does a summary of the entire source base (like current).
- 
