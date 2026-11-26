# Voxora — AI voice assistant for business

Voxora is a small, runnable web app with a business setup screen, AI-powered conversation grounded in the company's description, browser speech input, and spoken responses. It uses the browser's built-in Web Speech APIs for speech recognition and synthesis, and calls OpenAI from a Node.js server so the API key is never sent to the browser.

## Requirements

- Node.js 18 or newer (built-in `fetch` is used).
- An OpenAI API key with API access and billing enabled.
- A browser with JavaScript enabled. Speech recognition support varies by browser; text chat remains available if it is not supported. Microphone access generally requires `localhost` or HTTPS.

## Run locally

1. Copy `.env.example` to `.env` and set `OPENAI_API_KEY` to your own key. Do not commit `.env` or put the key in frontend code.
2. Start the server:

   ```sh
   npm start
   ```

3. Open <http://127.0.0.1:3000>.
4. Describe the company and select a voice. Ask a question by typing or pressing the microphone button.

The first screen is also served by `npm start`; opening `index.html` directly as a file will not connect to the AI endpoint.

## Configuration

`OPENAI_API_KEY` is required for AI replies. `OPENAI_MODEL` defaults to `gpt-4o-mini`. `HOST` and `PORT` default to `127.0.0.1` and `3000`. Check `GET /api/health` to see whether a key is configured; it does not expose the key.

Business configuration and chat history are kept in the user's browser local storage and are sent to the server only when a chat message is submitted. The server forwards the business description and recent conversation to the configured AI provider. Do not use real customer personal data in this prototype. The browser voice used for replies depends on voices installed on the user's device; exact gender selection is not guaranteed across operating systems.

## Production notes

This is a functional starter, not a production-ready phone system. It does not include telephony/SIP, authentication, multi-tenant accounts, persistent server-side company profiles, appointment booking, or a call-recording system. Before exposing it publicly, add user authentication, tenant isolation, rate limiting, HTTPS, privacy and retention controls, abuse monitoring, and a production-grade speech/telephony provider. Budget for AI API usage; browser microphone support and recognition quality vary by browser and language.
