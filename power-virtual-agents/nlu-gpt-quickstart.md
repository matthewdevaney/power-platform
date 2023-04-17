---
title: Quickstart guide for building bots with GPT (preview)
description: Build bots quickly and provide the most relevant information to your customers with natural language understanding advancements in Power Virtual Agents preview.
keywords: "PVA, GPT, NLU"
ms.date: 3/16/2023
ms.topic: how-to
author: iaanw
ms.author: iawilt
ms.reviewer: 
ms.collection: virtual-agent
ms.service: power-virtual-agents
ms.search.region: USA
searchScope:
  - "Power Virtual Agents"
---

# Quickstart guide for building bots with GPT (preview)

[!INCLUDE [AI tech disclosure with Bing Search](includes/disclosure-ai-preview-bing-addendum.md)]


Microsoft has made bot building even simpler with AI-powered capabilities in Power Virtual Agents (preview). Whether you're new to conversational AI or a seasoned developer, our intelligence platform is with you and your team every step of the way. 

This quickstart guide introduces you to the minimal steps necessary to get started quickly in creating and boosting a chatbot with expanded natural language understanding (NLU) capabilities. Using the intelligent authoring of AI-powered bots, you can now create a new topic or edit an existing one by describing what you want to happen or have your bot generate conversational responses even if there isn't a matching topic.

## Prerequisites 

> [!CAUTION] 
>  
> Your bot must be created in the US region. 
>  
> Other regions, and languages other than English, aren't supported during the preview.


- You'll need an account for Power Virtual Agents. 

    > [!NOTE]
    > If you don't have a Power Virtual Agents account, you can go to the [Power Virtual Agents introduction website](https://aka.ms/TryPVA), select **Start free**, and then sign in with your work email address. Also see the [Quickstart guide for creating a Power Virtual Agents bot](fundamentals-get-started.md).
    >  
    > Personal Microsoft accounts aren't supported. 
    >  
    > Supported browsers include Microsoft Edge, Chrome, and Firefox.

- You must be using the [preview version of Power Virtual Agents](preview/overview.md), and the bot type must be **Preview**. Preview chatbots have **(preview)** added to their name. When you create a new bot, select **Try the unified canvas (preview)**.  

    :::image type="content" source="media/nlu-gpt/nlu-boost-preview-bots.png" alt-text="Screenshot of the list of chatbots showing bots with preview added to their names.":::

- [Review AI response generation training, model, and usage notes](nlu-boost-conversations.md#ai-response-generation-training-model-and-usage-notes) and [Learn more about Azure OpenAI](/legal/cognitive-services/openai/transparency-note).

- Your bot must be created in the US region. Other regions, and languages other than English, aren't supported during the preview.

- This capability may be subject to usage limits or capacity throttling.
 
> [!IMPORTANT] 
> During the preview period, if you create a bot that has **Boost conversations** enabled, you'll need your admin to [enable bot publishing for your tenant](nlu-boost-conversations.md#publishing). 

## How bot conversations work

Power Virtual Agent bots use a [customized NLU model and AI capabilities](advanced-ai-features.md) to understand what a user types and to respond with the most appropriate bot topic. A bot topic is a sequence of nodes that logically flow from one step to the other. See [Create and edit topics (preview)](preview/authoring-create-edit-topics.md) for details on how bot topics work.

For example, you might create a bot for your customers to ask common questions about your business, thus reducing your support overhead by deflecting support calls. In the bot, you could create a topic that includes details about your store opening hours and call it **Store hours**. 

When a customer asks a question such as "When do you open?" or "What are your opening hours?", the bot uses NLU to understand the _intent_ behind the question (in this case, that the customer wants to know about hours of operation), and matches that intent to the most appropriate bot topic (which would be the **Store hours** topic). 

The bot then follows the _conversation flow_ that you've defined in the **Store hours** topic, which might be a series of questions that use if/else arguments, or logic gates, to ask the customer which store location they're interested in. The final output of the topic might be to then display the hours and contact information for that location.  

However, you may not be able to anticipate all the types of questions your customers ask. To help mitigate this, Power Virtual Agents (preview) incorporates a powerful new AI-powered capability that uses the latest advancements in NLU models. When you have **Boost conversations** enabled in your bot, and linked to a publicly available, Bing-indexed website, your bot can provide automatically generated, conversationally friendly, plain language responses without depending upon the bot builder to create topics for every eventuality. 

Also, with Power Virtual Agents new Copilot feature, your chatbot uses AI, powered by the Azure OpenAI GPT model (which is also used in Bing), to create bot topics based upon a simple description of what you want to achieve. You can also modify and update any topic in your bot in the same manner, by describing the changes you want to make.

Ready to get started? The first step is to create your bot.

## Create a boosted bot 

1. Go to the [Power Virtual Agents home page](https://web.powerva.microsoft.com/). 

1. In the side navigation menu, select **Create**. You can also select **Create a bot** on the **Home** page or **New chatbot** from the **Chatbots** page.

   :::image type="content" source="media/nlu-gpt/nlu-quickstart-home.png" alt-text="Screenshot of the Power Virtual Agents home page.":::

2. Select **Try the unified canvas (preview)** to create a preview bot. 
   - An opt-in confirmation message appears the first time you create or view a preview bot that describes some of their benefits.

   :::image type="content" source="media/nlu-gpt/nlu-quickstart-create-bot.png" alt-text="Screenshot of the Create a chatbot page.":::

3. Enter a name for your bot, and add the website you'd like your bot to fall back to if it can't find an appropriate bot topic, and select **Create**. 

   :::image type="content" source="media/nlu-gpt/nlu-quickstart-boost-create.png" alt-text="Screenshot of the Boost your conversation preview option.":::

There you have it! You’ve created a new bot.  

For any user-sent message that can't be matched to an existing topic, your bot looks for an answer on the website you've specified, and turns the answer into a simple message that it sends to the user. 

See the [Boost conversations (preview)](nlu-boost-conversations.md) topic for more details on the capability, including instructions for enabling boosted conversations in preview bots you've already created.

## Create a new topic using Copilot (preview)

1. With your bot open, select **Topics**. On the **Topics** page, select **+ New topic** and then **Create with Copilot (preview)**.

    :::image type="content" source="media/nlu-gpt/describe-it-new-topic.png" alt-text="Screenshot of the Power Virtual Agents navigation pane with Topics and the New topics button highlighted.":::

    > [!NOTE]
    >  
    > If you don't see the **Copilot** option, you may need to enable **Intelligent authoring support**:
    >1. Select the **Settings** icon on the top menu and then **General settings**.
    >:::image type="content" source="media/nlu-gpt/describe-it-enable.png" alt-text="Screenshot of the Power Virtual Agents menu with the Settings icon open.":::  
    >  
    >2. Set the switch under **Intelligent authoring support (preview)** to **On**.

2. In the **Create it with Copilot (preview)** window that appears, enter a name for your topic in the **Name your topic** field. 

3. In the **Create a topic to...** field, describe the topic you want to create in simple, plain English. You can include questions you want the bot to ask, messages it should show, and details of the specific behavior you want the bot to take.

    :::image type="content" source="media/nlu-gpt/describe-it-create-topic.png" alt-text="Screenshot of the Describe it to build it pop-up window.":::
   
    You can select any of the examples to automatically insert them into the **Create a topic to...** field. Select **View more examples** to generate new suggestions. 
      
4. Select **Create**.

Once your topic is created, your bot is ready for testing. It's that simple! 


## Edit your new topic with Copilot

With the new **Edit with Copilot (preview)** pane, you can make changes to your topic using the power of NLU. For example, if you want to make updates to your bot, such as moving and updating the nodes, all you need to do is describe what you want with Copilot.

Think of this new capability as a powerful wizard-like feature that walks you through the editing a topic process to fine-tune your bot's topics without having to work directly in the authoring canvas. You can also make additions and changes to existing nodes, and tell Copilot what you want it to do.

1. Select the topic you want to modify, and then **Edit with Copilot** on the menu bar just above the topic's conversation path.

    > [!TIP]
    >
    >If you have selected any nodes on the canvas, they will be used to scope your request.  
    >For example, if you have a **Question** node selected, you could write _add a speech response_, instead of _add a speech response to the question node_.
    > You can see the nodes you've selected next to the **Update** button.

    :::image type="content" source="media/nlu-gpt/describe-it-toolbar.png" alt-text="Screenshot of the Power Virtual Agents authoring window with the Describe it button highlighted.":::
   
2. In the **What do you want to do** field, describe what you want to change or add in the topic. 

    :::image type="content" source="media/nlu-gpt/describe-it-modify.png" alt-text="Screenshot of the Power Virtual Agents authoring window with the Describe it side panel open.":::

    Use simple, plain English to direct the AI with what you want it to do, as in the these examples:

    - _add a question to ask the user for their date of birth_
    - _add 2 message variations to all questions in the topic_
    - _summarize the information collected from the user in an Adaptive Card_

3. Click **Update**. The AI will make updates based on your directions.
   
4. Once the update has been applied, you can review the changes and continue to edit your topic, either in the [usual ways of editing topics](authoring-create-edit-topics.md) or by describing more things you want to change. 
    
    If you don't like the changes, select the **Undo** button. You can then change your directions and try again.

    You can always see the last thing you asked Copilot to do under the **What you asked for** label.

> [!TIP]
>  
> You can provide feedback on how well the AI did by selecting the "thumbs up" or "thumbs down" icon at the bottom of the **Edit with Copilot** panel.  
> If you select the thumbs down icon, you can also include more verbose feedback. We'll use this feedback to improve the quality of the AI.
>  
> :::image type="content" source="media/nlu-gpt/describe-it-feedback.png" alt-text="Screenshot of the Power Virtual Agents Describe it feedback panel.":::

Next, it's time to test your bot! 

## Test your bot's boosted conversational reach 

Once you create a bot, you can immediately test the bot and try out different phrases for your bot to reply to. 

The **Test bot** pane shows how a bot conversation plays out at every step and you can fine-tune a topic directly within the **Power Virtual Agents (preview)** portal:
 
1. With a topic open for editing, select **Test bot** above the authoring canvas. You can also select **Test your bot** from the side navigation menu. 

    :::image type="content" source="media/nlu-gpt/nlu-quickstart-test-bot.png" alt-text="Screenshot of Test bot option.":::

2. At the **Type your message** prompt, ask the bot about the return policy of the organization whose website you linked to. For example, you could type *What is your return policy?*. 
 
   The bot retrieves information from the website and returns a response. The response provides a link to where it found that information and allows you to provide feedback.
 
4. (Optional) Try asking the bot about something you know is not on the website you specified, such as *Why is the sky blue*. Because the bot can't find a relevant bot topic or a relevant answer on the specified website, it replies with a [system fallback topic](authoring-system-fallback-topic.md) that indicates it can't understand the question, and asks you to rephrase the question. 

    :::image type="content" source="media/nlu-gpt/nlu-quickstart-system-fallback.png" alt-text="Screenshot of Test bot pane with the message that the bot doesn't understand.":::
 
> [!NOTE]
> After you test your bot, you can select the reset icon at the top of the **Test bot** pane to clear previous conversations. Resetting makes it easier to follow the flow of the current topic without getting confused by previous conversations.
>  
> :::image type="content" source="media/nlu-gpt/nlu-quickstart-test-reset.png" alt-text="Screenshot of Test bot pane reset button that looks like a an arrow in a circle shap.":::

You can return to the authoring canvas at any time to revise the conversation path. The **Test bot** pane automatically refreshes when you select **Save**. 



## Add features to further develop your bot 

It's easy to take your bot's conversations up a notch by giving your bot a voice of its own. You can add images and video clips, as well as adaptive cards, entities, and variable expressions. 

See the [Key concepts - Enhanced authoring](advanced-fundamentals.md) for more details, or continue your bot-building journey by checking out the rest of the [Power Virtual Agents documentation](index.yml).

[!INCLUDE[footer-include](includes/footer-banner.md)]
