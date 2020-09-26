# Notes about chatterbots
Chatbots can be broadly classified into two different types;

Rule-Based Chatbots
===================

The very first bots to see the light of day, rule based chatbots relied on pattern-matching methodologies to ‘guess’ appropriate responses from an existing database. These bots started with the release of ELIZA in 1966 and continued till around 2001 with the release of SmarterChild developed by ActiveBuddy.

The simplest rule-based chatbots have one-to-one tables of inputs and their responses. These bots are extremely limited and can only respond to queries if they are an exact match with the inputs defined in their database. This means the conversation can only follow a number predefined flows. In a lot of cases, the chatbot doesn’t even allow users to type in queries, relying, instead on, preset inputs that the bot understands.

This doesn’t necessarily limit their use though. Rule-based Chatbots are widely used in modern businesses for customer support tasks. A Customer Support Chatbot has a very limited job description. A customer support chatbot for a bank, for example, would need to answer some operational queries about the bank (timings, branch locations) and complete some basic tasks (authenticate user’s, block stolen credit cards, activate new credit cards, register complaints).

In almost all of these cases, the conversation would follow a pattern. The flow of conversation, once defined, would stay mostly the same for a majority of the users. The small number of customers who need more specialized support could be forwarded to a human agent.

A lot of modern customer-facing chatbots are AI-based Chatbots that use Retrieval based Models (which we’ll be discussing below). They are primarily rule-based but employ some form of Artificial Intelligence (AI) to help them understand the flow of human conversations.

AI-Based Chatbots
=================

These are a relatively newer class of chatbots, having come out after the proliferation of artificial intelligence in recent years. These bots (like Microsoft’s Tay) learn by being trained on conversational datasets, instead of having hard-coded rules like their rule-based kin.

AI based chatbots are based on complex machine learning models that enable them to self-learn. These types of chatbots can be broadly classified into two main types depending on the types of models they use;

1. Retrieval based Models: 
As their name suggests, Chatbots using retrieval-based models are provided with a database of answers and are trained to retrieve the most relevant answer based on the input question. These bots already have a provided list of responses and are trained to rank each response based on the input/question. They cannot generate their own answers but with an extensive database of answers and proper training, they can be very productive and useful.
Usually easier to develop and customize, retrieval based chatbots are mostly used in customer support and feedback applications where the conversation is generally limited to a topic (either a product, a service or an entity).

2. Generative Models:
Generative models, unlike Retrieval based models, can generate their own responses by analyzing the input word by word to understand the query. These models are more ‘human’ during their interactions but at the same time also more prone to errors as they need to build sentence responses themselves.
Chatbots based on Generative Models are quite complex to build and are usually overkill for customer-facing applications. They are mostly used in applications where conversations are expected to be general/not limited to a specific topic. Take Google Assistant as an example. The Assistant is an always listening chatbot that can answer questions, tell jokes and carry out very ‘human’ conversations. The one thing it can’t do? Provide customer support for Google products.

Modern Chatbots: Where are they used?

1. Customer Services
Use of chatbots has been growing exponentially in the Customer Services industry. The chatbot market is projected to grow from $2.6 billion in 2019 to $9.4 billion by 2024. This really isn’t surprising when you look at the immense benefits chatbots bring to businesses. According to a study by IBM, chatbots can reduce customer services cost by up to 30%. Couple that with customer’s being open to interacting with bots for support and purchases, it’s a win-win scenario for both parties involved.
In the customer support industry, chatbots are mostly used to automate redundant queries that would normally be handled by a human agent. Businesses are also starting to use them in automating order-booking applications. The most successful example being Pizza Hut’s automated ordering platform.

2. Healthcare
Despite not being a substitute for healthcare professionals, chatbots are gaining popularity in the healthcare industry. They are mostly used as self-care assistants, helping patients manage their medications and help them track and monitor their fitness.

3. Financial Assistants
Financial chatbots usually come bundled with apps from leading banks. Once linked to your bank account, they can extend the functionality of the app by providing you with a conversational (text or voice) interface to your bank. Besides these, there are quite a few financial assistant chatbots available. These are able to track your expenses, budget your resources and help you manage your finances. Charlie is a very good example of a financial assistant. The chatbot is designed to help you budget your expenses and track your finances so that you end up saving more.













## Build a Chatterbot chatbot
Chatterbot is a python-based library that makes it easy to build AI-based chatbots. The library uses machine learning to learn from conversation datasets and generate responses to user inputs. The library allows developers to train their chatbot instance with pre-provided language datasets as well as build their own datasets.

A newly initialized Chatterbot instance starts off with no knowledge of how to communicate. To allow it to properly respond to user inputs, the instance needs to be trained to understand how conversations flow. Since Chatterbot relies on machine learning at its backend, it can very easily be taught conversations by providing it with datasets of conversations.

Chatterbot’s training process works by loading example conversations from provided datasets into its database. The bot uses the information to build a knowledge graph of known input statements and their probable responses. This graph is constantly improved and upgraded as the chatbot is used.

The Chatterbot Corpus is an open-source user-built project that contains conversational datasets on a variety of topics in 22 languages. These datasets are perfect for training a chatbot on the nuances of languages – such as all the different ways a user could greet the bot. This means that developers can jump right to training the chatbot on their custom data without having to spend time teaching common greetings.

Chatterbot has built-in functions to download and use datasets from the Chatterbot Corpus for initial training.

Chatterbot uses Logic Adapters to determine the logic for how a response to a given input statement is selected.

A typical logic adapter designed to return a response to an input statement will use two main steps to do this. The first step involves searching the database for a known statement that matches or closely matches the input statement. Once a match is selected, the second step involves selecting a known response to the selected match. Frequently, there will be a number of existing statements that are responses to the known match. In such situations, the Logic Adapter will select a response randomly. If more than one Logic Adapter is used, the response with the highest cumulative confidence score from all Logic Adapters will be selected.

Chatterbot stores its knowledge graph and user conversation data in a SQLite database. Developers can interface with this database using Chatterbot’s Storage Adapters.

Storage Adapters allow developers to change the default database from SQLite to MongoDB or any other database supported by the SQLAlchemy ORM. Developers can also use these Adapters to add, remove, search and modify user statements and responses in the Knowledge Graph as well as create, modify and query other databases that Chatterbot might use.

n this tutorial, we will be using the Chatterbot Python library to build an AI-based Chatbot.

We will be following the steps below to build our chatbot

1. Importing Dependencies
2. Instantiating a ChatBot Instance
3. Training on Chatbot-Corpus Data
4. Training on Custom Data
5. Building a frontend

The first thing we’ll need to do is import the modules we’ll be using. The ChatBot module contains the fundamental Chatbot class that will be used to instantiate our chatbot object. The ListTrainer module allows us to train our chatbot on a custom list of statements that we will define. The ChatterBotCorpusTrainer module contains code to download and train our chatbot on datasets part of the ChatterBot Corpus Project.

A chatbot instance can be created by creating a ChatBot object. The ChatBot object needs to have a name of the chatbot and must reference any logic or storage adapters you might want to use.

In the case you don’t want your chatbot to learn from user inputs after it has been trained, you can set the read_only parameter to True.

Training your chatbot agent on data from the Chatterbot-Corpus project is relatively simple. To do that, you need to instantiate a ChatterBotCorpusTrainer object and call the train() method. The ChatterBotCorpusTrainer takes in the name of your ChatBot object as an argument. The train() method takes in the name of the dataset you want to use for training as an argument.

Detailed information about ChatterBot-Corpus Datasets is available on the project’s Github repository.

You can also train ChatterBot on custom conversations. This can be done by using the module’s ListTrainer class.

In this case, you will need to pass in a list of statements where the order of each statement is based on its placement in a given conversation. Each statement in the list as a possible response to it’s predecessor in the list.

The training can be undertaken by instantiating a ListTrainer object and calling the train() method. It is important to note that the train() method must be individually called for each list to be used.

Once the chatbot has been trained, it can be used by calling Chatterbot's get_response() method. The method takes a user string as an input and returns a response string.

The functionality of this bot can easily be increased by adding more training examples. You could, for example, add more lists of custom responses related to your application.

As we saw, building an AI-based chatbot is relatively easy compared to building and maintaining a Rule-based Chatbot. Despite this ease, chatbots such as this are very prone to mistakes and usually give robotic responses because of a lack of good training data.

A better way of building robust AI-based Chatbots is to use Conversational AI Tools offered by companies like Google and Amazon. These tools are based on complex machine learning models with AI that has been trained on millions of datasets. This makes them extremely intelligent and, in most cases, are almost indistinguishable from human operators.



## References
https://blog.datasciencedojo.com/building-an-ai-based-chatbot-in-python/

https://chatterbot.readthedocs.io/en/stable/

https://github.com/gunthercox/chatterbot-corpus/tree/master/chatterbot_corpus/data
