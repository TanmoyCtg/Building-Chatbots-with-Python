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































































