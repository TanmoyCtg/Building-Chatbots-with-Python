# Building Chatbots with Python
My first chatbot! After gaining a bit of historical context, I'll set up a basic structure for receiving text and responding to users, and then learn how to add the basic elements of personality. I'll then build rule-based systems for parsing text.

# EchoBot
Hello, World! 
I'll begin by writing two functions to build the simplest bot possible: EchoBot. EchoBot just responds by replying with the same message it receives.
I'll define a function that responds to a user's message. In the next exercise, I'll complete EchoBot by writing a function to send a message to the bot.

## Instructions
* Write a function called respond() with a single parameter message which returns the bot's response. To do this, concatenate the strings "I can hear you! You said: " and message. 
* Store the concatenated strings in bot_message, and return this result.

```python

bot_template = "BOT : {0}"
user_template = "USER : {0}"

# Define a function that responds to a user's message: respond
def respond(message):
    # Concatenate the user's message to the end of a standard bot respone
    bot_message = "I can hear you! You said: " + message 
    # Return the result
    return bot_message
```
# EchoBot II
Having written your respond() function, I'll now define a function called send_message() with a single parameter message which logs the message and the bot's response.

```python

# Define a function that sends a message to the bot: send_message
def send_message(message):
    # Print user_template including the user_message
    print(user_template.format(message))
    # Get the bot's response to the message
    response = respond(message)
    # Print the bot template including the bot's response.
    print(bot_template.format(response))

# Send a message to the bot
send_message("hello")
```
# Chitchat
Now I am creating a bot which can answer simple questions such as "What's your name?" and "What's today's weather?"
I'll use a dictionary with these questions as keys, and the correct responses as values. 
This means the bot will only respond correctly if the message matches exactly, which is a big limitation. 
The send_message function has already been defined , as well as the bot_template and user_template variables.

## Instructions
* Define a respond() function which takes in a message argument, checks if the message has a pre-defined response, and returns the response in the responses dictionary if there is a match, or the "default" message otherwise.

Well Done! Your bot is now able to answer some simple questions. Hit 'Run Code' and call send_message() in the IPython Shell with the following questions: 
**"what's today's weather?"**
**"what's your name?"**
**"what's your favorite color?"**

Hit 'Submit Answer' when you are done.

```python

# Define variables
name = "Greg"
weather = "cloudy"

# Define a dictionary with the predefined responses
responses = {
  "what's your name?": "my name is {0}".format(name),
  "what's today's weather?": "the weather is {0}".format(weather),
  "default": "default message"
}

# Return the matching response if there is one, default otherwise
def respond(message):
    # Check if the message is in the responses
    if message in responses:
        # Return the matching message
        bot_message = responses[message]
    else:
        # Return the "default" message
        bot_message = responses["default"]
    return bot_message
```
# Adding variety
It can get a little boring hearing the same old answers over and over. I'll add some variation. If you ask your bot how it's feeling, it may equally well respond with "oh I'm great!" as with "I'm very sad today".

Here, I'll use the random module - specifically random.choice(ls) - which randomly selects an element from a list ls.
A dictionary called responses, which maps each message to a list of possible responses, has been defined for you.

## Instructions
* Import the random module.
* Use random.choice() in the respond() function to choose one of the matching responses.

```python

# Import the random module
import random

name = "Greg"
weather = "cloudy"

# Define a dictionary containing a list of responses for each message
responses = {
  "what's your name?": [
      "my name is {0}".format(name),
      "they call me {0}".format(name),
      "I go by {0}".format(name)
   ],
  "what's today's weather?": [
      "the weather is {0}".format(weather),
      "it's {0} today".format(weather)
    ],
  "default": ["default message"]
}

# Use random.choice() to choose a matching response
def respond(message):
    # Check if the message is in the responses
    if message in responses:
        # Return a random matching response
        bot_message = random.choice(responses[message])
    else:
        # Return a random "default" response
        bot_message = random.choice(responses["default"])
    return bot_message
   
```

# JOY I: asking questions
Asking questions is a great way to create an engaging conversation. Here, I'll create the very first hint of ELIZA's famous personality, by responding to statements with a question and responding to questions with answers.
A dictionary of responses with "question" and "statement" as keys, and lists of appropriate responses as values has already been defined for you. Explore this in the Shell with responses.keys() and responses["question"]

## Instructions

* Define a respond() function which takes in message as an argument, and uses the string's .endswith() method to check if a message ends with a question mark.

* If the message does end with a question mark, choose a random "question" from the responses dictionary. Else, choose a random "statement" from the responses 

* Send the bot multiple messages with and without a question mark - a few have been provided for you. If you want to experiment further in the Shell, be sure to first hit 'Run Code'. 


```python

import random

def respond(message):
    # Check for a question mark
    if message.endswith("?"):
        # Return a random question
        return random.choice(responses["question"])
    # Return a random statement
    return random.choice(responses["statement"])


# Send messages ending in a question mark
send_message("what's today's weather?")
send_message("what's today's weather?")

# Send messages which don't end with a question mark
send_message("I love building chatbots")
send_message("I love building chatbots")
```
# JOY II: Extracting key phrases
The really clever thing about ELIZA is the way the program appears to understand what you told it, by occasionally including phrases uttered by the user in its responses.
I will match messages against some common patterns and extract phrases using re.search(). A dictionary called rules has already been defined, which matches the following patterns:
"do you think (.*)"
"do you remember (.*)"
"I want (.*)"
"if (.*)"

```python

# Define match_rule()
def match_rule(rules, message):
    response, phrase = "default", None
    
    # Iterate over the rules dictionary
    for pattern, responses  in rules.items() :
        # Create a match object
        match = re.search(pattern,message)
        if match is not None:
            # Choose a random response
            response = random.choice(responses)
            if '{0}' in response:
                phrase = match.group(1)
    # Return the response and phrase
    return response, phrase

# Test match_rule
print(match_rule(rules, "do you remember your last birthday"))
```




















































