# Bazar: a party game where one of the players is an AI

A pass-the-phone party game in the spirit of Quiplash, built for **AI Cup 2026** as the first game of *vibe.games*, a feed of AI mini-games.

One phone, a group of friends, and an impostor. Each round everyone answers the same sharp prompt, and the AI slips in an answer of its own. Then you vote for the funniest answer and try to guess who wrote what, including which one came from the machine.

## How a round goes

1. **Lobby:** add the players at the table.
2. **Prompt:** Claude writes a fresh prompt in Russian with a bit of English and Kazakh, about school, parents, Almaty, pop culture and the absurd.
3. **Answers:** the phone goes around, and everyone types an answer the others can't see.
4. **The impostor:** the AI reads every real answer and writes its own fake, mirroring the group's length, language, spelling and vibe so it blends in.
5. **Vote:** the phone goes around again, and everyone picks a favorite. You can't vote for yourself.
6. **Attribution:** guess the author of each answer, +25 points for every hit, and the most for spotting the AI.
7. **Reveal:** who wrote what, scores, and a short sarcastic verdict from an AI host.

## The AI has three jobs

| Role | What it does |
|---|---|
| Writer | generates the round's prompt |
| Impostor | writes a fake answer that copies how *this* group writes |
| Host | gives a two-sentence roast of the round's results, 180 characters max |

All three run through one serverless function (`netlify/functions/quiplash.js`) on the Anthropic API.

## Stack

React 19, TypeScript, Vite, Tailwind, Zustand for the game state machine (`lobby → intro → answer → wait_ai → vote → attribute → reveal → final`), and a serverless function for the AI calls. The game is built for phones first, including fixes for iOS Safari quirks.

## Run it

```bash
npm install
ANTHROPIC_API_KEY=... npx netlify dev
```
