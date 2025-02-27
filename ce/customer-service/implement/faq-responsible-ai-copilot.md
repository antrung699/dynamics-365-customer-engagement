---
title: Responsible AI FAQ for Copilot in Customer Service
description: This FAQ provides information about the AI technology that Dynamics 365 Customer Service uses. This FAQ also includes key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
author: neeranelli
ms.author: nenellim
ms.reviewer: shujoshi
ms.topic: faq
ms.collection: 
ms.date: 11/21/2023
ms.custom: 
- bap-template
- responsible-ai-faq
---

# Responsible AI FAQ for Copilot in Customer Service

This FAQ article helps answer the questions around the responsible use of AI in copilot features in Customer Service.

## What is Copilot in Dynamics 365 Customer Service?

Copilot is an AI-powered tool that transforms the agent experience in Dynamics 365 Customer Service. It provides real-time AI powered assistance that will help agents resolve issues faster, handle cases more efficiently, and automate time-consuming tasks. Then agents can focus on delivering high-quality service to their customers.

## What are the systems capabilities?

Copilot provides the following main features:

- **Ask a question**: Is the first tab that agents see when they activate the Copilot help pane. It's a conversational interface with Copilot, which helps provide contextual responses to the agents’ questions. Copilot’s responses are based on both internal and external knowledge sources provided by your organization during setup.

- **Write an email**: Is the second tab on the Copilot help pane helps agents quickly create email responses based on the context of the case, reducing the time users need to spend creating emails.

- **Draft a chat response**: Enables agents to create a response in a single click to the ongoing digital messaging conversation from knowledge sources configured by your organization.

- **Summarize a case**: Copilot provides agents with a summary of a case right on the case form, so they can quickly catch up on the important details of a case.  

- **Summarize a conversation**: Copilot provides agents with a summary of a conversation at key points throughout the customer journey such as virtual agent handoffs, transfers and on demand. 

## What is the system’s intended use?

Copilot in Customer Service is intended to help customer service representatives work more efficiently and effectively. Customer service representatives can use Copilot’s knowledge-based responses to save time from searching knowledge articles and drafting responses. Copilot summaries are designed to support agents in quickly ramping up on cases and conversations. Content generated by Copilot in Customer Service isn't intended to be used without human review or supervision.

## How was Copilot in Customer Service evaluated? What metrics are used to measure performance?

Copilot in Customer Service has been evaluated against real world scenarios with customers around the world through each phase of its design, development, and release. Using a combination of research and business impact studies, we’ve evaluated various quantitative and qualitative metrics about Copilot, including its accuracy, usefulness, and agent-trust.

## What are the limitations of Copilot in Customer Service? How can users minimize the impact of Copilot limitations?  

Copilot’s knowledge-based capabilities like ask a question, write an email, and draft a chat response, are dependent on high-quality and up-to-date knowledge articles for grounding. Without these knowledge articles, users are more likely to encounter Copilot responses that aren't factual.  

To minimize the likelihood of seeing non-factual responses from Copilot, it’s important that the organizations employ robust knowledge management practices to ensure the business knowledge that connects to Copilot is of high-quality and up-to-date.

## What operational factors and settings allow for effective and responsible use of the system?  

### Always review results from Copilot

Copilot is built on large language model technology, which is probabilistic in nature. When presented with a piece of input text, the model calculates the probability of each word in that text given the words that came before it. The model then chooses the word that is most likely to follow. However, since the model is based on probabilities, it can't say with absolute certainty what the correct next word is. Instead, it gives us its best guess based on the probability distribution it has learned from the data it was trained on. Copilot uses an approach called grounding, which involves adding additional information to the input to contextualize the output to your organization. It uses semantic search to understand the input and retrieve relevant internal organizational documents and trusted public web search results, and guides the language model to respond based on that content. While this is helpful in ensuring Copilot responses adhere to organizational data, it's important to always review results produced by Copilot prior to using them.

### Get the best out of Copilot

When you're interacting with Copilot, it's important to keep in mind that the structure of the questions can greatly affect the response that Copilot gives. To interact with Copilot effectively, it's crucial to ask clear and specific questions, provide context to help the AI better understand your intent, ask one question at a time, and avoid technical terms for clarity and accessibility.

### Ask clear and specific questions

Clear intent is essential when asking questions, as it directly impacts the quality of the response. For instance, asking a broad question like “Why is the customer’s coffee machine not starting up?” is less likely to yield a useful response compared to a more specific question, such as “What steps can I take to determine why the customer’s coffee machine isn't starting up?”.

However, asking an even more detailed question like “What steps can I take to determine why a Contoso 900 coffee machine with a 5-bar pressure rating isn't starting up?” narrows down the scope of the problem and provides more context, leading to more accurate and targeted responses.

### Add Context

Adding context helps the conversational AI system better understand the user's intent and provide more accurate and relevant responses. Without context, the system might misunderstand the user's question or provide generic or irrelevant responses.

For example, "Why is the coffee machine not starting up?" will result in a generic response when compared to a question with more context like, "Recently, the customer initiated descaling mode on their coffee machine and completed descaling successfully. They even received three flashes from the power light at the end to confirm that descaling was complete. Why are they unable to start the coffee machine anymore?"

Adding context in this manner is important because it helps Copilot better understand the user's intent and provide more accurate and relevant responses.

### Avoid technical terms if possible

We recommend that you avoid using extremely technical terms and resource names when interacting with Copilot because the system may not always understand it accurately or appropriately. The use of simpler, natural language helps ensure that the system can understand the user's intent correctly and provide clear, useful responses. For example –  

"The customer can't SSH into the VM after having changed the firewall config."  

Instead, you can rephrase as –  

“The customer changed the firewall rules on their virtual machine. However, they can no longer connect using Secure Shell (SSH). Can you help?”

By following the suggestions, agents can enhance their interactions with Copilot and increase the likelihood of receiving accurate and confident responses from it.

### Summarizing or expanding a response

Sometimes the response from Copilot can be longer than expected. This could be the case when the agent is in a live chat conversation with a customer and needs to send concise responses when compared with sending a response over email. In such cases, asking Copilot to “summarize the response” will result in a concise answer to the question.  Similarly, if there's a need for more detail, asking Copilot to “Provide more details” will result in a more detailed answer to your question. If the response is truncated, typing “continue” will display the remaining part of the response.

## How can I influence the responses generated by copilot? Can I fine tune the underlying LLM?

It's not possible to customize the large language model (LLM) directly.  Copilot responses can be influenced by updating the source documentation. All the feedback content from Copilot responses is stored. Reports can be created using this data to determine the data sources that need to be updated. It’s a good idea to have processes in place to periodically review the feedback data and ensure knowledge articles are providing the best and most up-to-date information to Copilot.

## What's the data security model for Copilot?

Copilot enforces the role-based access (RBAC) controls defined and adheres to all the existing security constructs. Therefore, agents cannot view data that they do not have access to. Additionally, only data sources that the agent has access to are used for copilot response generation.

## Where does data processing and retrieval occur to generate copilot responses?  

Copilot is not calling the public OpenAI service that powers ChatGPT. Copilot in Customer Service uses the [Microsoft Azure OpenAI Service](/azure/ai-services/openai/overview) in a Microsoft managed tenant. All data processing and retrieval occurs within Microsoft managed tenants. Additionally, customer’s data is not shared and is not fed back into public models.

### See also

[Use copilot features](../use/use-copilot-features.md)  
[Region availability of Copilot](../administer/cs-region-availability-service-limits.md#region-availability-of-analytics-and-insights)  
[FAQ for Copilot data security and privacy in Microsoft Power Platform](/power-platform/faqs-copilot-data-security-privacy)