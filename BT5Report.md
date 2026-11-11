# This is a group report for Bot Task 5. All group members should contribute to this file only.

# Aythan Pao
## Threat Model
### Introduction
This analysis will present a formal threat model for the techdle Discord bot, developed in Java. It will identify potential security threats using the STRIDE framework,
determine their likely impact, and present prevention or mitigation strategies, where possible and relevant to the current build. 
### Bot Basic Description
The techdle bot allows Discord users to play Wordle through slash commands. Figure 1 shows the basic data flows of the bot.

The following serves as a key/legend to the individual components for Figure 1:
- Discord User: Person interacting with the bot.
- Discord API: Handles communication between discord and the bot.
- interactionCreate.js: Handles the majority of the bot's decision making and validation.
- store.js: Handles the game state.
- feedback.js: Handles bot output to the user, including failure messages. 

Figure 1
<img width="1280" height="960" alt="CSS 360 Bot Task 5 Aythan Pao 2026" src="https://github.com/user-attachments/assets/4a397798-df52-4f58-a9f8-b93135c775e0" />
A trust boundary represents a point where information moves between components with different levels of trust. The boundary in Figure 1 shows that primary boundary 
is between the user and the bot. All user input is treated as untrusted and must be verified, and measures should be taken to prevent unauthorized access to the bot 
from the user. 
### STRIDE Threat Analysis
The following tables identify potential threats to the bot, describes them, ranks their risk and impact, and suggests mitigation strategies for each. 

**Spoofing:** The user pretends to be someone or something other than themselves.
| Threat | Description | Risk | Impact | Mitigation |
| ------------- | ------------- | ------------- | ------------- |
| User/bot spoofing | An attacker forges a user's ID or gains access to the bot's .env token, obscuring their real identify. | Negligible | Medium | Preliminary analysis suggests that both the bot and Discord's API have sufficient protections against spoofing attacks. Discord's API should handle all attempts at spoofing the user. Restricting access to the bot's token in the .env file through the use of .gitignore and avoidance in logging the token in variables and debug console sufficiently protect the bot and its permissions against becoming compromised or misused. |

**Tampering:** Application data, functionality, or game state is modified without appropriate authorization. 
| Threat | Description | Risk | Impact |
| ------------- | ------------- | ------------- | ------------- |
| Modification of persistent game state | An attacker with access to the bot's local JSON file could modify it to manipulate the current game state. This could result in changes to the user's answer, the number of allowed attempts, and win/loss conditions.  | Negligible | High |
| Modification of concurrent game states | Preliminary analysis suggests that in order for the identified threats to materialize, the bot's JSON file,  | Negligible | High |
| Modification of source code | Preliminary analysis suggests that in order for the identified threats to materialize, the bot's JSON file,  | Negligible | High |
### STRIDE Mitigation Strategies

## CI/CD Pipeline

## Reflection
