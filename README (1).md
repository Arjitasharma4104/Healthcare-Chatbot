# DiaBuddy — Diabetes AI Health Assistant

DiaBuddy is an AI-powered diabetes health chatbot that gives personalized guidance on diet, exercise, blood sugar management, and mental health. Users sign up with their health profile (diabetes type + HbA1c score) and get tailored advice from an AI assistant that actually knows their condition.

**Link to project:** https://YOUR-USERNAME.github.io/diabuddy/diabuddy.html


## How It's Made:

**Tech used:** HTML, CSS, Vanilla JavaScript, Anthropic Claude API

I built this as a single-file web app — no frameworks, no build tools, just clean HTML/CSS/JS that runs straight in the browser. The app has two main screens: a signup/login page where users enter their name, phone, email, diabetes type, and HbA1c score, and a chat interface modelled after a WhatsApp-style messenger.

The chat is powered by the Anthropic Claude API. Every message includes the user's health profile injected into the system prompt, so the AI gives advice specific to that person's diabetes type and HbA1c level — not just generic health tips. User accounts and sessions are stored in localStorage so users can log back in without losing their profile.

The UI features a teal gradient header, animated typing indicators, quick-tap chip buttons for common questions, and a live HbA1c badge that color-codes as Normal, Prediabetes, or Diabetes as the user types their score.



## Optimizations

After the initial build I noticed the chat history was being sent in full on every API request, which would get expensive for long conversations. I kept this in as a feature (it gives the AI memory of the conversation) but in a production version I would cap history at the last 10 messages to keep token usage efficient.

I also considered using a backend proxy to hide the API key, which would be the right approach for a real deployment. For this demo the key is added directly to the fetch headers — something I'd refactor before going to production by adding a simple Node/Express server as a middleware layer.

The HbA1c score badge updates live on input using a simple threshold check, which gives instant feedback without any extra API calls.


## Lessons Learned:

Building DiaBuddy taught me how powerful it is to inject user context into an AI system prompt. The difference between a generic chatbot and one that says "Given your Type 2 diabetes and HbA1c of 8.2%, here's what I'd suggest..." is enormous — and it's just a few lines of string interpolation. That *wow, this actually feels personal* moment was a big one.

I also learned to respect the single-responsibility principle even in a single-file project. Keeping auth logic, chat logic, and UI rendering in clearly separated function groups made debugging much easier than if I'd written it as one long script.

Handling async API calls gracefully — showing a typing indicator, disabling the send button, catching errors cleanly — turned out to be just as important as the AI integration itself. Good UX around loading states is what makes an app feel polished vs. broken.
