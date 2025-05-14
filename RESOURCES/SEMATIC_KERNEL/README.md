# Understand the Semantic Kernel Agent Framework

Completed
100 XP
6 minutes

Semantic Kernel is an open-source SDK that enables developers to integrate AI models into their applications. Part of that SDK is the Semantic Kernel Agents Framework, enabling the creation of agents using the same features that exist in the core Semantic Kernel framework.

## What is the Semantic Kernel Agent Framework?

The Semantic Kernel Agent Framework is a framework designed to help developers build AI-powered agents. These agents can process user inputs, make decisions, and execute tasks autonomously by leveraging large language models and traditional programming logic. The framework provides structured components for defining AI-driven workflows, enabling agents to interact with users, APIs, and external services.

### Core concepts

The Agent Framework in Semantic Kernel provides architecture on top of existing Semantic Kernel resources, including:

#### Agents

Agents are intelligent, AI-driven entities capable of reasoning and executing tasks. They use language models, functions, and memory to make decisions dynamically.

#### Agent collaboration

Agents can collaborate together through an agent group chat, which enables multiple agents to join the same chat, even of different agent types. Agent group chats determine which agent should respond and how to determine if the conversation is finished.

The features that power Semantic Kernel are also still available within the Agent Framework, including:

#### Kernel

The kernel is the central component of the Semantic Kernel. The kernel acts as the execution engine, managing AI interactions, function orchestration, and memory.

#### Tools and plugins

Plugins align with existing Semantic Kernel features, enabling agents to dynamically interact with external services or execute complex tasks through function calling. Within the Agent Framework, tools are available to provide extra functionality to your agents, such as file searching or code interpreter, similar to tool usage in Azure AI Agent service. Agents use tools and plugins to perform specific tasks.

#### History

Agents can maintain chat history across multiple interactions, allowing them to track previous interactions and adapt responses accordingly. The conversation history is always accessible by the agents, either as a whole or for a specific agent's chat history.

### Types of agents

The Semantic Kernel Agent Framework supports several different types of agents, including:

- **Azure AI Agent**: a specialized agent within the Semantic Kernel Agent Framework. The AzureAIAgent type is designed to provide advanced conversational capabilities with seamless tool integration. It automates tool calling and securely manages conversation history using threads, reducing the overhead of maintaining state. The AzureAIAgent also supports a variety of built-in tools, including file retrieval, code execution, and data interaction via Bing, Azure AI Search, Azure Functions, and OpenAPI.

- **Chat Completion Agent**: designed for chat completion and conversation interfaces. The ChatCompletionAgent type mirrors the features and patterns in the underlying AI Service to support natural language processing, contextual understanding, and dialogue management.

- **OpenAI Assistant Agent**: designed for more advanced capabilities and multi-step tasks. The OpenAIAssistantAgent type supports goal-driven interactions with additional features like code interpretation and file search.

### Why you should use the Semantic Kernel Agent Framework

The Semantic Kernel Agent Framework offers a robust platform for building intelligent, autonomous, and collaborative AI agents. The framework can integrate agents from multiple sources, including Azure AI Agent Service, and supports both multi-agent collaboration and human-agent interaction. Agents can work together to orchestrate sophisticated workflows, where each agent specializes in a specific task, such as data collection, analysis, or decision-making. The framework also facilitates human-in-the-loop processes, enabling agents to augment human decision-making by providing insights or automating repetitive tasks. This combination of autonomy, collaboration, and interactivity makes the Semantic Kernel Agent Framework an ideal choice for applications requiring dynamic, goal-oriented behavior.

## Define a Chat Termination Strategy

Completed
100 XP
6 minutes

Multi-turn conversations have responses returned asynchronously, so the conversation can develop naturally. However, the agents need to know when to stop a conversation, which is determined by the termination strategy.

### Termination strategy

A termination strategy ensures that conversations or tasks conclude appropriately. This strategy prevents unnecessary messages to the user, limits resource usage, and improves the overall user experience.

For example, in the writer-reviewer agent scenario, once the ReviewingDirectorAgent reviews and approves our scrubbing brush slogan from the CopywriterAgent, us humans know the conversation should be over. However, if we don't define when to terminate the conversation, the CopywriterAgent is going to keep submitting slogans unnecessarily.

### Why use a termination strategy?

- **Efficiency**: It prevents endless loops or prolonged interactions, saving computational resources.
- **User satisfaction**: Users receive concise and relevant responses, avoiding frustration from overly long conversations.
- **Goal completion**: The use of an agent is to complete a task. By terminating appropriately, it confirms when a task or conversation has achieved its intended purpose.

### How does the framework implement termination strategies?

Similar to how the selection strategy is specified, developers can define a termination strategy or use a predefined strategy. Each termination strategy supports a `maximum_iterations` parameter that will end the chat after a maximum number of iterations. The default value is 99 iterations. Each termination strategy also requires the agents which should run the strategy. In the writer-reviewer agent scenario, the ReviewingDirectorAgent should determine when the chat should terminate.

#### DefaultTerminationStrategy

The `DefaultTerminationStrategy` class will only terminate after the specified number of maximum iterations.

#### KernelFunctionTerminationStrategy

The `KernelFunctionTerminationStrategy` class allows you to define your termination strategy by creating a kernel function from a prompt. In our writer and reviewer example, your selection strategy prompt might be:

```python
prompt="""
    Determine if the copy has been approved.  If so, respond with a single word: yes

    History:
    {{$history}}
    """
```

This class requires a `result_parser` parameter. The `result_parser` is a function that processes the output of your prompt function to determine whether the termination condition has been met. It takes the output of the prompt function and processes it to return `True` or `False`.

#### TerminationStrategy base class

The `TerminationStrategy` base class contains an overridable `should_agent_terminate` method where you can define custom logic for concluding the agent group chat. The return value must be a Boolean. For example, you could define a termination function that checks the most recent history entry for just the word "yes", however you would need to provide explicit instructions to your agent to return the termination keyword.

Once you've decided on your termination strategy, you can assign it to the `termination_strategy` parameter of the `AgentGroupChat` object.

### Truncating chat history

Since the termination strategy will typically rely on the last message in the chat to determine whether the chat should terminate, you can truncate the chat history to reduce token usage and help improve performance. The `KernelFunctionTerminationStrategy` accepts a `history_reducer` parameter which you can specify as:

```python
history_reducer = ChatHistoryTruncationReducer(target_count=1)
```

### Conversation state

Whether you use `AgentGroupChat` for a single-turn or multi-turn conversation, the state updates to `completed` once it meets the termination criteria. However, you may want to use the group chat instance again. To keep using the same chat instance, you'll need to reset the completion state to `False`. Without a state reset, the `AgentGroupChat` can't accept new interactions.

When a conversation hits the maximum number of iterations allowed, the conversation will end but won't be marked as completed. In this case, you can extend the conversation without resetting the conversation state.

By understanding these components, you can better utilize the Semantic Kernel Agent Framework to build intelligent multi-agent systems.
