---
title: How to manage conversation intelligence data in Dataverse
description: Learn about the data structure, storage, access, and deletion of conversation intelligence insights in Dataverse.
author: lavanyakr01
ms.author: lavanyakr
ms.reviewer: shujoshi
ms.topic: conceptual 
ms.collection: 
ms.date: 01/16/2024
ms.custom: 
  - bap-template
  - ai-seo-date: 01/11/2024
  - ai-gen-docs-bap
  - ai-gen-title
  - ai-gen-desc
content_well_notification: AI-contribution
---

# How to manage conversation intelligence data in Dataverse

This article describes how your call data flows to Microsoft Dataverse to generate insights and how this data is structured. It also describes how to manage the storage, access, and deletion of conversation intelligence insights in Dataverse.

## How data flows

The following diagram depicts the flow of events starting from the time a call comes in to the time the data is saved, processed, analyzed, and displayed in the call summary page.

:::image type="content" source="media/conversation-intelligence-data-flow.svg" alt-text="Diagram depicting the flow of events starting from the time a call comes in to the time the data is saved, processed, analyzed, and displayed in the call summary page." lightbox="media/conversation-intelligence-data-flow.svg":::

As depicted in the diagram, the flow works as follows:

1. A salesperson receives an incoming call or makes an outgoing call from the Teams dialer in Dynamics 365 Sales and starts the recording.

1. After the call ends, the recording is saved in the Azure blob storage or Dataverse, based on the [storage configuration in conversation intelligence settings](fre-setup-ci-sales-app.md). The transcript is saved in Dataverse.

1. Conversation intelligence uses advanced AI models to generate insights from the recording and transcript.  
1. The conversation intelligence app user updates [the tables](#how-data-is-structured-in-dataverse) in Dataverse with the insights. The tables are then assigned to the conversation’s owner.
1. The insights are then displayed in the call summary page. 

> [!NOTE]
> The insights are stored in Dataverse until the data retention period expires. For more information, see [Data retention and deletion](#data-retention-and-deletion).

## How data is structured in Dataverse

The conversation intelligence data is stored in Dataverse in the form of tables. The following diagram depicts the conversation intelligence tables and their relationships in Dataverse.

:::image type="content" source="media/conversation-intelligence-data-structure-in-dataverse.svg" alt-text="Diagram depicting the conversation intelligence tables and their relationships in Dataverse." lightbox="media/conversation-intelligence-data-structure-in-dataverse.svg":::

The following table describes the tables and their purpose.

| Table Name | Description |
|-------------|-------------|
| `msdyn_SCIConversation` | Contains data required to correlate between the conversation intelligence data, phone call activity, and audio recording files.
`msdyn_ConversationTag` | Contains tags that users have manually added to a conversation.
`msdyn_ConversationSystemTag` | Contains the automatic categorizations by the system, such as voicemail, wrong number, rain-check.
`msdyn_recording` | Contains a link to the recording file in the Azure blob storage, or stores the recording file itself, according to the storage settings.
`msdyn_transcript` | Contains the transcript of the conversation.
`msdyn_conversationAggregatedInsights` | Contains Key Performance Indicators (KPIs) such as longest monologue, switch count throughout the conversation, meeting duration, and more. It also contains IDs to correlate the lower level insights.
`msdyn_conversationSentiment` | Contains sentiment data for the conversation, such as overall percent of positive, negative, and neutral customer sentiments during the conversation.
msdyn_conversationSubject | Contains the automatic categorization of segments of the conversation, such as introduction, negotiation, closure, and more.
`msdyn_conversationParticipantInsights` | Contains identifiers for each participant, as well as their personal KPIs, such as average talking speed, own longest monologue, average pause before speaking, talk-to-listen ratio, and switch count. Each participant in a conversation, whether a seller or a customer, has their own instance of the participant table. This table also contains child nodes listed in the following rows.
`msdyn_conversationSignal` | Contains all the tracked keywords such as brands, times, competitors, and names that were mentioned by participants during the conversation.
`msdyn_conversationParticipantSentiment` | Contains the sentiment per each fragment of the participant’s speech.
`msdyn_conversationActionItem` | Contains suggested action items for the participant.
`msdyn_conversationSummarySuggestion` | Contains suggestions for the call summary which involves the participant or were a result of the participant’s communication.
`msdyn_conversationQuestion` | Contains questions asked by the participant.


## Grant access to conversation intelligence tables

By default, all out-of-the-box sales security roles have permission to access the conversation intelligence tables in Dataverse. The access is granted based on the current permission model in Dynamics 365. For example, sellers have access to their own conversations, managers have access to their team’s conversations, and so on.

If you have custom security roles, work with your Dataverse administrator to grant access to [the conversation intelligence tables](#how-data-is-structured-in-dataverse).

> [!NOTE]
> **Read** permission is sufficient for users who only need to view the call summary page. **Edit/write** permissions are required to edit the call summary, such as tagging a call, leaving a comment on the transcript, etc.

### Estimate storage space required for a conversation

The storage space required in Dataverse for a conversation depends on the duration of the conversation, the number of participants, and the configuration of the data saved. Estimate the space required for your organization so that you can plan your storage requirements accordingly.

The following table provides an estimate of the space required for a conversation based on the conversation’s duration for 2 participants:

> [!NOTE]
> Actual size may vary depending on the actual number of tables created or updated during the conversation. 

| Duration (minutes) | Size in MB (2 participants) | File Storage (MB) |
|:-------------------|:----------------------------|:------------------|
| 10                 | 0.15                         | 4                 |
| 20                 | 0.30                         | 8                 |
| 30                 | 0.45                         | 12                |
| 40                 | 0.60                         | 16                |
| 50                 | 0.75                         | 20                |
| 60                 | 0.90                         | 24                |
| 70                 | 1.05                         | 28                |
| 80                 | 1.20                         | 32                |
| 90                 | 1.35                         | 36                |

## Data retention and deletion

By default, there is no expiry date for the data stored in Dataverse. However, you can set a retention policy for the various tables or manually delete parts or all of the data when they're no longer needed. For more information, see [Manage data retention policies in Microsoft Dataverse](/power-apps/maker/data-platform/data-retention-manage).

The [conversation intelligence tables](#how-data-is-structured-in-dataverse) are organized in a tree structure with parent-child relationships. When you delete a record, the following rules apply:

- Deleting a record from any of the tables in the tree will cascade-delete corresponding data in all its sub-nodes. For example, deleting a record from the `msdyn_conversationParticipantInsights` table will delete corresponding records from the `msdyn_conversationSignal`, `msdyn_conversationParticipantSentiment`, `msdyn_conversationActionItem`, `msdyn_conversationSummarySuggestion`, and `msdyn_conversationQuestion` tables. 

- If you've partially deleted the data from Dataverse, the call summary page will continue to display the available insights, provided that the recording and transcripts of the call are available. For example, if you delete a participant's row in the `msdyn_conversationParticipantInsights` table, the call summary page will display all the insights, including the participant's insights for the other participants. 


## See also

- [Set up conversation intelligence for Dynamics 365 Sales](fre-setup-ci-sales-app.md)
- [Manage data retention policies in Microsoft Dataverse](/power-apps/maker/data-platform/data-retention-manage)
