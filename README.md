# Switchboard

63 AI tools in one static page, plus a photo generator, a side-by-side AI comparison, saved history, and a builder for your own tools. Everything runs in your browser on whichever AI you choose: Claude, OpenAI, Gemini, Mistral, Groq, DeepSeek, xAI, OpenRouter, Together, Fireworks, Cerebras, Perplexity, Ollama, LM Studio, or any endpoint URL you add.

There is no build step and no server.

## Put it online with GitHub Pages

1. Create a new public repository on GitHub.
2. Upload every file from this folder to the repository root (`index.html`, `manifest.webmanifest`, `sw.js`, the two icons, `.nojekyll`).
3. Open **Settings → Pages**. Under **Build and deployment** choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
4. After a minute your site is live at `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

## Features

- **63 tools:** chat partners, writing, creative, code, learning, life and play. Each has "Try an example", an editable instructions box, and its own AI picker.
- **Any AI:** add keys per provider, fetch each key's model list, or add custom endpoint URLs. Pick the AI at the top, or per tool.
- **Compare AIs:** one prompt to several providers at once, with timing.
- **Photo generator:** real images from `gpt-image-1`, DALL·E, or any OpenAI-compatible image endpoint, plus a prompt improver.
- **Make your own AI:** build a one-shot or chat tool with your own instructions. Export and import tools as JSON.
- **History and memory:** chats and results are saved in your browser, searchable, and restored after a reload. Export everything as Markdown or a JSON backup.
- **Attachments:** add text or code files to any chat or form, and images in chat (with a provider that can see images).
- **Voice:** dictate with the microphone, and have answers read aloud.
- **Chat controls:** copy, retry, read aloud, export chat, copy code blocks, tables rendered properly.
- **Preferences:** an "about you" note added to every AI's instructions, plus a creativity slider.
- **Command palette:** press Ctrl+K (or Cmd+K) to jump anywhere.
- **Installable:** works as an app on phones and desktops, and opens offline (the AI still needs the internet).

## No key? It still works

If you haven't added any API key, Switchboard automatically uses a **free shared AI** (Pollinations), so every tool and the photo generator work straight away. It needs no account. It is slower and less capable than a paid model, it can be busy, and your prompts are sent to that third-party service, so don't put private information in. The home page shows a banner while you're on it.

For better results, open **Add AI keys → Get a free key**. It lists providers with free tiers (Groq, Google Gemini, OpenRouter, Cerebras, Mistral, or Ollama on your own computer) with a link to get a key and a **Set up** button. Free tiers and their limits change, so check each site. As soon as you add any key, the free shared AI is switched off unless you tick it under its own entry.

### Why there is no key built into the site

Anything in `index.html` is public. A key placed in the file would be copied and used up by strangers within hours, and the provider would usually cancel it. That is why the keyless free service plus "bring your own free key" is used instead.

## Your keys and data

Click **Add AI keys** (top right), open a provider, paste its key, and press **Fetch models** to pick a model. Model names change often, so the defaults may be out of date.

Keys, history, chats and custom tools are saved only in your browser (localStorage) and keys are sent only to the provider's URL. Anyone who uses your site adds their own keys. Never put a key inside `index.html` or commit one to the repository, because anyone could read it and spend your credit. Use **Your data → Export backup** before clearing browser data.

## Notes

- **Browser access (CORS).** Calls go straight from the browser to each provider. Most allow this, but some may block it. If one fails with "couldn't be reached", use **OpenRouter** (one key, many models) or your own proxy URL.
- **Local models.** For Ollama, allow your site's address, for example `OLLAMA_ORIGINS="https://YOUR-USERNAME.github.io" ollama serve`, then tick "Use Ollama" in its row.
- **Photos** need an image model your key can use. They are not saved after you close the page, so download the ones you like.
- **Costs.** Each provider bills your own account. Compare AIs sends your prompt to every provider you tick.

## Add or change tools in code

Edit the `TOOLS` array in `index.html`:

```js
T("haiku","🌸","Haiku maker","create","Three lines on any subject.",{
  f:[t("about","Subject","Autumn rain")],
  tpl:"Write 3 original haiku about: {about}"
})
```

- `f` lists the form fields: `t` is a text box, `a` a large text area, `s` a dropdown.
- `tpl` is the prompt; `{about}` inserts the field with that key.
- `sys` sets the system prompt. Add `k:"chat"` for a chat tool, `k:"svg"` for vector art, `k:"html"` for live web pages, or `k:"cards"` for flashcards.

To add a built-in provider, add a line to the `PROV` list (any OpenAI-compatible API works with `base` and `model`).
