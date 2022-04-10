---
title: ""
excerpt_separator: "<!--more-->"
date: 2021-09-15T15:34:30-04:00
categories:
  - Draft
tags:
  - 
header:
  image: /assets/images/spider-man-analyzing-the-web.png
---

### What to expect:
- 

---

N Gram
Markov Chain (Chain Rule)
### Hidden Markov Chain (HMM)

we assume that every event/item in a sequence is associated with a state
every event/item are discrete and sequential.

in the context of nlp, some words belongs to an entity (a person, a location etc.), these are considered the **hidden states**. the word counts are observable (output sequence) but the entities are not (state sequence). we can conclude that the data is "partially observed", where states are not observed, items are observed.

for every current state, it applies the markov model to depend only on the previous state; for output sequence, once its state is confirmed, the output is determined by the state, not the previous observation. i.e. first, determine the state, and based on the state, determine the right word, then back the state sequence for the next state, and so on.

decoding: finding the most likely sequence of states
evaluation: finding the probability of a given sequence-> the output
training: estimating the model parameters based on data, in the context of nlp it is the count of words, or even labels for their states.

application- part of speech tagging, entity extraction, machine translation, time series analysis, speech recognition