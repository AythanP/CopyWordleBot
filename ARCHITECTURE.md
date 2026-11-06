# Techdle Diagram

This diagram shows how our Techdle bot uses `/techdle` and `/guess` commands to saved game files.

# Aythan - Data Flow
This diagram shows the dataflows between Discord's API and our bot.

```mermaid
flowchart TD
    A[Discord.js]
    B[techdle.js]
    C((Build commands))
    D((Convert to JSON))
    E[.env file]
    F[registerTechdle.js]
    G((Validate .env variables))
    H((Register the slash commands))
    I[Discord.js]
    J[Console/Terminal]

    A-->|API-compatible JSON data for slash commands|B
    B-->|Builder class|C
    C-->|/techdle and /guess slash command definitions|D
    D-->|Array of JSON commands returned by the techdleCommands function|F
    A-->|HTTP client used to communicate with Discord's API|F
    A-->|Collection of API endpoint/URL builders from Discord|F
    E-->|DiscordBot Token, user ID, server ID|F
    F-->|Discord bot token, user ID, server ID|G
    F-->|Array of JSON commands returned by the techdleCommands function|H
    H-->|Discord API endpoint for each command|I
    H-->|HTTP request for each command|I
    G-->|Validation result|J
    I-->|Command registration result|J
```
# Anthony - Network Diagram

# Mario - Control Flow

# Sida - Class Diagram

# Abhi - Use Case Diagram

Each player has one current game. Starting `/techdle` again replaces that player's game. Guesses must be five letters and any five-letter guess is scored without checking a word list. Invalid guesses use no attempts.

**Code:** `src/events/interactionCreate.js` handles commands and replies; `src/game/` contains the rules and feedback; `src/game/store.js` saves games; and `src/game/words.js` provides tech answers.
