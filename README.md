# Rasa Chatbot in Tamil
This is a chatbot in Tamil language developed with the RasaNLU framework. This project was undertaken to understand the concepts of Natural Language Understanding and explore the possibilites of regional language support for customer support bots.

## Introduction

Many users struggle to recharge their mobile plans through their respective carrier’s online portals. The main reason is the difficulty in understanding English and the unfamiliarity with keywords that are used for the same. To explore a possible solution, I explored designing a bot that can assist users in Tamil. The bot is developed with *RasaNLU* framework.

The bot has the following functionalities:
- Recharge support for mobile plans
- Cancel last recharge
- Get a refund
- Get coverage for a particular zone (Certain carriers don't provide national mobile coverage)
- Standard Conversations like greeting, asking simple questions
All these questions can be asked in Tamil!

As I am only interested in the implementation of the dialogue flow and modelling the chatbot, I didn't focus on the backend system of the recharge portal. So, to simulate conditions where users face technical difficultes, I have added some randomness in the output. For example, a mobile recharge might be successful or unsuccessful which depends on a random True/False result.

If time persists, I might also add a working backend in the a future iteration 😄

### Issues Faced during Development

1.	Rasa would not detect certain numbers in a statement.
      1. With default pipeline, Rasa could not detect phone number at times.
      2. But it detected account number and amount correctly.
      2. So, I played a little bot with the pipeline and switched to *RegexEntityExtractor*. It was worse. It detected numbers but did not correctly identify them as correct entities. For example, an *account number* is wrongly slotted into *phone number*.
      2. So as an ultimate solution, I have changed regex for *phone*, *account*, and *amount* (Initially there was no regex, I just gave some examples for Rasa to identify correct slots itself) and replaced *RegexEntityExtractor* with *RegexFeaturizer*.
      2. It works now, however in forums they said the inconsistencies in training is common, and sometimes it might not work well.

2.	Sometimes slots are forgotten.
      a.	The culprit is the *MemoizationPolicy*. I changed history to 7 and now it works.
      b.	Also, for *TEDPolicy*, the epochs to train are increased to 200

Also, I have utilized most of Rasa’s core concepts such as *rules*, *actions*, *NLU* and *domain*. Some new things such as *SlotSet* took some time to work out, but eventually I got through it. I have added enough in-code comments to project as well.
