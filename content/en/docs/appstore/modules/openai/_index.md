---
title: "OpenAI"
url: /appstore/modules/openai-connector/
linktitle: "OpenAI"
description: "Describes the configuration and usage of the OpenAI Connector from the Mendix Marketplace that allows you to integrate generative AI into your Mendix app."
tags: ["OpenAI", "generative AI", "AI", "connector", "marketplace", "chatgpt", "dall-e", "genAI", "embeddings", "RAG", "Azure OpenAI", "function calling", "tools", "LLM", "ReAct", "vision"]
aliases:
    - /appstore/connectors/openai-connector/
---

## 1 Introduction {#introduction}

The [OpenAI Connector](https://marketplace.mendix.com/link/component/220472) allows you to integrate generative AI into your Mendix app and is compatible with [OpenAI's platform](https://platform.openai.com/) as well as [Azure's OpenAI service](https://oai.azure.com/). 

The current scope covers text generation use cases based on the [OpenAI Chat Completions API](https://platform.openai.com/docs/api-reference/chat), image generation use cases based on the [Image Generations API](https://platform.openai.com/docs/api-reference/images), and embeddings use cases based on the [Embeddings API](https://platform.openai.com/docs/api-reference/embeddings).

Mendix provides dual platform support for OpenAI as well as Azure OpenAI.

### 1.1 Typical Use Cases {#use-cases}

#### 1.1.1 Text Generation {#use-cases-text}

* Develop interactive AI chatbots and virtual assistants that can carry out conversations in a natural and engaging manner. 
* Use OpenAI’s large language models for text comprehension and analysis use cases such as summarization, synthesis, and answering questions about large amounts of text.
* Fine-tune the OpenAI models on a specific task or domain, by training it on custom data, to improve its performance. 
* Integrate more easily with OpenAI’s platform which, by providing text generation models, allows you to build applications with the following features:
    * Draft documents 
    * Write computer code 
    * Answer questions about a knowledge base 
    * Analyze texts 
    * Give software a natural language interface 
    * Tutor in a range of subjects 
    * Translate languages 
    * Simulate characters for games
    * Image to text

OpenAI provides market-leading large language model capabilities with GPT-4: 

* Advanced reasoning: Follow complex instructions in natural language and solve difficult problems with accuracy. 
* Creativity: Generate, edit, and iterate with end-users on creative and technical writing tasks, such as composing songs, writing screenplays, or learning an end-user’s writing style. 
* Longer context: GPT-4 is capable of handling over 25,000 words of text, allowing for use cases like long form content creation, extended conversations, and document search and analysis. 

#### 1.1.2 Image Generation {#use-cases-images}

Generate one or more completely new, original images and art from a text description. Powered by the OpenAI DALL-E models, the connector enables developers to generate these images by combining concepts, attributes, and styles.

#### 1.1.3 Embeddings {#use-cases-embeddings}

Convert strings into vector embeddings for various purposes based on the relatedness of texts. 
Embeddings are commonly used for:

* Search 
* Clustering 
* Recommendations 
* Anomaly detection 
* Diversity measurement 
* Classification 

Combine embeddings with text generation capabilities and leverage specific sources of information to create a smart chat functionality tailored to your own knowledge base.

{{% alert color="info" %}}
See [RAG Example Implementation in the OpenAI Showcase Application](/appstore/modules/openai-connector/rag-example-implementation/) for more information on how to set up a vector database for retrieval augmented generation (RAG). Also, check out our [showcase app](https://marketplace.mendix.com/link/component/220475) for an example implementation.
{{% /alert %}}

### 1.2 Features {#features}

Mendix provides dual platform support for both [OpenAI](https://platform.openai.com/) and [Azure OpenAI](https://oai.azure.com/). 

With the current version, Mendix supports the Chat Completions API for [text generation](https://platform.openai.com/docs/guides/text-generation), the Image Generations API for [images](https://platform.openai.com/docs/guides/images), and the Embeddings API for [vector embeddings](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings). 

### 1.3 Limitations {#limitations}

The current scope of the connector is focused on text and image generation use cases, as well as embeddings. We try to release early and often, so keep your eyes open for new releases!

### 1.4 Prerequisites {#prerequisites}

You should have [signed up](https://platform.openai.com/) for an OpenAI account, or have access to deployments at [Azure OpenAI](https://oai.azure.com/).

### 1.5 Dependencies {#dependencies}

* Mendix Studio Pro version [9.24.0](/releasenotes/studio-pro/9.24/#9240) or higher 
* [Encryption](https://marketplace.mendix.com/link/component/1011) module
* [Community commons](https://marketplace.mendix.com/link/component/170) module

## 2 Installation {#installation}

Follow the instructions in [Using Marketplace Content](/appstore/overview/use-content/) to import the OpenAI Connector into your app. 

## 3 Configuration {#configuration}

After you install the OpenAI Connector, you can find it in the **App Explorer**, in the **Marketplace modules** section. The connector provides a [domain model](#domain-model) and several [activities](#activities) that you can use to connect your app to OpenAI. Each activity can be implemented by using it in a microflow. To ensure that your app can connect to OpenAI, you must also [configure the Encryption module](/appstore/modules/encryption/#configuration). 

### 3.1 General Configuration {#general-configuration}

1. Add the module role **OpenAIConnector.Administrator** to your Administrator user role in the security settings of your app. 
2. Add the **Configuration_Overview** page (**USE_ME > Configuration**) to your navigation or add the **Snippet_Configurations** to a page that is already part of your navigation. 
3. Continue to set up your OpenAI configuration at runtime. Based on the type of your configuration, continue with one of the following sections:
   * [OpenAI Configuration](#openai-configuration)
   * [Azure OpenAI Configuration](#azure-openai-configuration)

#### 3.1.1 OpenAI Configuration {#openai-configuration} 

The following inputs are required for the OpenAI configuration: 

| Parameter   | Value                                                        |
| ----------- | ------------------------------------------------------------ |
| DisplayName | This is the name identifier of a configuration, e.g. *MyConfiguration*. |
| API type    | Select `OpenAI`.<br />For more information, see the [ENUM_ApiType](#enum-apitype) section. |
| Endpoint    | This is the API Endpoint, e.g. `https://api.openai.com/v1`   |
| API key     | This is the access token to authorize your API call. <br />To get an API, follow these steps:<ol><li>Create an account and sign in at [OpenAI](https://platform.openai.com/).</li><li> Go to the [API key page](https://platform.openai.com/account/api-keys) to create a new secret key. </li><li>Copy the API key and save this somewhere safe.</li></ol> |

{{% alert color="info" %}}
If you have signed up for an OpenAI account and are using free trial credits, note that these are only valid for three months after the account has been created (not after the API key has been created). To continue using the OpenAI API with an account that is older than three months, you will need to top up your account balance with credit and create a new API key. <br />For more details, see the [OpenAI API reference](https://platform.openai.com/docs/api-reference/authentication).
{{% /alert %}}

#### 3.1.2 Azure OpenAI Configuration {#azure-openai-configuration} 

The following inputs are required for the Azure OpenAI configuration: 

| Parameter      | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| DisplayName    | This is the name identifier of a configuration, e.g. *MyConfiguration*. |
| API type       | Select `AzureOpenAI`.<br />For more information, see the [ENUM_ApiType](#enum-apitype) section. |
| Endpoint       | This is the API Endpoint, e.g. `https://your-resource-name.openai.azure.com/openai/deployments/`.<br />For more information about how to obtain `your-resource-name`, see the [Obtaining Azure OpenAI Resource Name](#azure-resource-name) section below. |
| DeploymentName | This is the deployment name you chose when you deployed the model. Deployments provide endpoints to the Azure OpenAI base models, or your fine-tuned models.<br />To check the deployment name, go to [Azure OpenAI](https://oai.azure.com/) and check the deployment name under **Deployments**. |
| API version    | This is the API version to use for this operation. This follows the `yyyy-MM-dd` format. See [Azure OpenAI documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference) for supported versions. Note that the supported versions can vary depending on the type of model, so make sure to look for the right section on that page (e.g. Chat completions, Image generation or Embeddings). |
| API key        | This is the access token to authorize your API call.         |
| Key type       | This is the type of token that is entered in the API key field. For Azure OpenAI, two types of keys are currently supported: `Microsoft Entra token` and `API key`. <br />For more information about how to generate a Microsoft Entra access token, see [How to Configure Azure OpenAI Service with Managed Identities](https://learn.microsoft.com/en-gb/azure/ai-services/openai/how-to/managed-identity). Alternatively, if your organization allows it, you could use the Azure **api-key** authentication mechanism. For more information about how to obtain an `API key`, see the [Obtaining Azure OpenAI API keys](#azure-api-keys) section below. For more information, see the [ENUM_KeyType](#enum-keytype) section. |

{{% alert color="info" %}}
For the Azure OpenAI configuration, each model needs a separate deployment so that it can be used. In order to benefit from multiple supported operations in your Mendix app, you need to create multiple configuration objects, one for every deployed model. For details, see the [Azure OpenAI Service REST API reference](https://learn.microsoft.com/en-gb/azure/ai-services/openai/reference).
{{% /alert %}}

##### 3.1.2.1 Obtaining Azure OpenAI Resource Name {#azure-resource-name}

1. Go to the [Azure OpenAI portal](https://oai.azure.com/) and sign in.
2. On the upper-right corner, click **Settings** ({{% icon name="cog" %}}). 
3. Go to the **Resource** tab.
4. Go to **Current resource** and click **JSON view**.
5. Use the value of the **name** field as your resource name in the endpoint URL.

##### 3.1.2.2 Obtaining Azure OpenAI API keys {#azure-api-keys}

1. Go to the [Azure OpenAI portal](https://oai.azure.com/) and sign in.
2. On the upper-right corner, click **Settings** ({{% icon name="cog" %}}). 
3. Go to the **Resource** tab.
4. Go to **Current resource** and click **JSON view**.
5. Use the value of the **key1** or **key2** field as your API key while setting up the configuration. Note that these keys might not be available depending on your organization's security settings. 

### 3.2 Chat Completions Configuration {#chat-completions-configuration} 

After following the general setup above, you are all set to use the microflows in the **USE_ME > Operations > ChatCompletions** folder in your logic. Currently, three microflows for chat completions are exposed as microflow actions under the **OpenAI Connector** category in the **Toolbox** in Mendix Studio Pro. 

These microflows expect a [Configuration](#configuration-entity) object, as well as the desired AI model that should be used for generating responses. 

* For the OpenAI API configuration, the desired model must be specified for every call.
* For the Azure OpenAI configuration, the model is already determined by the deployment in the [Azure OpenAI portal](https://oai.azure.com/portal). Any model explicitly specified will be ignored and hence can be left empty. 

In the context of chat completions, system prompts and user prompts are two key components that help guide the language model in generating relevant and contextually appropriate responses. For more information on prompt engineering, see the [Read More](#read-more) section. It varies per exposed microflow activity which prompts are required and how these must be passed, as described in the following sections. For more information, see the [ENUM_Role](#enum-role) section.

All chat completions operations within the OpenAI connector support [JSON mode](#enum-responseformat-chat), [function calling](#chatcompletions-functioncalling), and [vision](#chatcompletions-vision).

For more inspiration or guidance on how to use the above-mentioned microflows in your logic, Mendix highly recommends downloading our [showcase app](https://marketplace.mendix.com/link/component/220475) from the Marketplace that displays a variety of examples. 

#### 3.2.1 `Chat Completions (without history)` {#chatcompletions-without-history}

The microflow activity `Chat Completions (without history)` supports scenarios where there is no need to send a list of (historic) messages comprising the conversation so far as part of the request. The system prompt and user prompt are available as string input parameters. Depending on the use case, both or only one can be used. For technical details, see the [Technical reference](#chat-completions-without-history-technical) section.

Functionally, the prompt strings can be written in a specific way and can be tailored to get the desired result and behavior. For more information on prompt engineering, see the [Read More](#read-more) section.

Optionally, you can also make use of [function calling](#chatcompletions-functioncalling) by adding a [FunctionCollection](#functioncollection) or [send images](#chatcompletions-vision) along with the user prompt by adding an [ImageCollection](#imagecollection) as part of the request.

For technical details, see the [Technical reference](#chat-completions-without-history-technical) section.

#### 3.2.2 `Chat Completions (with history)` {#chatcompletions-with-withory}

The microflow activity `Chat completions with history` supports more complex use cases where a list of (historical) messages (e.g. comprising the conversation or context so far) is sent as part of the request to the language model.

Optionally, you can also make use of [function calling](#chatcompletions-functioncalling) by adding a [FunctionCollection](#functioncollection) or [send images](#chatcompletions-vision) along with the user prompt by adding an [ImageCollection](#imagecollection) as part of the request.

For technical details, see the [Technical reference](#chat-completions-with-history-technical) section.

#### 3.2.3 `Chat Completions (advanced)` {#chatcompletions-advanced}

The microflow activity `Chat Completions (advanced)` can be used in cases where the above-mentioned microflows do not provide enough support or flexibility. The interface of this operation resembles the API interface. The construction of the request and handling of the response must be implemented in a custom way.

For technical details, see the [Technical reference](#chat-completions-advanced-technical) section.

#### 3.2.4 Function Calling {#chatcompletions-functioncalling}

Function calling enables LLMs (Large Language Models) to connect with external tools to gather information, execute actions, convert natural language into structured data, and much more. Function calling thus enables the model to intelligently decide when to let the Mendix app call one or more predefined function microflows to gather additional information to include in the assistant's response.

OpenAI does not call the function. The model returns a tool call JSON structure that is used to build the input of the function(s) so that they can be executed as part of the chat completions operation. Functions in Mendix are essentially microflows that can be registered within the request to the LLM​. The OpenAI connector takes care of handling the tool call response as well as executing the function microflow(s) until the API returns the final assistant's response.

Function microflows take a single input parameter of type string and must return a string.

{{% alert color="warning" %}}
Function calling is a very powerful capability, but this also introduces potential risks. Function microflows do not respect any entity access rules for the current end-user. Make sure to retrieve and return only information that the end-user is allowed to view, otherwise confidential information may be visible to the current end-user in the assistant's response.

Mendix also strongly advises that you build user confirmation logic into function microflows that have a potential impact on the world on behalf of the end-user, for example sending an email, posting online, or making a purchase.
{{% /alert %}}

You can use function calling in all chat completions operations by providing the optional input parameter [FunctionCollection](#functioncollection).
Two helper microflow are available to construct the `FunctionCollection` with a list of `Functions`:

* `FunctionCollection_CreateAndAddFunction` can be used to initialize a new `FunctionCollection` and add a new `Function` to it.
* `FunctionCollection_AddFunction` can be used to add a new `Function` to an existing `FunctionCollection`.

For more information, see [Function Calling](/appstore/modules/openai-connector/function-calling/).

#### 3.2.5 Vision {#chatcompletions-vision}

Vision enables models like GPT-4 Turbo to interpret and analyze images, allowing them to answer questions and perform tasks related to visual content. This integration of computer vision and language processing enhances the model's comprehension and makes it valuable for tasks involving visual information. To make use of vision inside the OpenAI connector, an optional [ImageCollection](#imagecollection) containing one or multiple images must be sent along with a single message.

You can use vision in all chat completions operations by providing the optional input parameter [ImageCollection](#imagecollection). 

Two helper microflows are available to construct the `ImageCollection` with a list of `ChatCompletionImages`:

* `ImageCollection_CreateAndAddImage` can be used to initialize a new `ImageCollection` and add a new `ChatCompletionImage` to it.
* `ImageCollection_AddImage` can be used to add a new `ChatCompletionImage` to an existing `ImageCollection`.

For `Chat Completions without History` the `ImageCollection` is an optional input parameter, while for `Chat Completions with History` the `ImageCollection` can optionally be added to individual user messages in `ChatCompletionsSession_AddMessage`.

{{% alert color="info" %}}
OpenAI and Azure OpenAI for vision do not yet provide feature parity when it comes to combining functionalities, i.e., Azure OpenAI currently does not support the use of JSON mode and function calling in combination with image (vision) input.
Furthermore, when you use Azure OpenAI, it is recommended to set the optional `MaxTokens` input parameter so that the response will not be cut off.
{{% /alert %}}

For more information on vision, see [OpenAI](https://platform.openai.com/docs/guides/vision) and [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/gpt-with-vision) documentation.

### 3.3 Image Generations Configuration {#image-generations-configuration}

In order to implement image generations into your Mendix application, you can use the microflows in the **USE_ME > Operations > ImageGenerations** folder. Currently, two microflows for image generations are exposed as microflow actions under the **OpenAI Connector** category in the **Toolbox** in Mendix Studio Pro. 

These microflows, similar to the [Chat Completions](#chat-completions-configuration) case, expect a [Configuration](#configuration-entity) entity, as well as the desired AI model that should be used for generating image responses in the case of OpenAI configurations. In this case the field is optional, as OpenAI assumes a default value `dall-e-2`.

For more inspiration or guidance on how to use the below-mentioned microflows in your logic, Mendix highly recommends downloading our [showcase app](https://marketplace.mendix.com/link/component/220475) from the Marketplace that displays a variety of examples. 

#### 3.3.1 `Image Generations (single image)` {#imagegenerations-single}

The microflow activity `Image Generations (single image)` supports scenarios where a single image must be generated based on the provided prompt. In order to implement this operation, you must create a specialization of the [GeneratedImage](#generatedimage) entity. For every implementation of this microflow, an instance of this specialization has to be created first and must be passed into the `OutputImage` parameter of the microflow. If the call is successful, the image generated by the model will be stored into that object.
For technical details, see the [Technical reference](#image-generations-single-technical) section.

#### 3.3.2 `Image Generations (advanced)` {#imagegenerations-advanced}

The microflow activity `Image Generations (advanced)` can be used in cases where the above-mentioned microflows do not provide enough support or flexibility. The interface of this operation resembles the API interface. The construction of the request and handling of the response must be implemented in a custom way. One accompanying microflow is available to construct the input for the microflow:

* `ImageGenerationsRequest_Create` is used to create the request object.

The construction of the request and handling of the response must be implemented in a custom way.

For technical details, see the [Technical reference](#image-generations-advanced-technical) section.

### 3.4 Embeddings Configuration {#embeddings-configuration}

In order to implement embeddings into your Mendix application, you can use the microflows in the **USE_ME > Operations > Embeddings** folder. Currently, three microflows for embeddings are exposed as microflow actions under the **OpenAI Connector** category in the **Toolbox** in Mendix Studio Pro. 

These microflows expect a [Configuration](#configuration-entity) entity, as well as the desired AI model that should be used for generating responses. 

* For the OpenAI API configuration, the desired model must be specified for every call.
* For the Azure OpenAI configuration, the model is already determined by the deployment in the [Azure OpenAI portal](https://oai.azure.com/portal). Any model explicitly specified will be ignored and hence can be left empty. 

#### 3.4.1 `Embeddings (single input)` {#embeddings-single}

The microflow activity `Embeddings (single input)` supports scenarios where the vector embedding of a single string must be generated. This input string can be passed directly as the `Input` parameter of this microflow. Note that the parameter `EncodingFormat` is optional; the current version of this operation only supports the float representation of the resulting vector.

For technical details, see the [Technical reference](#embeddings-single-technical) section.

#### 3.4.2 `Embeddings (list input)` {#embeddings-list}

The microflow activity `Embeddings (list input)` supports the more complex scenario where a list of strings must be vectorized in a single API call, e.g. converting a batch of text strings (chunks) from a private knowledge base into embeddings. Instead of calling the API for each string, executing a single call for a list of strings can significantly reduce HTTP overhead. The embedding vectors returned after a successful API call will be stored as `EmbeddingVector` attribute in the same `DataChunk` entity. Thus, the microflow does not return an Object or List, but only a `Success` Boolean. Two accompanying microflows are available to help construct the input for the main microflow: 

* `DataBatch_Create` is used to create the wrapper object for the list of `DataChunk` objects that must be passed as input parameter. 
* `DataChunk_Create` can be used repetitively to attach a chunk of text (as a string) to the `DataBatch` entity. 

For technical details, see the [Technical reference](#embeddings-list-technical) section.

#### 3.4.3 `Embeddings (advanced)` {#embeddings-advanced}

The microflow activity `Embeddings (advanced)` can be used in cases where the above-mentioned microflows do not provide enough support or flexibility. The interface of this operation resembles the API interface. Two accompanying microflows are available to help construct the input for the main microflow: 

* `EmbeddingsRequest_Create` is used to create the request object.
* `EmbeddingsInput_Create` is used to create the input object.

The construction of the request and handling of the response must be implemented in a custom way.

For technical details, see the [Technical reference](#embeddings-advanced-technical) section.

## 4 Technical Reference {#technical-reference}

To help you work with the **OpenAI Connector**, the following sections list the available [entities](#domain-model), [enumerations](#enumerations), and [activities](#activities) that you can use in your application. 

### 4.1 Domain Model {#domain-model} 

The domain model in Mendix is a data model that describes the information in your application domain in an abstract way. For more general information, see [Domain model](/refguide/domain-model/). To learn about where the entities from the domain model are used and relevant during implementation, see the [Activities](#activities) section below.

#### 4.1.1 Configuration {#configuration-domain-model}

{{< figure src="/attachments/appstore/modules/openai-connector/domain-model-configuration.png" >}}

##### 4.1.1.1 `Configuration` {#configuration-entity} 

`Configuration` is used to store the API credentials and endpoints in the configuration for OpenAI or Azure OpenAI .

| Attribute        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `DisplayName`    | This is the name identifier of a configuration.              |
| `ApiType`        | The value can be `OpenAI` or `AzureOpenAI`.<br />For more information, see the [ENUM_ApiType](#enum-apitype) section. |
| `Endpoint`       | This is the API Endpoint, e.g. `https://api.openai.com/v1` for OpenAI, or `https://your-resource-name.openai.azure.com/openai/deployments/`for Azure OpenAI. |
| `DeploymentName` | This is the deployment name you chose when you deployed the model. This is only relevant for configurations of `ApiType` **AzureOpenAI**. Deployments provide endpoints to the Azure OpenAI base models, or your fine-tuned models.<br />To check the deployment name, follow these steps:<ol><li>Sign in at [Azure OpenAI](https://oai.azure.com/).</li><li>Navigate to deployments in the sidebar.</li></ol> |
| `ApiVersion`     | This the API version used for this operation. This follows the `YYYY-MM-DD` format. Only relevant for configurations of `ApiType` **AzureOpenAI**. |
| `ApiKey`        | This is the access token to authorize your API call. <br />For details, see the [OpenAI configuration](#openai-configuration) and [Azure OpenAI configuration](#azure-openai-configuration) sections. |
| `KeyType`        | This is the type of token entered in the `ApiKey` field. This is only relevant for configurations of `ApiType` **AzureOpenAI**.<br />For more information, see the [ENUM_ApiType](#enum-keytype) section. |

##### 4.1.1.2 `ApiKey` {#apikey}

`ApiKey` is only used for editing the `ApiKey` to be stored in the [Configuration](#configuration-entity) entity. 

| Attribute | Description                                          |
| --------- | ---------------------------------------------------- |
| `ApiKey`  | This is the access token to authorize your API call. |

##### 4.1.1.3 `ConfigurationTest` {#configurationtest}

`ConfigurationTest` is only used to send a simple [chat completions request](#chat-completions-without-history-technical) to test an existing [configuration](#configuration-entity).

| Attribute              | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `UserPrompt`           | This is the user message sent to the chat completions API.   |
| `AssistantResponse`    | This is the assistant response returned by the chat completions API. |
| `ChatCompletionsModel` | This is the model used for the API call.                     |

#### 4.1.2 Generalizations {#generalizations-domain-model}

{{< figure src="/attachments/appstore/modules/openai-connector/domain-model-generalizations.png" >}}

##### 4.1.2.1 `AbstractUsage` {#abstractusage}

`AbstractUsage` contains usage statistics for an API call. Do not use this entity directly. Instead, use one of its specializations.

| Attribute       | Description                                             |
| --------------- | ------------------------------------------------------- |
| `Prompt_tokens` | This is the number of tokens in the prompt.             |
| `Total_tokens`  | This is the total number of tokens used in the request. |

For more information on how to manage tokens for text generation, see [Managing tokens](https://platform.openai.com/docs/guides/text-generation/managing-tokens).

##### 4.1.2.2 `AbstractChatCompletionsMessage` {#abstractchatcompletionsmessage} 

`AbstractChatCompletionsMessage` is the abstract entity for `ChatCompletionsMessage`. Do not use this entity directly. Instead, use one of its specializations. 

| Attribute     | Description                                                  |
| --------------| ------------------------------------------------------------ |
| `Content`     | This is the content of a message.                            |
| `Role`        | This is the role of the message author.<br />For more information, see the [ENUM_Role](#enum-role) section. |
| `ToolCallId`  | Tool call that this message is responding to. Only applicable and required for messages with role `tool`.                |

##### 4.1.2.3 `AbstractTool` {#abstracttool}

`AbstractTool` is the abstract entity for `Tool` reused in the Chat Completions request and response. Do not use this entity directly. Instead, use one of its specializations. 

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `ToolType`| The type of the tool. Currently, only function is supported. <br />For more information, see the [ENUM_ToolType](#enum-tooltype) section. |

##### 4.1.2.4 `AbstractFunction` {#abstractfunction}

`AbstractFunction` is the abstract entity for `Function` reused in the Chat Completions request and response. Do not use this entity directly. Instead, use one of its specializations. 

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `Name`    | The name of the function to call.                            |

#### 4.1.3 Chat Completions {#chatcompletions-domain-model}

{{< figure src="/attachments/appstore/modules/openai-connector/domain-model-chat-completions.png" >}}

##### 4.1.3.1 `ChatCompletionsRequest` {#chatcompletionsrequest} 

`ChatCompletionsRequest` is a chat completions request that creates a model response for the given chat conversation. 

| Attribute           | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `Model`             | This is required for requests to OpenAI. Model is NOT considered for request to Azure OpenAI, because the model is determined by the deployment.<br />For more information, see the [compatible models](https://platform.openai.com/docs/models) in the OpenAI documentation. |
| `Frequency_penalty` | The value should be a decimal between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood of repeating the same line verbatim. This attribute is optional. The default value is 0.0. |
| `Max_tokens`        | This is the maximum number of tokens to generate in the chat completion. The total length of input tokens and generated tokens is limited by the model's context length. This attribute is optional. |
| `Temperature`       | This is the sampling temperature. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. This attribute is optional. The value should be a decimal between 0.0 and 2.0. The default value is 1.0. |
| `Top_p`             | This is an alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with `Top_p` probability mass. 0.1 means only the tokens comprising the top 10% probability mass are considered. Mendix generally recommends altering `Top_p` or `Temperature` but not both. This attribute is optional. The value should be a decimal between 0.0 and 1.0. The default value is 1.0. |
| `N`                 | This is the number of chat completions choices to generate for each input message. You will be charged based on the number of generated tokens across all choices. Keep `N` as 1 to minimize costs. This attribute is optional. The default value is 1. |
| `ToolChoice`        | This optional attribute controls which (if any) function is called by the model. <br />For more information, see the [ENUM_ToolChoice](#enum-toolchoice) section. |

{{% alert color="info" %}}The request and response parts of the domain model were designed to portray the [API reference of OpenAI](https://platform.openai.com/docs/api-reference/chat/create) as close as possible.{{% /alert %}}

##### 4.1.3.2 `ResponseFormat` {#responseformatchat}

`ResponseFormat` specifies the format that the chat completions model must output. 

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `_Type`   | This describes the format that the chat completions model must output. <br />For more information, see the [ENUM_ResponseFormat_Chat](#enum-responseformat-chat) section. |

##### 4.1.3.3 `ChatCompletionsMessages` {#chatcompletionsmessages}

`ChatCompletionsMessages` is a wrapper for a list of messages comprising the conversation so far. 

##### 4.1.3.4 `ChatCompletionsMessageRequest` {#chatcompletionsmessagerequest}

`ChatCompletionsMessageRequest` is a specialization of the [AbstractChatCompletionsMessage](#abstractchatcompletionsmessage) entity. Each instance contains a text that needs to be taken into account by the model when processing the completion request. 

##### 4.1.3.5 `ImageCollection` {#imagecollection}

`ImageCollection` is a wrapper for an optional list of images to be sent along with the `ChatCompletionsMessageRequest` to use vision. `ImageCollections` can only be sent along messages with role `User`.

##### 4.1.3.6 `ChatCompletionsImage` {#chatcompletionsimage}

`ChatCompletionsImage` is an image that is part of the `ChatCompletionsMessageRequest`. Only applicable for messages with role user.

| Attribute      | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| `ImageContent` | Image content is either a URL of the image or the base64-encoded image data. |
| `Detail`       | This optional attribute specifies the detail level of the image. <br />For more information, see the [ENUM_ImageDetail](#enum-imagedetail) section. Defaults to `auto`. |

##### 4.1.3.7 `ToolCall` {#toolcall}

`ToolCall` is a specialization of the [AbstractTool](#abstracttool) entity and represents the tool calls generated by the model, such as function calls. The ToolCall entity is only applicable for messages with role `assistant`.

| Attribute | Description                                    |
| --------- | -----------------------------------------------|
| `_id`     | The ID of the tool call, generated by the LLM. |

##### 4.1.3.8 `ToolCallFunction` {#toolcallfunction}

`ToolCallFunction` is a specialization of the [AbstractFunction](#abstractfunction) entity and represents the function that the model called.
The ToolCallFunction entity is only applicable for messages with role `assistant`.

| Attribute  | Description                                    |
| ---------- | -----------------------------------------------|
| `Arguments`| The arguments to call the function with, as generated by the model in JSON format. Note that the model does not always generate valid JSON, and may hallucinate parameters not defined by your function schema. Validate the arguments before using them. |

##### 4.1.3.9 `Tools` {#tools}

`Tools` is a wrapper for a list of tools the model may call. Currently, only functions are supported as as tools. A maximum of 128 functions are supported.

##### 4.1.3.10 `ToolRequest` {#toolrequest}

`ToolRequest` is a specialization of the [AbstractTool](#abstracttool) entity and represents a tool the model may call.

##### 4.1.3.11 `FunctionRequest` {#functionrequest}

`FunctionRequest` is a specialization of the [AbstractFunction](#abstractfunction) entity and represents a function the model may call.

| Attribute          | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| `Description`      | A description of what the function does, used by the model to choose when and how to call the function. This attribute is optional, but Mendix suggests using it to help the model choose the correct function. |
| `FunctionMicroflow`| The microflow that is called within this function. A function microflow can only have a single String input parameter and returns a String. Note that function microflows do not respect the entity access rules for the current end-user. Make sure that you only return information that the end-user is allowed to view, otherwise confidential information may be visible to the current end-user in the assistant's response. |

##### 4.1.3.12 `ChatCompletionsResponse` {#chatcompletionsresponse} 

 `ChatCompletionsResponse` represents a chat completion response returned by the model, based on the provided input. 

| Attribute            | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `_id`                | This is a unique identifier for the chat completion.         |
| `_object`            | This is the object type, which is always *chat.completion*.  |
| `Created`            | This is the Unix timestamp (in seconds) of when the chat completion was created. |
| `Model`              | This is the model that was used for the chat completion.     |
| `System_fingerprint` | This fingerprint represents the backend configuration that the model runs with. The value can be used in conjunction with the seed request parameter to understand when backend changes have been made that might impact determinism. |

{{% alert color="info" %}} The request and response parts of the domain model were designed to portray the [API reference of OpenAI](https://platform.openai.com/docs/api-reference/chat/create) as close as possible.{{% /alert %}}

##### 4.1.3.13 `Choice` {#choicechat}

 `Choice` is a list of chat completion choices which are part of the response. There can be more than one choice if `N` in the [request](#chatcompletionsrequest) is greater than 1, meaning that there was an explicit request for multiple alternative response texts. Each is used as a wrapper entity for the actual message content. 

| Attribute       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `Index`         | This is the index of the choice in the list of choices.      |
| `Finish_reason` | This is the reason the model stopped generating tokens. This will be `stop` if the model hit a natural stop point or a provided stop sequence, `length` if the maximum number of tokens specified in the request was reached, `content_filter` if content was omitted due to a flag from our content filters, or `tool_calls` if the model called a tool. |

##### 4.1.3.14 `ChatCompletionsMessageResponse` {#chatcompletionsmessageresponse}

`ChatCompletionsMessageResponse` is a specialization of the [AbstractChatCompletionsMessage](#abstractchatcompletionsmessage) entity. It contains the response text (assistant prompt). 

##### 4.1.3.15 `ChatCompletionsUsage` {#chatcompletionsusage}

`ChatCompletionsUsage` is a specialization of the [AbstractUsage](#abstractusage). It contains the statistics for the completion request with an additional attribute:

| Attribute           | Description                                               |
| ------------------- | --------------------------------------------------------- |
| `Completion_tokens` | This is the number of tokens in the generated completion. |

##### 4.1.3.16 `ChatCompletionsSession` {#chatcompletionssession} 

`ChatCompletionsSession` is a wrapper object for a chat completions session. It is associated with a list of (historical) messages comprising the conversation so far that can be mapped to the chat completions request. 

##### 4.1.3.17 `FunctionCollection` {#functioncollection}

 `FunctionCollection` is a wrapper for a collection of functions to be sent along with the ChatCompletionsRequest as tools.

##### 4.1.3.18 `Function` {#function} 

 `Function` is a specialization of the [FunctionRequest](#functionrequest) entity and represents a function the model may call.

##### 4.1.3.19 `ChatCompletionsSessionMessage` {#chatcompletionssessionmessage}

`ChatCompletionsSessionMessage` is a specialization of the [AbstractChatCompletionsMessage](#abstractchatcompletionsmessage) entity. 

#### 4.1.4 Image Generations {#imagegenerations-domain-model}

{{< figure src="/attachments/appstore/modules/openai-connector/domain-model-images.png" >}}

##### 4.1.4.1 `ImageGenerationsRequest` {#imagegenerationsrequest} 

`ImageGenerationsRequest` is an image generations request that creates a model response including generated image (or images) for the given prompt. 

| Attribute        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `Prompt`         | This is the prompt that is used by the model to generate the image (or images) . |
| `Model`          | The model to use for image generation. This is an optional field for OpenAI. Its default value is `dall-e-2`. <br />For more information, see the [compatible models](https://platform.openai.com/docs/models) in the OpenAI documentation. |
| `N`              | This is the number of images to generate. The value must be between 1 and 10. For `dall-e-3`, only n=1 is supported. This attribute is optional. |
| `Quality`        | This is the requested quality of the generated images. This attribute is optional and only supported for `dall-e-3`. It defaults to `standard`.<br />For more information, see the [ENUM_Quality](#enum-quality) section. |
| `ResponseFormat` | This is a parameter used to specify the technical format of the returned generated images by the API. This attribute is optional. The default value is  `url`. <br />For more information see the [ENUM_ResponseFormat_Image](#enum-responseformat-image) section. |
| `Size`           | This is the requested size of the generated images. This attribute is optional. Its default value is `1024x1024`.<br />For more information see the [ENUM_Size](#enum-size) section. |
| `Style`          | This is the style of the generated images. This attribute is optional. Its default value is `vivid`.<br />For more information, see the [ENUM_Style](#enum-style) section. |
| `User`           | This is a unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. This attribute is optional. |

{{% alert color="info" %}}The request and response parts of the domain model were designed to portray the [API reference of OpenAI](https://platform.openai.com/docs/api-reference/images/create) as close as possible.{{% /alert %}}

##### 4.1.4.2 `ImageGenerationsResponse` {#imagegenerationsresponse} 

`ImageGenerationsResponse` represents an image generations response returned by the model, based on the provided input. 

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `Created` | This is the Unix timestamp (in seconds) of when the image generation was created. |

##### 4.1.4.3 `Data` {#dataimage}

 `Data` is a wrapper for a list of [images](#image) that are part of the [response](#imagegenerationsresponse). 

##### 4.1.4.4 `Image` {#image}

 `Image` represents the URL or the content of an image generated by the API.

| Attribute       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `Url`           | This is the URL of the generated image that can be used to fetch the image data if the `responseFormat` is `url`. <br />{{% alert color="info" %}}URLs typically expire after a certain time.{{% /alert %}} |
| `B64Json`       | This is the base64-encoded string representation of the generated image that can be used to process the image data if the `responseFormat` is `b64_json`. |
| `RevisedPrompt` | This is the prompt that was used to generate the image. It is only populated if there was any revision to the prompt. |

{{% alert color="info" %}} The request and response parts of the domain model were designed to portray the [API reference of OpenAI](https://platform.openai.com/docs/api-reference/chat/create) as close as possible.{{% /alert %}}

##### 4.1.4.5 `GeneratedImage` {#generatedimage}

`GeneratedImage` is an entity that is used to map the [image](#image) data from the API response onto a Mendix image entity so that it can be used as such in the application. 

| Attribute       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `RevisedPrompt` | This is the prompt that was used to generate the image. It is only populated if there was any revision to the prompt. |

{{% alert color="info" %}} This entity is meant to be used as a generalization when one of the [exposed microflows for image generations](#image-generations-technical) is implemented. For more information about how to use this entity, see the [Image Generations Configuration](#image-generations-configuration) section. {{% /alert %}}

#### 4.1.5 Embeddings {#embeddings-domain-model}

{{< figure src="/attachments/appstore/modules/openai-connector/domain-model-embeddings-with-data-batch.png" >}}

##### 4.1.5.1 `EmbeddingsRequest` {#embeddingsrequest} 

`EmbeddingsRequest` is an embeddings request that generates a model response including a vector embedding per given input string text. 

| Attribute         | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `Model`           | This is the model used for generating embeddings. This is a mandatory field for OpenAI.<br />For more information, see the [compatible models](https://platform.openai.com/docs/models) in the OpenAI documentation. |
| `Encoding_format` | This is the format in which the embeddings are returned. The connector currently only supports float and not base64.<br />For more information see the [ENUM_EncodingFormat_Embeddings](#enum-encodingformat-embeddings) section. |
| `User`            | This is a unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. This attribute is optional. |

{{% alert color="info" %}}The request and response parts of the domain model were designed to portray the [API reference of OpenAI](https://platform.openai.com/docs/api-reference/images/create) as close as possible.{{% /alert %}}

##### 4.1.5.2 `EmbeddingsInput` {#embeddingsinput}

`EmbeddingsInput` is an entity that is used to contain a string input text for the embeddings model. 

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `Input`   | This is the string input for a text chunk for which the embedding vector needs to be generated. |

##### 4.1.5.3 `EmbeddingsResponse` {#embeddingsresponse}

`EmbeddingsResponse` represents an embeddings response returned by the model, based on the provided input.

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `_object` | This is the object type, which is always `list`.             |
| `Model`   | This is the model that has been used for generating the embeddings. |

##### 4.1.5.4 `EmbeddingsUsage`  {#embeddingsusage}

`EmbeddingsUsage` is a specialization of the [AbstractUsage](#abstractusage) entity. It represents usage statistics for the embeddings request that was processed.

##### 4.1.5.5 `EmbeddingVector` {#embeddingvector}

`EmbeddingVector` is the vector that represents the embedding for the text input that was given in the request. There will be an instance of this entity for every input text string provided.

| Attribute | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `_object` | This is the object type, which is always `embedding`.        |
| `Index`   | This is the index of the embedding in the list of embeddings. This can be used for ordering. |

##### 4.1.5.6 `EmbeddingValue` {#embeddingvalue}

`EmbeddingValue` represents an element in the list of floats in the embedding vector returned by the API. It is a separate entity for mapping purposes and is only relevant for the [encoding format](#enum-encodingformat-embeddings) option `float`. The length of the vector depends on the model as listed in the [documentation](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings) of OpenAI.

| Attribute | Description                                |
| --------- | ------------------------------------------ |
| `Value`   | This is a decimal in the embedding vector. |

##### 4.1.5.7 `DataBatch` {#databatch}

`DataBatch` functions as a wrapper object for the [list input operation for embeddings](#embeddings-list-technical). It is associated with a list of input objects of entity [DataChunk](#datachunk) that contain the string texts for which the embedding vectors must be generated. 

##### 4.1.5.8 `DataChunk` {#datachunk}

`DataChunk` represents a text string, usually a part of a larger base text or discrete piece of text in a data set. It is designed to contain the input string and the corresponding embedding vector retrieved from the Embeddings API.

| Attribute         | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `Input`           | This is the input text to embed will be mapped to the `EmbeddingsInput` entity as part of the request. |
| `EmbeddingVector` | This is the string representation of the embedding vector of the input string. |
| `Index`           | This is used for mapping the EmbeddingVector from the response onto the correct DataChunk in the list. |

### 4.2 Enumerations {#enumerations} 

An enumeration is a predefined list of values that can be used as an attribute type. For more information about enumerations in general, see [Enumerations](/refguide/enumerations/). 

#### 4.2.1 General {#general-enumerations}

##### 4.2.1.1 `ENUM_ApiType` {#enum-apitype} 

 `ENUM_ApiType` provides a list of supported API types. 

| Name          | Caption          |
| ------------- | ---------------- |
| `AzureOpenAI` | **Azure OpenAI** |
| `OpenAI`      | **OpenAI**       |

##### 4.2.1.2 `ENUM_KeyType` {#enum-keytype}

`ENUM_KeyType` provides a list of key types that can be used during the connection to the APIs of Azure OpenAI. 

| Name           | Caption                   |
| -------------- | ------------------------- |
| `Bearer_Token` | **Microsoft Entra token** |
| `API_key`      | **API key**               |

##### 4.2.1.3 `ENUM_ToolType` {#enum-tooltype}

`ENUM_ToolType` is the type of the tool. Currently, only function is supported.

| Name           | Caption                   |
| -------------- | ------------------------- |
| `Function`     | **Function**              |

#### 4.2.2 Chat Completions {#chatcompletions-enumerations}

##### 4.2.2.1 `ENUM_Role` {#enum-role} 

 `ENUM_Role` provides a list of message author roles. 

| Name        | Caption       | Description                                                  |
| ----------- | ------------- | ------------------------------------------------------------ |
| `assistant` | **Assistant** | An assistant message was generated by the model as a response to a user message. |
| `system`    | **System**    | A system message can be used to specify the assistant persona or give the model more guidance and context. This is typically specified by the developer to steer the model response. |
| `user`      | **User**      | A user message is the input from an end-user.                     |
| `tool`      | **Tool**      | A tool message contains the return value of a tool call as it's content. Additionally, a tool message has a ToolCallId that is used to map it to the corresponding previous assistant response which provided the tool call input. |

##### 4.2.2.2 `ENUM_ResponseFormat_Chat` {#enum-responseformat-chat} 

`ENUM_ResponseFormat_Chat` provides a list of supported response types for chat completions. Currently chat completions can be returned in normal text format (supported for all chat completions models available in the connector), as well as in JSON mode for [specific models](https://platform.openai.com/docs/guides/text-generation/json-mode).

| Name          | Caption        | Description               |
| ------------- | -------------- | ------------------------- |
| `json_object` | **JSONObject** | Model should return json. |
| `text`        | **Text**       | Model should return text. |

##### 4.2.2.3 `ENUM_ToolChoice` {#enum-toolchoice} 

 `ENUM_ToolChoice` controls which (if any) function is called by the model.

| Name          | Caption        | Description                                                             |
| ------------- | -------------- | ----------------------------------------------------------------------- |
| `auto`        | **auto**       | The model can pick between generating a message or calling a function.  |
| `none`        | **none**       | The model will not call a function and instead generate a message.     |
| `function`    | **function**   | A particular function needs to be called, which is specified over association to the specific [Function](#function) or [ToolRequest](#toolrequest). |

##### 4.2.2.4 `ENUM_ImageDetail` {#enum-imagedetail} 

`ENUM_ImageDetail` specifies the detail level of the image. For more information, see [low or high fidelity image understanding](https://platform.openai.com/docs/guides/vision/low-or-high-fidelity-image-understanding).

| Name   | Caption  | Description                                                  |
| ------ | -------- | ------------------------------------------------------------ |
| `auto` | **auto** | By default, the model will use the `auto` setting which will consider the image input size and decide whether it should use the `low` or `high` setting. |
| `low`  | **low**  | `low` will enable the "low res" mode. The model will receive a low-resolution 512 px x 512 px version of the image, and represent the image with a budget of 65 tokens. This allows the API to return faster responses and consume fewer input tokens for use cases that do not require high detail. |
| `high` | **high** | `high` will enable the "high res" mode, which first allows the model to see the low-resolution image and then creates detailed crops of input images as 512 px squares based on the input image size. Each of the detailed crops uses twice the token budget (65 tokens) for a total of 129 tokens. |

#### 4.2.3 Image Generations {#imagegenerations-enumerations}

##### 4.2.3.1 `ENUM_ResponseFormat_Image` {#enum-responseformat-image} 

`ENUM_ResponseFormat_Image` provides a list of supported response types for generated images. Currently, images can be returned either as a URL to a PNG file, or a base64-encoded string representation of the image directly.

| Name       | Caption         |
| ---------- | --------------- |
| `url`      | **URL**         |
| `b64_json` | **Base64-JSON** |

##### 4.2.3.2 `ENUM_Size` {#enum-size} 

`ENUM_Size` provides a list of supported pixel dimensions for the generated images. It depends on the model which options are supported.

{{% alert color="info" %}}In this case, the captions are the values that are relevant for the raw API calls, since enumeration key values do not allow certain characters.{{% /alert %}}

| Name         | Caption       |
| ------------ | ------------- |
| `_256x256`   | **256x256**   |
| `_512x512`   | **512x512**   |
| `_1024x1024` | **1024x1024** |
| `_1204x1792` | **1024x1792** |
| `_1792x1024` | **1792x1024** |

##### 4.2.3.3 `ENUM_Style` {#enum-style} 

`ENUM_Style` provides a list of supported visual styles for the generated images. It depends on the model whether this field is supported.

| Name      | Caption     |
| --------- | ----------- |
| `vivid`   | **Vivid**   |
| `natural` | **Natural** |

##### 4.2.3.4 `ENUM_Quality` {#enum-quality} 

`ENUM_Quality` provides a list of quality levels for the images that are generated. 

| Name       | Caption      |
| ---------- | ------------ |
| `standard` | **Standard** |
| `hd`       | **HD**       |

#### 4.2.4 Embeddings {#embeddings-enumerations}

##### 4.2.4.1 `ENUM_EncodingFormat_Embeddings` {#enum-encodingformat-embeddings}

`ENUM_EncodingFormat_Embeddings` provides a list of supported encoding formats for embeddings returned by the API. The connector operations currently only support the floating point representation of embedding vectors and not base64. Therefore, only one value `float` exits.

| Name     | Caption   |
| -------- | --------- |
| `_float` | **float** |

{{% alert color="info" %}}In this case, the captions are the values that are relevant for the raw API calls, since enumeration key values do not allow certain characters or words.{{% /alert %}}

### 4.3 Activities {#activities} 

Activities define the actions that are executed in a microflow or a nanoflow.

#### 4.3.1 Chat Completions {#chatcompletions-technical}

The chat completions API from OpenAI accepts a complex JSON structure that consists of a number of parameters plus one or more messages as input and generates a model-generated message structure as output. While the chat structure is designed for facilitating multi-turn conversations (with history), it is equally valuable for single-turn tasks that do not involve any prior conversation (without history). The exposed microflows in this connector are built to abstract away the complex message structure and are meant to facilitate easier implementation in certain use cases. All chat completions operations support [JSON mode](#enum-responseformat-chat), [function calling](#chatcompletions-functioncalling), and [vision](#chatcompletions-vision).

##### 4.3.1.1 Chat Completions (Without History) {#chat-completions-without-history-technical} 

Use the microflow `ChatCompletions_Execute_WithoutHistory` to execute a simple chat completions API call with string input and output not considering a previous conversation. See [ENUM_Role](#enum-role) for the difference between `UserPrompt` and `SystemPrompt`. It is not required to provide a `SystemPrompt` string. The `Model` value is mandatory for OpenAI, but is ignored for Azure OpenAI type configurations where it is implicitly specified by the deployment already.
For [specific models](https://platform.openai.com/docs/guides/text-generation/json-mode) it is possible to force the assistant response to be a valid JSON structure using the optional `ENUM_ResponseFormat_Chat` [parameter](#enum-responseformat-chat); if no value is specified, the default value as specified in the [OpenAI documentation](https://platform.openai.com/docs/api-reference/chat/create) will be assumed by the API. 

**Input parameters**

| Name             | Type                                                  | Mandatory                     | Description                                                  |
| ---------------- | ----------------------------------------------------- | ----------------------------- | ------------------------------------------------------------ |
| `UserPrompt`     | String                                                | mandatory                     | A user message is the input from a user.                     |
| `SystemPrompt`   | String                                                | optional                      | A system message can be used to specify the assistant persona or give the model more guidance and context. |
| `Configuration`  | [Configuration](#configuration-entity)                | mandatory                     | This is an object that contains endpoint and API key.        |
| `Model`          | String                                                | only mandatory for **OpenAI** | This is the ID of the model to use; not considered for **Azure OpenAI** configurations. |
| `ResponseFormat` | [ENUM_ResponseFormat_Chat](#enum-responseformat-chat) | optional                      | This can be used to specify the format that the model must output. |
| `Temperature`    | Decimal                                               | optional                      | This can be used to control the randomness of the output. The value should be a decimal between 0.0 and 2.0. The default value is 1.0. Higher values make the output more random, while lower values make it more focused and deterministic. Note: very high values for temperature (>1.7) may give unexpected results and even internal server errors. |
| `MaxTokens`      | Integer                                               | optional                      | This is the maximum number of tokens to generate in the chat completion. |
| `FunctionCollection`    | Object                                         | optional                      | This is a collection of functions to be sent along with the ChatCompletionsRequest as tools to use function calling. |
| `ImageCollection`| Object                                                | optional                      | This is a collection of images to be sent along with the `UserPrompt` to use vision. |

**Return value**

| Name                    | Type   | Description                                                  |
| ----------------------- | ------ | ------------------------------------------------------------ |
| `AssistantResponseText` | String | An assistant message was generated by the model as a response to a user message. |

Four accompanying microflows are available to construct the input for the microflow:

Function calling:
* `FunctionCollection_CreateAndAddFunction` can be used to initialize a new `FunctionCollection` and add a new `Function` to it in order to enable [function calling](#chatcompletions-functioncalling).
* `FunctionCollection_AddFunction` can be used to add a new `Function` to an existing `FunctionCollection`.

Vision:
* `ImageCollection_CreateAndAddImage` can be used to initialize a new `ImageCollection` and add a new `ChatCompletionImage` to it in order to enable [vision](#chatcompletions-vision).
* `ImageCollection_AddImage` can be used to add a new `ChatCompletionImage` to an existing `ImageCollection`.

##### 4.3.1.2 Chat Completions (with History) {#chat-completions-with-history-technical}

Use the microflow `ChatCompletions_Execute_WithHistory` to execute a chat completions API call with a [ChatCompletionsSession](#chatcompletionssession) input and a string output of the assistant response. It is not required to provide a `SystemPrompt` string. The `Model` value is mandatory for OpenAI, but is ignored for Azure OpenAI type configurations where it is implicitly specified by the deployment already. For certain models it is possible to force the assistant response to be a valid JSON structure using the optional `ENUM_ResponseFormat_Chat` [parameter](#enum-responseformat-chat); if no value is specified, the default value as specified in the [OpenAI documentation](https://platform.openai.com/docs/api-reference/chat/create) will be assumed by the API.

**Input parameters**

| Name                     | Type                                                  | Mandatory                     | Description                                                  |
| ------------------------ | ----------------------------------------------------- | ----------------------------- | ------------------------------------------------------------ |
| `ChatCompletionsSession` | String                                                | mandatory                     | This is a wrapper object for a list of messages comprising the conversation so far. |
| `Configuration`          | [Configuration](#configuration-entity)                | mandatory                     | This is an object that contains endpoint and API key.        |
| `Model`                  | String                                                | only mandatory for **OpenAI** | This is the ID of the model to use; not considered for **Azure OpenAI** configurations. |
| `ResponseFormat`         | [ENUM_ResponseFormat_Chat](#enum-responseformat-chat) | optional                      | This can be used to specify the format that the model must output. |
| `Temperature` | Decimal | optional | This can be used to control the randomness of the output. The value should be a decimal between 0.0 and 2.0. The default value is 1.0. Higher values make the output more random, while lower values make it more focused and deterministic. Note: very high values for temperature (>1.7) may give unexpected results and even internal server errors. |
| `MaxTokens`              | Integer                                               | optional                      | This is the maximum number of tokens to generate in the chat completion. |
| `FunctionCollection`     | Object                                                | optional                      | A collection of functions to be sent along with the ChatCompletionsRequest as tools. |

**Return value**

| Name                    | Type   | Description                                                  |
| ----------------------- | ------ | ------------------------------------------------------------ |
| `AssistantResponseText` | String | Assistant message that was generated by the model as a response to a user message. |

The following microflows may be used to construct and handle the required inputs: 

* `ChatCompletionsSession_Create` is used to create the session wrapper that must be passed as input parameter. 
* `ChatCompletionsSession_AddMessage` is used to attach the historical messages to the `ChatCompletionsSession`. If multiple messages are relevant, these should be added chronologically. `ImageCollection_CreateAndAddImage` and `ImageCollection_AddImage` can be used to create an `ImageCollection` which is in turn to be added to a user message in order to enable [vision](#chatcompletions-vision).
* `FunctionCollection_CreateAndAddFunction` can be used to initialize a new `FunctionCollection` and add a new `Function` to it in order to enable [function calling](#chatcompletions-functioncalling).
* `FunctionCollection_AddFunction` can be used to add a new `Function` to an existing `FunctionCollection`.

##### 4.3.1.3 Chat Completions (Advanced) {#chat-completions-advanced-technical}

For developers who want to configure the [ChatCompletionsRequest](#chatcompletionsrequest) object themselves and adjust its attributes according to their needs, Mendix recommends using the `ChatCompletions_CallAPI` microflow. The inputs and output are shown in the table below: 

**Input parameters**

| Name                     | Type                                              | Mandatory | Description                                                  |
| ------------------------ | ------------------------------------------------- | --------- | ------------------------------------------------------------ |
| `ChatCompletionsRequest` | [ChatCompletionsRequest](#chatcompletionsrequest) | mandatory | This is the request object with associated messages as specified by the Chat Completions API. |
| `Configuration`          | [Configuration](#configuration-entity)            | mandatory | This is an object that contains endpoint and API key.    |

**Return value**

| Name                      | Type                                                | Description                                                  |
| ------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| `ChatCompletionsResponse` | [ChatCompletionsResponse](#chatcompletionsresponse) | This is the response object containing the assistant message and other details about the request. |

This option can be used if the default values of the `ChatCompletionsRequest` are insufficient and must be changed to work for your specific use case. It is also useful if you are interested in other [ChatCompletionsResponse](#chatcompletionsresponse) values apart from the assistant response like usage metrics or multiple choices.

The following microflows may be used to construct and handle the required inputs:

* `ChatCompletionsRequest_Create` is used to create the request object.
* `ChatCompletionsMessages_Create` is used to create the wrapper object for the `ChatCompletionsMessageRequest` objects.
* `ChatCompletionsMessageRequest_Create` is used to create the message objects.
* `ChatCompletionsRequest_AddFunctionCalling` can be used to add a list of functions to be sent along with the `ChatCompletionsRequest` as tools in order to enable [function calling](#chatcompletions-functioncalling).

#### 4.3.2 Image Generations {#image-generations-technical} 

The image generations API from OpenAI accepts a JSON structure that consists of a number of parameters including the user prompt as input and generates a structure of one or many model-generated images as output. The image is returned as a URL or as a base64-encoded string. Depending on the model used, the API can return one or many model-generated images based on the input prompt plus other optional parameters. The exposed microflows in this connector are built to abstract away part of the complexity of the input and output structures and are meant to facilitate easier implementation in certain use cases. Currently, only the OpenAI API provides support for images (not Azure OpenAI).

##### 4.3.2.1 Image Generations (Single Image) {#image-generations-single-technical} 

Use the microflow `ImageGenerations_Execute` to execute a single image generations API call based on a prompt string input, where the response is mapped as an image onto the `OutputImage` object. The `OutputImage` instance must be a specialization of `GeneratedImage`. It is not required to provide the `Model`, `ENUM_Size`, `UserString`, `ENUM_Quality`, `ENUM_Style` and `ENUM_ResponseFormat_Image`  values. For the optional parameters, if left empty, the default value as specified by the OpenAI documentation will be assumed in the API.

**Input parameters**

| Name             | Type                                                    | Mandatory                     | Description                                                  |
| ---------------- | ------------------------------------------------------- | ----------------------------- | ------------------------------------------------------------ |
| `OutputImage`    | specialization of [GeneratedImage](#generatedimage)     | mandatory                     | This is the target instance in which the resulting image will be stored. It must be instantiated before calling this flow, and it must be a custom specialization of the GeneratedImage entity. |
| `Prompt`         | String                                                  | mandatory                     | This is the prompt that is used by the model to generate the image. |
| `Configuration`  | [Configuration](#configuration-entity)                  | mandatory                     | This is an object that contains endpoint and API key.        |
| `Model`          | String                                                  | only mandatory for **OpenAI** | This is the ID of the model to use. This is not considered for **Azure OpenAI** configurations. |
| `Size`           | [ENUM_Size](#enum-size)                                 | optional                      | This can be used to request a specific image size. The default value is `1024x1024`. |
| `Quality`        | [ENUM_Quality](#enum-quality)                           | optional                      | This is the quality of the image that will be generated. This parameter is only supported for dall-e-3. |
| `Style`          | [ENUM_Style](#enum-style)                               | mandatory                     | This is the style of the generated images. This parameter is only supported for dall-e-3. |
| `ResponseFormat` | [ENUM_ResponseFormat_Image](#enum-responseformat-image) | mandatory                     | This is the format in which the generated images are returned. Must be one of url or b64_json. Defaults to url. |
| `UserString`     | String                                                  | optional                      | This is a unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. |

**Return value**

| Name        | Type    | Description                                                  |
| ----------- | ------- | ------------------------------------------------------------ |
| `IsSuccess` | Boolean | The value is `true` if the image generations request was successful. The value is `false` if an error occurred or a validation failed. |

##### 4.3.2.2 Image Generations (advanced) {#image-generations-advanced-technical} 

For developers who want to configure the [ImageGenerationsRequest](#chatcompletionsrequest) object themselves and adjust its attributes according to their needs, Mendix recommends using the `ImageGenerations_CallAPI` microflow. The inputs and output are shown in the table below: 

**Input parameters**

| Name                      | Type                                               | Mandatory | Description                                               |
| ------------------------- | -------------------------------------------------- | --------- | --------------------------------------------------------- |
| `ImageGenerationsRequest` | [ImageGenerationsRequest](#chatcompletionsrequest) | mandatory | This is the request object for the Image Generations API. |
| `Configuration`           | [Configuration](#configuration-entity)             | mandatory | This is an object that contains endpoint and API key.     |

**Return value**

| Name                       | Type                                                  | Description                                                 |
| -------------------------- | ----------------------------------------------------- | ----------------------------------------------------------- |
| `ImageGenerationsResponse` | [ImageGenerationsResponse](#imagegenerationsresponse) | This is the response object containing the generated image. |

The microflow `ImageGenerationsRequest_Create` may be used here to create and handle the input request in a custom way.

#### 4.3.3 Embeddings

The embeddings API from OpenAI accepts a complex JSON structure that consists of a number of parameters plus one or more text strings as input and generates a structure of model-generated vector embeddings as output; per input string one vector is returned. Depending on the use case, there may be a need of generating an embedding for a single text at a time, whereas in the case of processing larger amount of data, bigger texts or data sets will be split up in discrete chunks, for which embeddings can be generated using batches of multiple input texts. The exposed microflows in this connector are built to abstract away the complex message structure and are meant to facilitate easier implementation in certain use cases. 

##### 4.3.3.1 Embeddings (single input) {#embeddings-single-technical} 

Use the microflow `Embeddings_Execute_SingleInput` to execute a call to the embeddings API for a single string input. The output will be the string representation of a vector embedding for the input. See [ENUM_EncodingFormat_Embeddings](#enum-encodingformat-embeddings) for information of what is supported in terms of vector encoding formats. The encoding format can be left empty: if no value is specified, the default value as specified in the [OpenAI documentation](https://platform.openai.com/docs/api-reference/chat/create) will be assumed by the API. The `Model` value is mandatory for OpenAI, but is ignored for Azure OpenAI type configurations where it is implicitly specified by the deployment already.

**Input parameters**

| Name             | Type                                                         | Mandatory                     | Description                                                  |
| ---------------- | ------------------------------------------------------------ | ----------------------------- | ------------------------------------------------------------ |
| `Input`          | String                                                       | mandatory                     | This is the input text to embed.                             |
| `Configuration`  | [Configuration](#configuration-entity)                       | mandatory                     | This is an object that contains endpoint and API key.        |
| `Model`          | String                                                       | only mandatory for **OpenAI** | This is the ID of the model to use. This is not considered for **Azure OpenAI** configurations. |
| `EncodingFormat` | [ENUM_EncodingFormat_Embeddings](#enum-encodingformat-embeddings) | optional                      | This can be used to specify the format in which the generated vectors must be returned. |

**Return value**

| Name              | Type   | Description                                                  |
| ----------------- | ------ | ------------------------------------------------------------ |
| `EmbeddingVector` | String | This is the string representation of a vector embedding for the input. |

##### 4.3.3.2 Embeddings (list input) {#embeddings-list-technical}

Use the microflow `Embeddings_Execute_ListInput` to execute an embeddings API call with a [DataBatch](#databatch) input with a list of text strings, attached to the batch in the form of [DataChunk](#datachunk) objects. The resulting embedding vectors returned by the model end up in the `EmbeddingVector` string attribute of the [DataChunks](#datachunk). See [ENUM_EncodingFormat_Embeddings](#enum-encodingformat-embeddings) for the information of what encoding formats are supported. The encoding format can be left empty: if no value is specified, the default value as specified in the [OpenAI documentation](https://platform.openai.com/docs/api-reference/chat/create) will be assumed by the API. The `Model` value is mandatory for OpenAI, but is ignored for Azure OpenAI type configurations where it is implicitly specified by the deployment already.

**Input parameters**

| Name             | Type                                                         | Mandatory                     | Description                                                  |
| ---------------- | ------------------------------------------------------------ | ----------------------------- | ------------------------------------------------------------ |
| `DataBatch`      | [DataBatch](#databatch)                                      | mandatory                     | This is a wrapper object for a list of `DataChunk` objects with Inputs for which an Embeddings vector should be generated. |
| `Configuration`  | [Configuration](#configuration-entity)                       | mandatory                     | This is an object that contains endpoint and API key.        |
| `Model`          | String                                                       | only mandatory for **OpenAI** | This is the ID of the model to use. This is not considered for **Azure OpenAI** configurations. |
| `EncodingFormat` | [ENUM_EncodingFormat_Embeddings](#enum-encodingformat-embeddings) | optional                      | This can be used to specify the format in which the generated vectors must be returned. |

**Return value**

| Name        | Type    | Description                                                  |
| ----------- | ------- | ------------------------------------------------------------ |
| `Success`   | Boolean | The value is `true` if the embeddings request was successful. The value is `false` if an error occurred or a validation failed. |

The `DataBatch` is a wrapper object for the list of text strings for which the embeddings are generated. You can use `DataBatch_Create` to create a new `Databatch`  and with `DataChunk_Create` new `DataChunk` objects will be added to the wrapper. The order is not relevant technically here; each `DataChunk` will be enriched with the corresponding embedding vector that was returned in the API call: the microflow `Embeddings_Execute_ListInput` already takes care of mapping the result onto the correct `DataChunk` entities and the microflow itself only returns a `Success` Boolean.

##### 4.3.3.3 Embeddings (Advanced) {#embeddings-advanced-technical}

For developers who want to configure the [EmbeddingsRequest](#embeddingsrequest) object themselves and adjust its attributes according to their needs, Mendix recommends using the `Embeddings_CallAPI` microflow. The inputs and output are shown in the table below: 

**Input parameters**

| Name                | Type                                    | Mandatory | Description                                           |
| ------------------- | --------------------------------------- | --------- | ----------------------------------------------------- |
| `EmbeddingsRequest` | [EmbeddingsRequest](#embeddingsrequest) | mandatory | This is the request object for the Embeddings API.    |
| `Configuration`     | [Configuration](#configuration-entity)  | mandatory | This is an object that contains endpoint and API key. |

**Return value**

| Name                 | Type                                      | Description                                                  |
| -------------------- | ----------------------------------------- | ------------------------------------------------------------ |
| `EmbeddingsResponse` | [EmbeddingsResponse](#embeddingsresponse) | This is the response object containing the generated embedding vectors. |

This option can be used if the default values and behavior of the `EmbeddingsRequest` are insufficient and must be changed to work for your specific use case. It is also useful if you are interested in other [EmbeddingsResponse](#embeddingsresponse) values apart from the vector embeddings, like usage metrics. 
The following flows may be used in order to construct and handle the required inputs: `EmbeddingsRequest_Create` and `EmbeddingsInput_Create`.

## 5 Showcase Application {#showcase-application}

For more inspiration or guidance on how to use those microflows in your logic, Mendix highly recommends downloading the [showcase app](https://marketplace.mendix.com/link/component/220475) from the Marketplace that displays a variety of example use cases.

{{% alert color="info" %}}
For more information on how to set up a vector database for retrieval augmented generation (RAG),  see [RAG Example Implementation in the OpenAI Showcase Application](/appstore/modules/openai-connector/rag-example-implementation/).
{{% /alert %}}

## 6 Troubleshooting {#troubleshooting}

### 6.1 Outdated JDK Version Causing Errors while Calling the Embeddings API {#outdated-jdk-version}

The Java Development Kit (JDK) is a framework needed by Mendix Studio Pro to deploy and run applications. For more information, see [Studio Pro System Requirements](/refguide/system-requirements/). Usually, the right JDK version is installed during the installation of Studio Pro, but in some cases it still may be outdated causing exceptions when calling the Embeddings API or other REST-based services with large data volumes.

We have seen the following two exceptions when using JDK version `jdk-11.0.3.7-hotspot`:
`java.net.SocketException - Connection reset` or
`javax.net.ssl.SSLException - Received fatal alert: record_overflow`.

Follow these steps to check your JDK version and update if necessary:

1. Check your JDK version: In Studio Pro Go to **Edit** -> **Preferences** -> **Deployment**-> **JDK directory**. If the path points to `jdk-11.0.3.7-hotspot`, you need to update the JDK by following the next steps.
2. Go to [Eclipse Temurin JDK 11](https://adoptium.net/en-GB/temurin/releases/?variant=openjdk11&os=windows&package=jdk) and download the `.msi` file of the latest release of **JDK 11**.
3. Open the downloaded file and follow the installation steps. Remember the installation path. Usually this should be something like `C:/Program Files/Eclipse Adoptium/jdk-11.0.22.7-hotspot`.
4. After the installation has finished, you might be asked to restart your computer.
5. Open Studio Pro and go to **Edit** -> **Preferences** -> **Deployment** -> **JDK directory**. Click on **Browse** and select the folder with the new JDK version you just installed. This should be the folder containing the *bin* folder. Save your settings by clicking **OK**.
6. Run the project and execute the action that threw the above mentioned exception earlier.
    1. You might get an error saying `FAILURE: Build failed with an exception. The supplied javaHome seems to be invalid. I cannot find the java executable.`. Verify that you have selected the right JDK directory containing the updated JDK version. You may also need to updated Gradle. For this, go to **Edit** -> **Preferences** -> **Deployment** -> **Gradle directory**. Click **Browse** and select a newer Gradle version from the Mendix folder. In this case we replaced `grade-7.6` with `gradle-7.6.3`. Save your settings by clicking **OK**.
    2. Rerun the project.

### 6.2 Chat Completions with Vision and JSON mode (Azure OpenAI)

At this moment, Azure OpenAI does not support the use of JSON mode and function calling in combination with image (vision) input and will return a `400 - model error`. Make sure the optional input parameters `ResponseFormat` and `FunctionColletion` are set to `empty` for all chat completions operations if you want to use vision with Azure OpenAI.

### 6.3 Chat Completions with Vision Response is Cut Off (Azure OpenAI)

When you use Azure OpenAI, it is recommended to set the optional `MaxTokens` input parameter so that the response will not be cut off. See [Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/gpt-with-vision?tabs=rest%2Csystem-assigned%2Cresource#call-the-chat-completion-apis) for more details.

## 7 Read More {#read-more}

* [Prompt Engineering – OpenAI Documentation](https://platform.openai.com/docs/guides/prompt-engineering)
* [Introduction to Prompt Engineering – Microsoft Azure Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/prompt-engineering)
* [Prompt Engineering Techniques – Microsoft Azure Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/advanced-prompt-engineering?pivots=programming-language-chat-completions)
* [ChatGPT Prompt Engineering for Developers - DeepLearning.AI](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers)
* [Function Calling - OpenAI Documentation](https://platform.openai.com/docs/guides/function-calling)
* [Vision - OpenAI Documentation](https://platform.openai.com/docs/guides/vision)
* [Vision - Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/gpt-with-vision)
