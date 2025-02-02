---

title: Use variables (preview)
description: Use variables with custom and prebuilt entities to created customized bot conversations in Power Virtual Agents preview.
keywords: "PVA"
ms.date: 12/15/2022
ms.service: power-virtual-agents
ms.topic: how-to
author: iaanw
ms.author: iawilt
ms.reviewer: clmori
ms.custom: authoring, ceX, bap-template
ms.collection: virtual-agent
---

# Use variables (preview)

[!INCLUDE [Preview disclaimer](includes/public-preview-disclaimer.md)]

Save customers' responses in a bot conversation to variables and reuse them later in the conversation. Or, use variables to create logical expressions that dynamically route the customer down different conversation paths.

For example, save a customer's name in a variable called `UserName`, and the bot can address the customer by name as the conversation continues.

Variables can also be passed to, and returned from, [other topics](authoring-variables-bot.md) and [Power Automate flows](advanced-flow.md).  

## Variable scopes

Variables can exist at three levels, or scopes:

- **Topic** variables can only be used in the topics in which they're created. This scope is the default for variables that you create.
- [**Global** variables](authoring-variables-bot.md) can be used in all topics. You can change the scope of a topic variable to make it a global variable.
- [**System** variables](#system-variables) are created automatically with your bot. They provide more contextual information about the conversation or the user. They're available in all topics.

## Variable types

A variable is associated with a **base type**. The type determines what values the variable can contain and the operators that you can use when you construct a logical expression with it.

<!-- best viewed without wordwrap -->
| Type     | Description                                                                                                                                |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| String   | A sequence of characters used to represent text                                                                                            |
| Boolean  | A logical value that can only be `true` or `false`                                                                                         |
| Number   | Any real number                                                                                                                            |
| Table    | A list of values, but all values must be of the same type                                                                                  |
| Record   | A collection of name-value pairs where values can be of any type                                                                           |
| DateTime | A date, time, day of the week, or month relative to a point in time                                                                        |
| Choice   | A list of string values that have associated synonyms                                                                                      |
| Blank    | A placeholder for "no value" or "unknown value"; for more information, see [Blanks in Power Fx](/power-platform/power-fx/data-types#blank) |

A variable's type is set the first time a value is assigned to it. After that, the type for that variable is fixed and it can't be assigned values of any other type. For example, a variable given the starting value of `1` is assigned the type **Number**. Attempting to assign it to a **String** value of `"apples"` will result in an error.

When you're testing a bot, a variable may appear temporarily as the type **unknown**. An **unknown** variable hasn't been assigned a value yet.

Order of variables is determined from top to bottom of the authoring canvas. That is, nodes at the top of the authoring canvas are considered before nodes at the bottom. When you create branches with **Condition** nodes, branches are ordered from left to right. That is, nodes in the leftmost branch are considered before nodes in the rightmost branch.

## Entities

Power Virtual Agents uses [entities](advanced-entities-slot-filling.md) to identify a specific type of information from a user's responses. The identified information is saved in a variable of the type that's appropriate for the information. The following table lists the variable base type that's associated with pre-built entities.

| Entity                  | Variable Base Type |
| ----------------------- | ------------------ |
| Multiple-choice options | Choice             |
| User's entire response  | String             |
| Age                     | Number             |
| Boolean                 | Boolean            |
| City                    | String             |
| Color                   | String             |
| Continent               | String             |
| Country or region       | String             |
| Date and time           | DateTime           |
| Email                   | String             |
| Event                   | String             |
| Integer                 | Integer            |
| Language                | String             |
| Money                   | Number             |
| Number                  | Number             |
| Ordinal                 | Number             |
| Organization            | String             |
| Percentage              | Number             |
| Person name             | String             |
| Phone number            | String             |
| Point of interest       | String             |
| Speed                   | Number             |
| State                   | String             |
| Street address          | String             |
| Temperature             | Number             |
| URL                     | String             |
| Weight                  | Number             |
| Zip code                | String             |
| Custom entity           | Choice             |

## Create a variable

Any node that prompts you to select a variable as an output, such as a [**Question** node](authoring-ask-a-question.md), automatically creates an output variable of the appropriate type.

:::image type="content" source="media/authoring-variables/authoring-variables-default-variable.png" alt-text="Screenshot of a Question node, with the name and type of the default variable highlighted.":::

## Pick an entity to use

**Question** nodes are created with multiple-choice options by default. To use a different prebuilt or custom entity, select the **Identify** box and choose the type of information the bot should listen for.

:::image type="content" source="media/authoring-variables/authoring-variables-select-entity.png" alt-text="Screenshot of a Question node with the Choose information to identify menu open and the Person name entity highlighted.":::

## Rename a variable

Variables are automatically assigned a name when you create them. A best practice is to give your variables meaningful names to make their purpose clear to anyone else who must maintain your bot.

1. Select the variable to open it in the [**Variable properties** pane](#variable-properties-pane).

1. Under **Variable name**, enter a new name for your variable.

## Set a variable

Typically you'll use a [**Question** node](authoring-ask-a-question.md) to save user input to a variable. There may be situations where you want to set the value yourself, however. In those cases, use a **Set Variable Value** node.

1. Select **Add node** (**+**) to add a node, and then select **Set a variable value**.

1. Select the box under **Set variable**, and then select **Create a new variable**.

    :::image type="content" source="media/authoring-variables/create-variable.png" alt-text="Screenshot of the Create a new variable button.":::

    A new variable is created. Its type is **unknown** until you assign a value to it.

    :::image type="content" source="media/authoring-variables/authoring-variables-set-variable-value.png" alt-text="Screenshot of a Set Variable Value node with a new variable of unknown type.":::

1. For **To value**, assign a value using one of the following options:

   - Type a [literal value](#use-literal-values).
   - Select an existing variable of the same type. This action sets your variable to the same value as the variable you select.
   - Use a [Power Fx formula](advanced-power-fx.md). Power Fx formulas are useful for more complex types where literal values can't be used, such as Table and Record types.

## Use literal values

Instead of selecting a variable value, you can enter a literal value into any variable.

:::image type="content" source="media/authoring-variables/set-variable-to-literal.png" alt-text="Screenshot showing the use of a literal value for a variable named productName.":::

:::image type="content" source="media/authoring-variables/set-redirect-variable-to-literal.png" alt-text="Screenshot showing a literal value as the input for a variable in a redirect node.":::

The node attempts to interpret literal values as a string, a number, or a boolean type. For example, `123` is interpreted as a number. If you want it to be interpreted as a string value instead, you can wrap the value in double quotes, like this: `"123"`.

For some scenarios, or where you're using more complex types, use a [Power Fx formula](advanced-power-fx.md) to set a specific type.

## Variables pane

The **Variables** pane is where you can view all the variables that are available in the topic, regardless of which nodes they're defined or used in. For each variable, you can select whether it can receive its value from other topics, return its value to other topics, or both. You can also select a variable to edit its properties in the [**Variable properties** pane](#variable-properties-pane).

To open the **Variables** pane, in the topic's menu bar, select **Variables**.

:::image type="content" source="media/authoring-variables/authoring-variables-open-variable-pane.png" alt-text="Screenshot of the Variables pane in the Power Virtual Agents authoring canvas, with the Variables button highlighted.":::

## Variable properties pane

In the **Variable properties** pane, you can rename a variable, see where it's used, or convert it to a [global variable](authoring-variables-bot.md). You can't convert it from a global variable back to a topic variable, however. You can also select whether it can receive values from or pass its value to other topics.

To open the **Variable properties** pane, select a variable in the [**Variables** pane](#variables-pane). You can also open the **Variable properties** pane by selecting a variable in any node.

:::image type="content" source="media/authoring-variables/variable-properties.png" alt-text="Screenshot of the Variable properties pane.":::

## System variables

Every bot comes with built-in system variables that provide additional information about a conversation.

:::image type="content" source="media/authoring-variables/authoring-variables-system-variable-picker.png" alt-text="Screenshot of system variables in a bot topic.":::

Not all system variables are shown in the list. You must access these hidden system variables with a [Power Fx formula](advanced-power-fx.md).

To use system variables in a Power Fx formula, you must add `System.` before the variable name. For example, to include the system variable `User.DisplayName` in a formula, you'd need to refer to it as `System.User.DisplayName`.

| Name                           | Type   | Hidden  | Definition                                                  |
|--------------------------------|--------|---------|-------------------------------------------------------------|
| Activity.Channel               | choice | visible | The channel ID of the current conversation                  |
| Activity.ChannelData           | any    | hidden  | An object that contains channel-specific content            |
| Activity.ChannelId             | string | hidden  | The channel ID of the current conversation, as a string     |
| Activity.From.Id               | string | hidden  | The channel-specific unique ID of the sender                |
| Activity.From.Name             | string | hidden  | The channel-specific user-friendly name of the sender       |
| Activity.Name                  | string | visible | The name of the event                                       |
| Activity.Text                  | string | visible | The most recent message sent by the user                    |
| Activity.Type                  | choice | visible | Type of [activity][]                                        |
| Activity.TypeId                | string | hidden  | Type of [activity][], as a string                           |
| Activity.Value                 | any    | hidden  | Open-ended value                                            |
| Bot.Name                       | string | visible | The name of your bot                                        |
| Channel.DisplayName            | string | hidden  | The display the name of the channel                         |
| Conversation.Id                | string | visible | The unique ID of the current conversation                   |
| LastActivity.Id                | string | visible | The ID of the previously sent [activity][]                  |
| LastMessage.Id                 | string | visible | The ID of the previous message sent by the user             |
| LastMessage.Text               | string | visible | The previous message sent by the user                       |
| Recognizer.TriggerMessage.Id   | string | visible | The ID of the user message that triggered the current topic |
| Recognizer.TriggerMessage.Text | string | visible | The user message that triggered the current topic           |
| User.DisplayName               | string | visible | The display name of the signed-in user                      |

[activity]: /azure/bot-service/bot-activity-handler-concept

<!-- TODO: this section needs to be re-written with a specific scenario so that its less confusing -->
## Pass variables between topics

When you redirect one topic to another, you can pass the values of variables between the original topic and the destination topic. Passing variables between topics is especially useful when an earlier topic already collected information that a later topic needs. Your users will appreciate not having to answer the same questions again.

### Receive values from other topics

When a topic defines a variable (for example, in a Question node), the bot asks the user the question to fill in the variable's value. If the bot has already acquired the value in an earlier topic, there's no reason to ask the question again. In these cases, you can set the variable to **Receive values from other topics**. When another topic redirects to this one, it can pass either the value of a variable (or a [literal value](#use-literal-values)) to this variable and skip the question. The experience for the user talking to the bot is seamless.

In this example, we'll use two topics, Greeting and Talk to Customer. Both topics ask for the customer's name. However, if the Greeting topic runs first, the Talk to Customer topic skips its question. Instead, it uses the value of the variable that's passed from the Greeting topic.

Here's the flow of the Talk to Customer topic:

:::image type="content" source="media/authoring-variables/authoring-variables-passed-ex3.png" alt-text="Screenshot of the Talk to Customer topic conversation flow.":::

As shown in the Test bot pane, if this topic is triggered first, it asks the user, "What should I call you?" It stores the value in a string variable called `userName`. The `userName` variable is also set to get its value from other topics. The topic concludes with the message, "I hope you're having a wonderful day, {userName}!"

Here's the flow of the Greeting topic:

:::image type="content" source="media/authoring-variables/authoring-variables-passed-ex1.png" alt-text="Screenshot of the Greeting topic conversation flow.":::

As shown in the Test bot pane, if this topic is triggered first, it asks the user, "What's your name?" It stores the value in a string variable called `UserName`. The topic sends the message, "Pleased to meet you, {UserName}!" It then redirects to the Talk to Customer topic, which sends the message, "I hope you're having a wonderful day, {userName}!" Note, however, that the Talk to Customer topic skipped asking for the user's name again. Instead, it used the value of the `UserName` variable passed from the Greeting topic.

Finally, here's that second conversation again, this time from the perspective of the Talk to Customer topic:

:::image type="content" source="media/authoring-variables/authoring-variables-passed-ex2.png" alt-text="Screenshot of the Talk to Customer topic conversation flow when the Greeting topic is triggered first.":::

Let's walk through the steps to set up a topic to receive values from other topics. We'll use our current example, but the same steps will work anytime a topic needs to get a value from an earlier topic.

#### Set up the destination topic

The destination topic is the topic being redirected to, the one that will receive values from other topics. In our example, it's Talk to Customer.

1. Create or go to your destination topic.

1. [Add a Question node](../authoring-create-edit-topics.md#ask-a-question) and enter `What should I call you?` for the message.

1. Under **Identify**, select the pre-built entity **Person name**.

1. Select the variable to open the **Variable properties** pane. Name it `userName`, and then select **Receive values from other topics**.

    :::image type="content" source="media/authoring-variables/authoring-variables-passed-destination.png" alt-text="Screenshot of the Talk to Customer topic with the userName variable and its properties highlighted.":::

1. [Add a Message node](../authoring-create-edit-topics.md#show-a-message).

1. In the message box, type `I hope you're having a wonderful day, `.

1. Select the **Insert variable** icon (**{x}**), and then select **userName**.

1. Select the space after the variable and type `!`.

1. Save the topic.

#### Set up the source topic

The source topic is the topic doing the redirecting, the one that provides the value that will be passed to the destination topic. In our example, it's Greeting.

1. Go to the source topic.

1. [Add a Redirect node](authoring-topic-management.md#redirect-to-another-topic) and select the destination topic.

1. Select **+ Add input**, and then select the variable from the destination topic that you want to pass a value to.

    :::image type="content" source="media/authoring-variables/authoring-variables-passed-source.png" alt-text="Screenshot of the Greeting topic with the userName variable added as input in a redirect node.":::

1. Select the **>** icon, and then select the variable whose value you want to pass.

    :::image type="content" source="media/authoring-variables/authoring-variables-passed-source-selected.png" alt-text="Screenshot of the Greeting topic with the UserName variable value selected.":::

    The Redirect node should look like this:

    :::image type="content" source="media/authoring-variables/authoring-variables-passed-source-final.png" alt-text="Screenshot of the Greeting topic with the completed Redirect node.":::

1. Save the topic.

### Return values to original topics

When a topic is redirected to and obtains a variable by asking a question or in some other way, the variable can be returned to the original topic. The variable becomes part of the original topic and can be used like any other variable. Information the bot obtains is thus available across topics, reducing the need for [global variables](../authoring-variables-bot.md).

Let's continue with the example from the previous section. We'll ask a new question in the Talk to Customer topic, and then return the answer to the Greeting topic.

#### Set up the source topic for a returned variable

When you're returning a variable to a topic, the source topic is the topic being redirected to, the one that provides the value that will be passed back to the original topic. In this example, it's Talk to Customer.

1. Go to the source topic.

1. [Add a Question node](../authoring-create-edit-topics.md#ask-a-question) and enter `What city do you live in?` for the message.

1. Under **Identify**, select the pre-built entity **City**.

1. Select the variable to open the **Variable properties** pane. Name it `userCity`, and then select **Return values to original topics**.

    :::image type="content" source="media/authoring-variables/authoring-variables-returned-source.png" alt-text="Screenshot of the Talk to Customer topic with the userCity variable and its properties highlighted.":::

1. Save the topic.

#### Set up the destination topic for a returned variable

When you're returning a variable to a topic, the destination topic is the topic doing the redirecting, the one that will receive values from other topics. In our example, it's Greeting.

1. Go to the destination topic.

1. The variable you selected in the source topic should appear in the Redirect node as an output variable.

    :::image type="content" source="media/authoring-variables/authoring-variables-returned-destination.png" alt-text="Screenshot of the Greeting topic conversation flow with a returned variable in a Redirect node.":::

1. Save the topic.

### See also

- [Reuse variables across topics](authoring-variables-bot.md)
- [Customize the look and feel of the bot](customize-default-canvas.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
