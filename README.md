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

## Issues Faced during Development

1.	Rasa would not detect certain numbers in a statement.
      1. With the default pipeline, Rasa could not detect phone number at times.
      2. However, it detected account number and amount correctly.
      2. Hence, I fiddled a little with the pipeline and switched to *RegexEntityExtractor*. But this time, it detected numbers but did not correctly identify them as entities. For example, *account number* gets wrongly classified as *phone number*.
      2. As a workaround for this, I changed regex for *phone*, *account*, and *amount* (Initially there was no regex, so I gave some examples to Rasa to identify correct slots) and replaced *RegexEntityExtractor* with *RegexFeaturizer*.
      2. It works now, although with some uncertainties. However, after a little digging around in the Rasa forums, they said the inconsistencies in training is common.

2.	Sometimes slots are forgotten.
      1. The fault lied in the *MemoizationPolicy*. After chaning the history to 7, it works now.
      2. For *TEDPolicy*, the epochs to train have been increased to 200.

## Working of the Code

I have tried my best to explain most of the terminologies and working of the various parts of the code. This can be found in the `Documentation.pdf` file in the repository.

## References

- The [RasaNLU Documenation](https://rasa.com/docs/rasa/) - A go-to source for understanding the nitty-gritty of open source Rasa
- The [Rasa Community Forum](https://forum.rasa.com/) - Cleared my doubts on many occasions, especially for the regional language support.
