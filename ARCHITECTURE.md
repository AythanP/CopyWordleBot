# My Techdle feature

This diagram shows how my `/techdle` and `/guess` commands use the game code and saved game file.

```mermaid
flowchart TD
    A[Player runs /techdle] --> B[Bot picks a tech word different from the last one and starts six tries]
    B --> C[Save game under player's Discord ID]
    D[Player runs /guess word] --> E[Load that player's saved game]
    C --> E
    E --> F[For a valid guess, score it and save the update]
    F --> G[Send private colors and game result]
```

Each player has one current game. Starting `/techdle` again replaces that player's game. Guesses must be five letters; any five-letter guess is scored, without checking a word list. Invalid guesses use no attempt.

**Code:** `src/events/interactionCreate.js` handles commands and replies; `src/game/` contains the rules and feedback; `src/game/store.js` saves games; and `src/game/words.js` provides tech answers.

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
    I((Register the slash commands))
    J[Discord.js]
    K[Console/Terminal]

    A-->|API-compatible JSON data for slash commands|B
    B-->|Builder class|C
    C-->|/techdle and /guess slash command definitions|D
    D-->|Array of JSON commands returned by the techdleCommands function|F
    A-->|HTTP client used to communicate with Discord's API|F
    A-->|Collection of API endpoint/URL builders from Discord|F
    E-->|DiscordBot Token, user ID, server ID|F
    F-->|Discord bot token, user ID, server ID|G
    F-->|Array of JSON commands returned by the techdleCommands function|I
    I-->|Discord API endpoint for each command|J
    I-->|HTTP request for each command|J
    G-->|Validation result|K
    J-->|Command registration result|K
```
