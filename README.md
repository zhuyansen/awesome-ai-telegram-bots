# Awesome AI Telegram Bots

[中文](README.zh-CN.md)

Open-source **Telegram bots built on AI**: GPT, Claude and local-model assistants, remote control for Claude Code and Codex, bot frameworks and MCP servers, utility, learning and business bots. 260 repos, each one read and security-graded by [Agent Skills Hub (agentskillshub.top)](https://agentskillshub.top).

Live page with filters: **[https://agentskillshub.top/best/telegram-bot/](https://agentskillshub.top/best/telegram-bot/)** · refreshed every 8 hours

## Which one to run

We read the source of 20 of these bots: who each one serves, and what it can do on your machine. This is what we would pick; the [full audit](#tested) is below.

- 🥇 **To drive Claude Code from your phone: [ccgram](https://github.com/alexei-led/ccgram)**  
  One of two bots of 14 that both refuse to start without your Telegram ID and send Claude's permission prompts to you in Telegram, so a risky command still waits for your tap. The other is six-ddc/ccbot, which it grew out of; ccgram had commits this week, ccbot's last was in July.
- 🥈 **If your agent is OpenCode: [opencode-telegram-bot](https://github.com/grinev/opencode-telegram-bot)**  
  Locked to exactly one Telegram user ID and will not start without it. When OpenCode asks for permission it shows Allow and Reject buttons in the chat; how often it asks is your OpenCode config.
- 🥉 **If you only want an AI chat bot: [ChatGPT-Telegram-Workers](https://github.com/tbxark/ChatGPT-Telegram-Workers)**  
  The only popular chat bot here that denies by default: it answers the admin and the IDs you add, nobody else. It runs on Cloudflare Workers, so there is no server of yours to break into. Set TELEGRAM_SECRET_TOKEN as well.

**Do not run as shipped:** claudecode-telegram (no access check at all, Claude runs with permissions skipped, and the webhook listens on every interface); claude-telegram-relay (forget one variable and it starts anyway, serving anyone); claude-code-telegram (the most-starred one; with an empty allowlist it lets everyone in unless ENVIRONMENT=production).

Whichever you pick: 9 of the 14 agent bots run with permission prompts off, so the allowlist is the only lock. Whoever controls your Telegram account then has a shell on that machine. Turn on Telegram two-step verification, and run the bot as its own user or in a container.

*Ranked by what the bot does when no allowlist is set, then (for bots that drive a coding agent) by what stands between a message and a command, then GitHub stars. Read from the source at the commit on each evidence page; nothing was run.*


## What these bots look like

<table>
<tr>
<td align="center" valign="top" width="33%"><b>💬 AI assistants</b><br><sub>91 repos</sub><br><br><a href="https://github.com/tuuject/surowan"><img src="assets/previews/tuuject__surowan.jpg" width="260" alt="tuuject/surowan"></a><br><sub>AI chat assistants in Telegram: GPT, Claude, Gemini, local models.</sub><br><a href="#type-assistant"><b>View the list →</b></a></td>
<td align="center" valign="top" width="33%"><b>🛰 Agent remote control</b><br><sub>70 repos</sub><br><br><a href="https://github.com/HNF-FRN/Reel-watcher-telegram-Agent"><img src="assets/previews/HNF-FRN__Reel-watcher-telegram-Agent.gif" width="260" alt="HNF-FRN/Reel-watcher-telegram-Agent"></a><br><sub>Control Claude Code, Codex or a computer from your phone.</sub><br><a href="#type-remote"><b>View the list →</b></a></td>
<td align="center" valign="top" width="33%"><b>🧱 Frameworks & MCP</b><br><sub>33 repos</sub><br><br><a href="https://github.com/EvilFreelancer/tgfake"><img src="assets/previews/EvilFreelancer__tgfake.jpg" width="260" alt="EvilFreelancer/tgfake"></a><br><sub>Libraries, templates and MCP servers for building bots.</sub><br><a href="#type-framework"><b>View the list →</b></a></td>
</tr>
<tr>
<td align="center" valign="top" width="33%"><b>🧰 Utility bots</b><br><sub>33 repos</sub><br><br><sub>Downloads, files, translation, group management.</sub><br><a href="#type-utility"><b>View the list →</b></a></td>
<td align="center" valign="top" width="33%"><b>🎲 Fun & learning</b><br><sub>7 repos</sub><br><br><a href="https://github.com/turmyshevd/openclawgotchi"><img src="assets/previews/turmyshevd__openclawgotchi.gif" width="260" alt="turmyshevd/openclawgotchi"></a><br><sub>Games, quizzes, language practice and companions.</sub><br><a href="#type-fun"><b>View the list →</b></a></td>
<td align="center" valign="top" width="33%"><b>💼 Business</b><br><sub>26 repos</sub><br><br><sub>Support, sales, payments, trading and monitoring.</sub><br><a href="#type-business"><b>View the list →</b></a></td>
</tr>
</table>

## Contents

- [🧪 Tested end to end](#tested)
- [💬 AI assistants](#type-assistant) (91)
- [🛰 Agent remote control](#type-remote) (70)
- [🧱 Frameworks & MCP](#type-framework) (33)
- [🧰 Utility bots](#type-utility) (33)
- [🎲 Fun & learning](#type-fun) (7)
- [💼 Business](#type-business) (26)

## How a repo gets on the list

1. It is a Telegram bot, or a tool for building or running one; Telegram is its main interface.
2. It is software someone can install or run, not a list of links or a placeholder.
3. It has a README. Without one it cannot be graded.
4. At 50 stars or more it is listed on topic alone. Under 50 it must also clear a README quality bar (shows it working, one-command start, a concrete outcome, complete docs), and have 5 stars.

The questions are answered by a decision model reading each README, not by hand. A repo near a cut-off can land on either side; open an issue if one is misfiled.

<a id="tested"></a>
## 🧪 Source audit

On 2026-10-10 we read the source of 20 of these bots. A bot needs a BotFather token to run, so this is a reading, not a run: for each one, who it serves when you set no allowlist, and for bots that drive a coding agent, what stands between a Telegram message and a command on your machine. Every answer cites its file and line; every "serves anyone" was re-read by hand.

**What we found:** 10 of 14 agent bots serve nobody until you list your ID, but 9 of 14 run the agent with permission prompts off, so that list is the only lock. 4 of 6 chat bots answer anyone by default. No repository had a real bot token committed.

### Bots that drive a coding agent on your machine (14)

| # | Bot | ★ | With no allowlist set | Before the agent acts | Setting to check |  |
|---|---|---|---|---|---|---|
| 1 | [opencode-telegram-bot](https://github.com/grinev/opencode-telegram-bot) | 1,234 | Serves nobody | Agent's own prompts sent to Telegram | TELEGRAM_ALLOWED_USER_ID (required) | [evidence](https://agentskillshub.top/best-runs/telegram/grinev__opencode-telegram-bot.html) |
| 2 | [ccgram](https://github.com/alexei-led/ccgram) | 277 | Serves nobody | Permission prompts sent to Telegram | ALLOWED_USERS (required) | [evidence](https://agentskillshub.top/best-runs/telegram/alexei-led__ccgram.html) |
| 3 | [ccbot](https://github.com/six-ddc/ccbot) | 276 | Serves nobody | Permission prompts sent to Telegram | ALLOWED_USERS (required) | [evidence](https://agentskillshub.top/best-runs/telegram/six-ddc__ccbot.html) |
| 4 | [takopi](https://github.com/banteg/takopi) | 1,049 | Serves nobody | Runs with permission prompts off | chat_id (required); allowed_user_ids for groups | [evidence](https://agentskillshub.top/best-runs/telegram/banteg__takopi.html) |
| 5 | [flock](https://github.com/duckbugio/flock) | 502 | Serves nobody | Runs with permission prompts off | ALLOWED_USERS | [evidence](https://agentskillshub.top/best-runs/telegram/duckbugio__flock.html) |
| 6 | [ductor](https://github.com/PleasePrompto/ductor) | 457 | Serves nobody | Runs with permission prompts off | allowed_user_ids (required) | [evidence](https://agentskillshub.top/best-runs/telegram/PleasePrompto__ductor.html) |
| 7 | [claude-telegram-bot](https://github.com/linuz90/claude-telegram-bot) | 448 | Serves nobody | Runs with permission prompts off | TELEGRAM_ALLOWED_USERS (required) | [evidence](https://agentskillshub.top/best-runs/telegram/linuz90__claude-telegram-bot.html) |
| 8 | [agent-second-brain](https://github.com/smixs/agent-second-brain) | 391 | Serves nobody | Runs with permission prompts off | ALLOWED_USER_IDS | [evidence](https://agentskillshub.top/best-runs/telegram/smixs__agent-second-brain.html) |
| 9 | [antigravity-telegram-suite](https://github.com/emreturkmencom/antigravity-telegram-suite) | 172 | Serves nobody | Runs with permission prompts off | ALLOWED_CHAT_ID (required) | [evidence](https://agentskillshub.top/best-runs/telegram/emreturkmencom__antigravity-telegram-suite.html) |
| 10 | [claudegram](https://github.com/NachoSEO/claudegram) | 153 | Serves nobody | Runs with permission prompts off | ALLOWED_USER_IDS (required) | [evidence](https://agentskillshub.top/best-runs/telegram/NachoSEO__claudegram.html) |
| 11 | [claudeclaw](https://github.com/earlyaidopters/claudeclaw) | 173 | Side commands open to anyone | Runs with permission prompts off | ALLOWED_CHAT_ID | [evidence](https://agentskillshub.top/best-runs/telegram/earlyaidopters__claudeclaw.html) |
| 12 | [claude-code-telegram](https://github.com/overwirehq/claude-code-telegram) | 2,802 | Serves anyone | No prompts; kept to one directory | ALLOWED_USERS, and ENVIRONMENT=production | [evidence](https://agentskillshub.top/best-runs/telegram/overwirehq__claude-code-telegram.html) |
| 13 | [claude-telegram-relay](https://github.com/godagoo/claude-telegram-relay) | 326 | Serves anyone | Depends on your Claude Code settings | TELEGRAM_USER_ID | [evidence](https://agentskillshub.top/best-runs/telegram/godagoo__claude-telegram-relay.html) |
| 14 | [claudecode-telegram](https://github.com/hanxiao/claudecode-telegram) | 608 | Serves anyone, no setting to change it | Runs with permission prompts off | none exists | [evidence](https://agentskillshub.top/best-runs/telegram/hanxiao__claudecode-telegram.html) |

### Chat-only bots (6)

| # | Bot | ★ | With no allowlist set | Setting to check |  |
|---|---|---|---|---|---|
| 1 | [ChatGPT-Telegram-Workers](https://github.com/tbxark/ChatGPT-Telegram-Workers) | 3,808 | Serves nobody | allowedUserIds (deny by default) | [evidence](https://agentskillshub.top/best-runs/telegram/tbxark__ChatGPT-Telegram-Workers.html) |
| 2 | [chatGPT-telegram-bot](https://github.com/altryne/chatGPT-telegram-bot) | 1,637 | Serves nobody | TELEGRAM_USER_ID (required) | [evidence](https://agentskillshub.top/best-runs/telegram/altryne__chatGPT-telegram-bot.html) |
| 3 | [chatgpt_telegram_bot](https://github.com/father-bot/chatgpt_telegram_bot) | 5,537 | Serves anyone | allowed_telegram_usernames | [evidence](https://agentskillshub.top/best-runs/telegram/father-bot__chatgpt_telegram_bot.html) |
| 4 | [ChatGPT-Telegram-Bot](https://github.com/yym68686/ChatGPT-Telegram-Bot) | 1,290 | Serves anyone | whitelist, ADMIN_LIST | [evidence](https://agentskillshub.top/best-runs/telegram/yym68686__ChatGPT-Telegram-Bot.html) |
| 5 | [ChatGPT-Telegram-Bot](https://github.com/V-know/ChatGPT-Telegram-Bot) | 649 | Serves anyone, no setting to change it | none exists (rate limits only) | [evidence](https://agentskillshub.top/best-runs/telegram/V-know__ChatGPT-Telegram-Bot.html) |
| 6 | [gpt2bot](https://github.com/polakowo/gpt2bot) | 442 | Serves anyone, no setting to change it | none exists | [evidence](https://agentskillshub.top/best-runs/telegram/polakowo__gpt2bot.html) |

[All results, prompts and scripts](https://github.com/zhuyansen/agent-skills-hub/blob/main/ops/telegram-audit/RESULTS.md) · [https://agentskillshub.top/best/telegram-bot/#test-results](https://agentskillshub.top/best/telegram-bot/#test-results)

<a id="type-assistant"></a>
## 💬 AI assistants

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-assistant)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/imkofty/Hermuse"><img src="assets/previews/imkofty__Hermuse.jpg" width="260" alt="imkofty/Hermuse"></a><br><sub><a href="https://github.com/imkofty/Hermuse">imkofty/Hermuse</a></sub></td>
</tr></table>

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [father-bot/chatgpt_telegram_bot](https://github.com/father-bot/chatgpt_telegram_bot) | 5.6k | 💬 Telegram bot with ChatGPT & Claude Python-based, using OpenAI's API. | [SAFE](https://agentskillshub.top/skill/father-bot/chatgpt_telegram_bot/) |
| [tbxark/ChatGPT-Telegram-Workers](https://github.com/tbxark/ChatGPT-Telegram-Workers) | 3.8k | Easily deploy your Telegram ChatGPT bot on Cloudflare Workers (or Vercel, Docker...). | [SAFE](https://agentskillshub.top/skill/tbxark/ChatGPT-Telegram-Workers/) |
| [altryne/chatGPT-telegram-bot](https://github.com/altryne/chatGPT-telegram-bot) | 1.6k | This is a very early attempt at having chatGPT work within a telegram bot | [SAFE](https://agentskillshub.top/skill/altryne/chatGPT-telegram-bot/) |
| [yym68686/ChatGPT-Telegram-Bot](https://github.com/yym68686/ChatGPT-Telegram-Bot) | 1.3k | TeleChat: 🤖️ an AI chat Telegram bot can Web Search Powered by GPT-5, DALL·E , Groq, Gemini 2.5 Pro/Flash and the official Claude4.1 API using Python… | [SAFE](https://agentskillshub.top/skill/yym68686/ChatGPT-Telegram-Bot/) |
| [V-know/ChatGPT-Telegram-Bot](https://github.com/V-know/ChatGPT-Telegram-Bot) | 648 | A Telegram bot with a silky smooth AI experience. UI enabled. | [SAFE](https://agentskillshub.top/skill/V-know/ChatGPT-Telegram-Bot/) |
| [smixs/agent-second-brain](https://github.com/smixs/agent-second-brain) | 466 | An always-on second brain you talk to. Voice notes in Telegram → typed, linked knowledge in your Obsidian vault. Runs 24/7 on the Claude subscription… | [SAFE](https://agentskillshub.top/skill/smixs/agent-second-brain/) |
| [linuz90/claude-telegram-bot](https://github.com/linuz90/claude-telegram-bot) | 451 |  | [SAFE](https://agentskillshub.top/skill/linuz90/claude-telegram-bot/) |
| [polakowo/gpt2bot](https://github.com/polakowo/gpt2bot) | 444 | Your new Telegram buddy powered by transformers | [SAFE](https://agentskillshub.top/skill/polakowo/gpt2bot/) |
| [Johnsheng1/cf-ai-TGbot](https://github.com/Johnsheng1/cf-ai-TGbot) | 377 | CF-ai-TGbot is a customizable Telegram bot powered by Node.js, integrating Cloudflare AI Gateway for smart, context-aware conversations. 🌐🤖 | [SAFE](https://agentskillshub.top/skill/Johnsheng1/cf-ai-TGbot/) |
| [F33RNI/GPT-Telegramus](https://github.com/F33RNI/GPT-Telegramus) | 353 | 💜 The best free Telegram bot for ChatGPT, Microsoft Copilot (aka Bing AI / Sidney / EdgeGPT), Microsoft Copilot Designer (aka BingImageCreator), Gemi… | [CAUTION](https://agentskillshub.top/skill/F33RNI/GPT-Telegramus/) |
| [nalgeon/pokitoki](https://github.com/nalgeon/pokitoki) | 342 | Humble AI Telegram Bot | [SAFE](https://agentskillshub.top/skill/nalgeon/pokitoki/) |
| [pyfbsdk59/Flask-ChatGPT-TelegramBot-Vercel](https://github.com/pyfbsdk59/Flask-ChatGPT-TelegramBot-Vercel) | 305 | 一個Flask ChatGPT TelegramBot快速建置於平台Vercel。 | [SAFE](https://agentskillshub.top/skill/pyfbsdk59/Flask-ChatGPT-TelegramBot-Vercel/) |
| [smixs/iva-agent](https://github.com/smixs/iva-agent) | 292 | AI assistant in Telegram that remembers everything and helps you run your life. Self-hosted in one command. | [SAFE](https://agentskillshub.top/skill/smixs/iva-agent/) |
| [yesbhautik/Master-AI-BOT](https://github.com/yesbhautik/Master-AI-BOT) | 267 | Master AI BOT 🤖: Unleash the power of GPT-4 Turbo with our fast and limitless Telegram bot. Say goodbye to daily usage limits and laggy interfaces. E… | [SAFE](https://agentskillshub.top/skill/yesbhautik/Master-AI-BOT/) |
| [14790897/tg-voice-ai](https://github.com/14790897/tg-voice-ai) | 243 | telegram voice chat ai bot with image generate | [SAFE](https://agentskillshub.top/skill/14790897/tg-voice-ai/) |
| [Helixform/TeleGPT](https://github.com/Helixform/TeleGPT) | 236 | An out-of-box ChatGPT bot for Telegram. | [SAFE](https://agentskillshub.top/skill/Helixform/TeleGPT/) |
| [tpai/summary-gpt-bot](https://github.com/tpai/summary-gpt-bot) | 234 | An AI-powered text summarization Telegram bot that generates concise summaries of text, URLs, PDFs, and YouTube videos. | [SAFE](https://agentskillshub.top/skill/tpai/summary-gpt-bot/) |
| [asukaminato0721/telegram-summary-bot](https://github.com/asukaminato0721/telegram-summary-bot) | 208 | Summarize group chat with AI, LLM && query group chat, FREE to deploy your own, support img, link meta info, reply to, auto fold result, 支持中文检索. | [SAFE](https://agentskillshub.top/skill/asukaminato0721/telegram-summary-bot/) |
| [ciuzaak/Claude-Telegram-Bot](https://github.com/ciuzaak/Claude-Telegram-Bot) | 202 | Anthropic Claude & Google Bard Bot for Telegram. | [SAFE](https://agentskillshub.top/skill/ciuzaak/Claude-Telegram-Bot/) |
| [missingus3r/friday-showcase](https://github.com/missingus3r/friday-showcase) | 194 | Friday — A 24/7 AI Assistant Built Entirely on Claude Code. A Tiny Moon Labs product (tinymoonlabs.com). | [SAFE](https://agentskillshub.top/skill/missingus3r/friday-showcase/) |
| [sudo-eugene/Connect-Telegram-Bot-to-Google-Sheets-ChatGPT-OpenAI](https://github.com/sudo-eugene/Connect-Telegram-Bot-to-Google-Sheets-ChatGPT-OpenAI) | 191 | Connect Telegram Bot to Google Sheets via Google Apps Scripts | [SAFE](https://agentskillshub.top/skill/sudo-eugene/Connect-Telegram-Bot-to-Google-Sheets-ChatGPT-OpenAI/) |
| [flynnoct/chatgpt-telegram-bot](https://github.com/flynnoct/chatgpt-telegram-bot) | 169 | Telegram bot implemented by OFFICIAL OpenAI ChatGPT API (gpt-3.5-turbo, released on 2023-03-01) | [SAFE](https://agentskillshub.top/skill/flynnoct/chatgpt-telegram-bot/) |
| [HexyeDEV/Telegram-Chatbot-Gpt4Free](https://github.com/HexyeDEV/Telegram-Chatbot-Gpt4Free) | 168 | This is a Python-based Telegram bot using the telethon library. The bot responds to messages using the evagpt4 reverse engeneered api from GPT4FREE r… | [SAFE](https://agentskillshub.top/skill/HexyeDEV/Telegram-Chatbot-Gpt4Free/) |
| [Timmy-web/Poe-Telegram-Chatbot](https://github.com/Timmy-web/Poe-Telegram-Chatbot) | 167 | 调用Poe官方API实现Telegram对话机器人，主要调用GPT-4和Claude-3-Opus模型。 | [SAFE](https://agentskillshub.top/skill/Timmy-web/Poe-Telegram-Chatbot/) |
| [imkofty/Hermuse](https://github.com/imkofty/Hermuse) | 159 | Hermuse (Hermes + Muse) — personal AI agent stack built for Muse: Hermes + 9Router + Telegram gateway, automated install, Cloudflare tunnel, watchdog… | [CAUTION](https://agentskillshub.top/skill/imkofty/Hermuse/) |
| [kargarisaac/telegram_link_summarizer_agent](https://github.com/kargarisaac/telegram_link_summarizer_agent) | 155 | Agentic Telegram bot that summarizes links (articles, papers, tweets, LinkedIn posts, PDFs) shared in a channel. Instantly provides concise summaries… | [CAUTION](https://agentskillshub.top/skill/kargarisaac/telegram_link_summarizer_agent/) |
| [innightwolfsleep/llm_telegram_bot](https://github.com/innightwolfsleep/llm_telegram_bot) | 135 | LLM telegram bot | [SAFE](https://agentskillshub.top/skill/innightwolfsleep/llm_telegram_bot/) |
| [Kourva/AwesomeChatGPTBot](https://github.com/Kourva/AwesomeChatGPTBot) | 123 | ChatGPT Telegram bot: Free & Rich-Feature bot for enhanced conversations. | [SAFE](https://agentskillshub.top/skill/Kourva/AwesomeChatGPTBot/) |
| [Hamster-Prime/Smart_Group_Bot](https://github.com/Hamster-Prime/Smart_Group_Bot) | 114 | 基于 LLM 的 Telegram 群聊智能管理机器人 — 智能决策、知识库 RAG、内容审查、贴纸学习、联网搜索、多层记忆架构 | [SAFE](https://agentskillshub.top/skill/Hamster-Prime/Smart_Group_Bot/) |
| [ma2za/telegram-llm-bot](https://github.com/ma2za/telegram-llm-bot) | 114 | Local-first Telegram AI bot with Ollama tool calling, voice transcription, MinIO storage, SearchApi web search, and readiness checks | [SAFE](https://agentskillshub.top/skill/ma2za/telegram-llm-bot/) |
| [Leask/halbot](https://github.com/Leask/halbot) | 102 | Just another AI powered Telegram bot, which is simple design, easy to use, extendable and fun. | [SAFE](https://agentskillshub.top/skill/Leask/halbot/) |
| [htlin222/mini-claw](https://github.com/htlin222/mini-claw) | 95 | Telegram bot for persistent Claude/ChatGPT conversations using Pi agent — zero-cost multi-turn AI sessions with file attachments, shell access, and l… | [SAFE](https://agentskillshub.top/skill/htlin222/mini-claw/) |
| [Lifailon/openrouter-bot](https://github.com/Lifailon/openrouter-bot) | 87 | This project allows to launch your Telegram bot in a few minutes to communicate with free or paid AI models via OpenRouter. | [SAFE](https://agentskillshub.top/skill/Lifailon/openrouter-bot/) |
| [LexiestLeszek/scrapeGPT](https://github.com/LexiestLeszek/scrapeGPT) | 86 | ScrapeGPT is a RAG-based Telegram bot designed to scrape and analyze websites, then answer questions based on the scraped content. The bot utilizes R… | [SAFE](https://agentskillshub.top/skill/LexiestLeszek/scrapeGPT/) |
| [wxc971231/TelegramChatBot](https://github.com/wxc971231/TelegramChatBot) | 82 | A telegram chatbot powered by OpenAI GPT API | [SAFE](https://agentskillshub.top/skill/wxc971231/TelegramChatBot/) |
| [Rai220/TelegramChatGPT](https://github.com/Rai220/TelegramChatGPT) | 81 | Personal telegram chat-bot based on OpenAI GPT-3 finetuning. | [SAFE](https://agentskillshub.top/skill/Rai220/TelegramChatGPT/) |
| [noes14155/Telegrambot-with-GPT](https://github.com/noes14155/Telegrambot-with-GPT) | 79 | telegram bot with gpt | [SAFE](https://agentskillshub.top/skill/noes14155/Telegrambot-with-GPT/) |
| [Magerko/TelegramHelper](https://github.com/Magerko/TelegramHelper) | 78 | Персональный AI-ассистент для Telegram: userbot + control bot с агентом, понимающим голос и свободный текст. SQLite FTS5, Qdrant, Whisper, OpenAI/Gem… | [SAFE](https://agentskillshub.top/skill/Magerko/TelegramHelper/) |
| [tusharhero/aitelegrambot](https://github.com/tusharhero/aitelegrambot) | 75 | aitelegrambot is a telegram bot which uses Ollama as its backend. | [SAFE](https://agentskillshub.top/skill/tusharhero/aitelegrambot/) |
| [dudynets/Telegram-Summarize-Bot](https://github.com/dudynets/Telegram-Summarize-Bot) | 74 | A Telegram bot that summarizes messages from a chat using AI. | [SAFE](https://agentskillshub.top/skill/dudynets/Telegram-Summarize-Bot/) |
| [sazonovanton/SirChatalot](https://github.com/sazonovanton/SirChatalot) | 74 | A Telegram bot that proves you don't need a body to have a personality. Works with any OpenAI-compatible LLM; agentic tools, MCP, RAG over your files… | [SAFE](https://agentskillshub.top/skill/sazonovanton/SirChatalot/) |
| [harshitethic/ChatGPT-Telegram-Bot](https://github.com/harshitethic/ChatGPT-Telegram-Bot) | 72 | Legacy Python Telegram AI bot example, with safer key handling, configuration tests, and documented compatibility limits | [SAFE](https://agentskillshub.top/skill/harshitethic/ChatGPT-Telegram-Bot/) |
| [flows-network/telegram-llm](https://github.com/flows-network/telegram-llm) | 71 | A Telegram LLM bot written in Rust | [SAFE](https://agentskillshub.top/skill/flows-network/telegram-llm/) |
| [jf3tt/chatgpt-telegram-bot](https://github.com/jf3tt/chatgpt-telegram-bot) | 62 | Python telegram bot, which utilizes the OpenAI API for implementing GPT-4 and speech-to-text functionality. The bot handles text and voice input from… | [SAFE](https://agentskillshub.top/skill/jf3tt/chatgpt-telegram-bot/) |
| [thaolst/tara-bot](https://github.com/thaolst/tara-bot) | 62 | Tara Bot — AI Telegram agent: search flights, compare prices, inject affiliate links | [SAFE](https://agentskillshub.top/skill/thaolst/tara-bot/) |
| [s-nagaev/chibi](https://github.com/s-nagaev/chibi) | 56 | Your Digital Companion. Self-hosted Telegram bot orchestrating multiple AI providers (OpenAI, Anthropic, Google, xAI, DeepSeek, Mistral, Alibaba, Min… | [SAFE](https://agentskillshub.top/skill/s-nagaev/chibi/) |
| [vladislav-bordiug/ChatGPT_DALL_E_StableDiffusion_Telegram_Bot](https://github.com/vladislav-bordiug/ChatGPT_DALL_E_StableDiffusion_Telegram_Bot) | 56 | This is ChatGPT, DALL·E, Stable Diffusion python-telegram-bot with cryptocurrency payments. It allows you to generate images and chat with ChatGPT. | [CAUTION](https://agentskillshub.top/skill/vladislav-bordiug/ChatGPT_DALL_E_StableDiffusion_Telegram_Bot/) |
| [KonstantinVanov/Article-Assistant--RAG-Telegram-Bot](https://github.com/KonstantinVanov/Article-Assistant--RAG-Telegram-Bot) | 54 | A sophisticated RAG (Retrieval-Augmented Generation) Telegram bot that transforms articles and documents into interactive knowledge bases. Upload PDF… | [SAFE](https://agentskillshub.top/skill/KonstantinVanov/Article-Assistant--RAG-Telegram-Bot/) |
| [Mostafa-Abbasi/HyperTAG](https://github.com/Mostafa-Abbasi/HyperTAG) | 54 | HyperTAG Bot - AI-Generated Tags and Summaries for Telegram Messages | [SAFE](https://agentskillshub.top/skill/Mostafa-Abbasi/HyperTAG/) |
| [emingenc/telegramGPT](https://github.com/emingenc/telegramGPT) | 53 | step-by-step guide on creating your very own AI bot using Python, Telegram, and OpenAI GPT models. | [SAFE](https://agentskillshub.top/skill/emingenc/telegramGPT/) |
| [AlexTs10/ai-girlfriend-with-voice-telegram-bot](https://github.com/AlexTs10/ai-girlfriend-with-voice-telegram-bot) | 52 | GPT Telegram Bot | [SAFE](https://agentskillshub.top/skill/AlexTs10/ai-girlfriend-with-voice-telegram-bot/) |
| [ahkarimi/chapar](https://github.com/ahkarimi/chapar) | 44 | Self-hosted Telegram bot for AI-driven chart analysis and market intelligence. FastAPI + Celery + Redis + PostgreSQL. | [SAFE](https://agentskillshub.top/skill/ahkarimi/chapar/) |
| [AbuZar-Ansarii/Openclaw-phone-control](https://github.com/AbuZar-Ansarii/Openclaw-phone-control) | 37 | OpenClaw allows you to manage your phone via a Telegram bot using the power of local AI (Ollama). No root access is required, making it accessible fo… | [CAUTION](https://agentskillshub.top/skill/AbuZar-Ansarii/Openclaw-phone-control/) |
| [tuuject/surowan](https://github.com/tuuject/surowan) | 37 | 基于 Agent 的 AI 驱动 Telegram Bot「塑料碗」 | [SAFE](https://agentskillshub.top/skill/tuuject/surowan/) |
| [zhuchangyi/Gemini2tg](https://github.com/zhuchangyi/Gemini2tg) | 31 | Gemini2tg is a project which deploys Google Gemini's API to a Telegram bot, giving you your own AI bot powerd by Gemini | [CAUTION](https://agentskillshub.top/skill/zhuchangyi/Gemini2tg/) |
| [xingty/CatGPT](https://github.com/xingty/CatGPT) | 30 | A telegram bot for OpenAI API | [SAFE](https://agentskillshub.top/skill/xingty/CatGPT/) |
| [maddness/vkusvill-mcp-bot](https://github.com/maddness/vkusvill-mcp-bot) | 29 | Telegram-бот для сбора продуктовой корзины ВкусВилл через mcp | [CAUTION](https://agentskillshub.top/skill/maddness/vkusvill-mcp-bot/) |
| [aneeshjoy/llama-telegram-bot](https://github.com/aneeshjoy/llama-telegram-bot) | 28 | A simple telegram chat bot for LLMs supported by llama.cpp | [CAUTION](https://agentskillshub.top/skill/aneeshjoy/llama-telegram-bot/) |
| [shanzi/Telegram-ChatGPT](https://github.com/shanzi/Telegram-ChatGPT) | 28 | A customizable Telegram bot with a ChatGPT (or GPT4, bring your own API key) backend. You can configure the bot’s context and prompt in template sett… | [SAFE](https://agentskillshub.top/skill/shanzi/Telegram-ChatGPT/) |
| [AbhiTheModder/gemini-ai-telegram](https://github.com/AbhiTheModder/gemini-ai-telegram) | 26 | Pyrogram(Pyrofork) Based Python script for Telegram Userbots and Bots | [SAFE](https://agentskillshub.top/skill/AbhiTheModder/gemini-ai-telegram/) |
| [anxkhn/OpynGPT-Chat](https://github.com/anxkhn/OpynGPT-Chat) | 23 | A Telegram chat bot powered by OpynGPT for natural language responses without the need for API keys. Easy to set up and use. | [SAFE](https://agentskillshub.top/skill/anxkhn/OpynGPT-Chat/) |
| [LuKresXD/claw-skeleton](https://github.com/LuKresXD/claw-skeleton) | 22 | 🪼 A personal AI assistant that lives in Telegram — every topic is its own isolated Claude Code agent with layered persistent memory and proactive cro… | [CAUTION](https://agentskillshub.top/skill/LuKresXD/claw-skeleton/) |
| [JackBekket/Hellper](https://github.com/JackBekket/Hellper) | 21 | Telegram bot which can work with both openAI and LocalAI modes, it also uses UncensoredGPT models like Wizard-Uncensored. It can be launch at ordinar… | [SAFE](https://agentskillshub.top/skill/JackBekket/Hellper/) |
| [muthupriyan-dev/telegram-ai-bot](https://github.com/muthupriyan-dev/telegram-ai-bot) | 21 |  | [SAFE](https://agentskillshub.top/skill/muthupriyan-dev/telegram-ai-bot/) |
| [EzeSandes/ChatGPT-OpenAI-TelegramBot](https://github.com/EzeSandes/ChatGPT-OpenAI-TelegramBot) | 15 | Unofficial OpenAI Telegram bot to interact with chatGPT | [SAFE](https://agentskillshub.top/skill/EzeSandes/ChatGPT-OpenAI-TelegramBot/) |
| [Tobiaspk/gpt3_telebot](https://github.com/Tobiaspk/gpt3_telebot) | 15 | Telegram Bot using GPT3 and enhanced functions | [SAFE](https://agentskillshub.top/skill/Tobiaspk/gpt3_telebot/) |
| [pyfbsdk59/Flask-ChatGPT-TelegramBot-Render](https://github.com/pyfbsdk59/Flask-ChatGPT-TelegramBot-Render) | 15 | 一個Flask ChatGPT TelegramBot快速建置於平台Render。 | [SAFE](https://agentskillshub.top/skill/pyfbsdk59/Flask-ChatGPT-TelegramBot-Render/) |
| [andykras/gptbot](https://github.com/andykras/gptbot) | 14 | Telegram bot with Assistant AsyncOpenAI API client and aiogram lib | [CAUTION](https://agentskillshub.top/skill/andykras/gptbot/) |
| [Exdenta/OinkAIJobSearch](https://github.com/Exdenta/OinkAIJobSearch) | 10 | AI job-search agent in Telegram — scrapes 25+ job boards, scores every posting against your CV with Claude, pushes real matches to your chat. Self-ho… | [CAUTION](https://agentskillshub.top/skill/Exdenta/OinkAIJobSearch/) |
| [alifgardika/CatatAja](https://github.com/alifgardika/CatatAja) | 9 | Bot Telegram pencatat pengeluaran tanpa server. Ketik transaksi pakai bahasa sehari-hari, bot memahaminya dengan Gemini AI lalu menyimpannya ke Googl… | [SAFE](https://agentskillshub.top/skill/alifgardika/CatatAja/) |
| [deseven/telegram-actual-llm-helper](https://github.com/deseven/telegram-actual-llm-helper) | 9 | A bot to assist with logging transactions in Actual Budget, leveraging the capabilities of ChatGPT or other LLMs | [SAFE](https://agentskillshub.top/skill/deseven/telegram-actual-llm-helper/) |
| [dhir4j/chatgpt-bot-telegram](https://github.com/dhir4j/chatgpt-bot-telegram) | 9 | A Python script that implements a basic chatbot using the OpenAI GPT-3 API. | [SAFE](https://agentskillshub.top/skill/dhir4j/chatgpt-bot-telegram/) |
| [irfan-yulianto/Telegram-Finance-Bot](https://github.com/irfan-yulianto/Telegram-Finance-Bot) | 8 | AI-powered personal finance tracker bot for Telegram. Track income & expenses with receipt scanning, natural language input, and automatic Google She… | [CAUTION](https://agentskillshub.top/skill/irfan-yulianto/Telegram-Finance-Bot/) |
| [backmeupplz/telegram-ai-searcher](https://github.com/backmeupplz/telegram-ai-searcher) | 7 | Telegram bot that searches the web and streams AI answers live. Live demo: https://t.me/frdy_bot — built with grammY, Fireworks AI, and self-hosted S… | [SAFE](https://agentskillshub.top/skill/backmeupplz/telegram-ai-searcher/) |
| [hschickdevs/Telegram-AI-Software-Architect](https://github.com/hschickdevs/Telegram-AI-Software-Architect) | 7 | Telegram bot that uses AI to generate full codebases from user prompts, providing structured, ready-to-deploy software projects, differentiating from… | [SAFE](https://agentskillshub.top/skill/hschickdevs/Telegram-AI-Software-Architect/) |
| [Aman262626/DarkGPT-Telegram-Bot](https://github.com/Aman262626/DarkGPT-Telegram-Bot) | 6 | 🌑 DarkGPT - A powerful Telegram bot powered by Claude Opus AI with conversation memory and multi-language support | [SAFE](https://agentskillshub.top/skill/Aman262626/DarkGPT-Telegram-Bot/) |
| [DoctorSB/GPT_Telegram_Bot](https://github.com/DoctorSB/GPT_Telegram_Bot) | 6 | Код для работы с api openai | [SAFE](https://agentskillshub.top/skill/DoctorSB/GPT_Telegram_Bot/) |
| [aleksbuss/termux-voice-bot](https://github.com/aleksbuss/termux-voice-bot) | 6 | A pocket-sized AI server running on your Android smartphone. This project turns your phone into a fully autonomous Telegram bot for voice and text pr… | [SAFE](https://agentskillshub.top/skill/aleksbuss/termux-voice-bot/) |
| [c17hawke/chatGPT-Telegram-bot](https://github.com/c17hawke/chatGPT-Telegram-bot) | 6 | chatGPT-Telegram-bot | [SAFE](https://agentskillshub.top/skill/c17hawke/chatGPT-Telegram-bot/) |
| [ibidathoillah/gemini-cli-telegram](https://github.com/ibidathoillah/gemini-cli-telegram) | 6 | Run Google Gemini CLI as a Telegram bot. AI coding assistant with project management, scheduled tasks, and autopilot mode. | [CAUTION](https://agentskillshub.top/skill/ibidathoillah/gemini-cli-telegram/) |
| [rokoss21/OpenBot-2.0](https://github.com/rokoss21/OpenBot-2.0) | 6 | This Telegram bot interfaces with AI models via OpenRouter, enabling users to authenticate with an API key, select AI models for interaction, process… | [CAUTION](https://agentskillshub.top/skill/rokoss21/OpenBot-2.0/) |
| [Cloudveerge/Gemini-1.5-flash-AI-Telegram-Bot](https://github.com/Cloudveerge/Gemini-1.5-flash-AI-Telegram-Bot) | 5 | An intelligent, conversational Telegram bot built on Node.js, leveraging the gemini-1.5-flash generative AI model. | [SAFE](https://agentskillshub.top/skill/Cloudveerge/Gemini-1.5-flash-AI-Telegram-Bot/) |
| [YevgeniyKapustin/VanessaAI](https://github.com/YevgeniyKapustin/VanessaAI) | 5 | Telegram AI Bot | [SAFE](https://agentskillshub.top/skill/YevgeniyKapustin/VanessaAI/) |
| [binnwkwk/SylvieAi-Telegram-Bot](https://github.com/binnwkwk/SylvieAi-Telegram-Bot) | 5 | This is the source code of the Sylvie AI telegram bot | [SAFE](https://agentskillshub.top/skill/binnwkwk/SylvieAi-Telegram-Bot/) |
| [bisbeebucky/ai-bot](https://github.com/bisbeebucky/ai-bot) | 5 | AI Telegram personal finance bot with cashflow forecasting and overdraft prediction | [SAFE](https://agentskillshub.top/skill/bisbeebucky/ai-bot/) |
| [divanshusingh-ds/TELREGRAM-BOT](https://github.com/divanshusingh-ds/TELREGRAM-BOT) | 5 | AI-powered Telegram assistant built with Python, Google Gemini, LangChain & LangGraph, featuring agentic tool calling, conversation memory, and modul… | [SAFE](https://agentskillshub.top/skill/divanshusingh-ds/TELREGRAM-BOT/) |
| [djblack1209-coder/OpenClaw-Bot](https://github.com/djblack1209-coder/OpenClaw-Bot) | 5 | Cenlio is a desktop workspace for intelligence briefs, research and multi-agent workflows. Built with Tauri, React and Python. | [SAFE](https://agentskillshub.top/skill/djblack1209-coder/OpenClaw-Bot/) |
| [flows-network/telegram-claude](https://github.com/flows-network/telegram-claude) | 5 |  | [SAFE](https://agentskillshub.top/skill/flows-network/telegram-claude/) |
| [palaklohade/pdf_Sumarizer_telegram_bot](https://github.com/palaklohade/pdf_Sumarizer_telegram_bot) | 5 | A Telegram bot built with Python that summarizes PDF files using an LLM model. Users can send PDFs to the bot and receive concise summaries or answer… | [SAFE](https://agentskillshub.top/skill/palaklohade/pdf_Sumarizer_telegram_bot/) |
| [tanishra/Telegram-Smart-Agent-Bot](https://github.com/tanishra/Telegram-Smart-Agent-Bot) | 5 | SmartAgent Bot is an AI-powered Telegram bot built using n8n workflows and Google Gemini models. It processes both text and voice messages, intellige… | [SAFE](https://agentskillshub.top/skill/tanishra/Telegram-Smart-Agent-Bot/) |
| [zkrige/zoidberg](https://github.com/zkrige/zoidberg) | 5 | Your own Claude on your own hardware, running on your Claude subscription instead of metered API credit. Talk to it on Telegram; it runs your schedul… | [SAFE](https://agentskillshub.top/skill/zkrige/zoidberg/) |

<a id="type-remote"></a>
## 🛰 Agent remote control

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-remote)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/SouravBeraAkaSpeed/xiryn"><img src="assets/previews/SouravBeraAkaSpeed__xiryn.jpg" width="260" alt="SouravBeraAkaSpeed/xiryn"></a><br><sub><a href="https://github.com/SouravBeraAkaSpeed/xiryn">SouravBeraAkaSpeed/xiryn</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/smixs/pi-durable-telegram"><img src="assets/previews/smixs__pi-durable-telegram.jpg" width="260" alt="smixs/pi-durable-telegram"></a><br><sub><a href="https://github.com/smixs/pi-durable-telegram">smixs/pi-durable-telegram</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/ortegarod/openclaw-vps-deploy"><img src="assets/previews/ortegarod__openclaw-vps-deploy.jpg" width="260" alt="ortegarod/openclaw-vps-deploy"></a><br><sub><a href="https://github.com/ortegarod/openclaw-vps-deploy">ortegarod/openclaw-vps-deploy</a></sub></td>
</tr></table>

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [overwirehq/claude-code-telegram](https://github.com/overwirehq/claude-code-telegram) | 2.8k | A powerful Telegram bot that provides remote access to Claude Code, enabling developers to interact with their projects from anywhere with full AI as… | [SAFE](https://agentskillshub.top/skill/overwirehq/claude-code-telegram/) |
| [grinev/opencode-telegram-bot](https://github.com/grinev/opencode-telegram-bot) | 1.4k | OpenCode mobile client via Telegram: run and monitor AI coding tasks from your phone while everything runs locally on your machine. OpenCode V2 suppo… | [SAFE](https://agentskillshub.top/skill/grinev/opencode-telegram-bot/) |
| [banteg/takopi](https://github.com/banteg/takopi) | 1.1k | he just wants to help-pi! | [SAFE](https://agentskillshub.top/skill/banteg/takopi/) |
| [hanxiao/claudecode-telegram](https://github.com/hanxiao/claudecode-telegram) | 613 | Telegram bridge for Claude Code | [SAFE](https://agentskillshub.top/skill/hanxiao/claudecode-telegram/) |
| [duckbugio/flock](https://github.com/duckbugio/flock) | 495 | Autonomous AI dev-team bot | [SAFE](https://agentskillshub.top/skill/duckbugio/flock/) |
| [PleasePrompto/ductor](https://github.com/PleasePrompto/ductor) | 467 | Control Claude Code, Codex CLI and Gemini CLI from Telegram. Live streaming, persistent memory, cron jobs, webhooks, Docker sandboxing. | [SAFE](https://agentskillshub.top/skill/PleasePrompto/ductor/) |
| [SouravBeraAkaSpeed/xiryn](https://github.com/SouravBeraAkaSpeed/xiryn) | 435 | Xiryn — the open-source personal agent. Does everything Muse, Grok Bot and Dots do, on your own computer: each agent gets its own Linux desktop in Do… | [SAFE](https://agentskillshub.top/skill/SouravBeraAkaSpeed/xiryn/) |
| [godagoo/claude-telegram-relay](https://github.com/godagoo/claude-telegram-relay) | 330 | Minimal pattern for running Claude Code as an always-on Telegram bot. Cross-platform daemon setup included. | [SAFE](https://agentskillshub.top/skill/godagoo/claude-telegram-relay/) |
| [alexei-led/ccgram](https://github.com/alexei-led/ccgram) | 288 | Telegram ↔ tmux/herdr/agterm bridge for Claude Code, Codex CLI, and Pi Agent. Monitor output, respond to prompts, manage parallel sessions. Control A… | [SAFE](https://agentskillshub.top/skill/alexei-led/ccgram/) |
| [six-ddc/ccbot](https://github.com/six-ddc/ccbot) | 278 | Telegram ↔ tmux bridge for Claude Code: 1 topic = 1 window = 1 session | [SAFE](https://agentskillshub.top/skill/six-ddc/ccbot/) |
| [emreturkmencom/antigravity-telegram-suite](https://github.com/emreturkmencom/antigravity-telegram-suite) | 194 | Antigravity Telegram bot — remote-control your AI agent via Telegram. Chat, switch models, orchestrate multi-agent workflows, and manage workspaces f… | [SAFE](https://agentskillshub.top/skill/emreturkmencom/antigravity-telegram-suite/) |
| [earlyaidopters/claudeclaw](https://github.com/earlyaidopters/claudeclaw) | 174 | Claude Code CLI as a personal Telegram bot — voice, memory, scheduled tasks, all your skills from your pocket. | [SAFE](https://agentskillshub.top/skill/earlyaidopters/claudeclaw/) |
| [NachoSEO/claudegram](https://github.com/NachoSEO/claudegram) | 158 | Telegram bot that bridges messages to Claude Code | [SAFE](https://agentskillshub.top/skill/NachoSEO/claudegram/) |
| [k1p1l0/claude-telegram-supercharged](https://github.com/k1p1l0/claude-telegram-supercharged) | 146 | Run Claude Code 24/7 from Telegram. Drop-in upgrade for the official plugin: voice notes both ways, a self-healing daemon, memory across restarts, an… | [SAFE](https://agentskillshub.top/skill/k1p1l0/claude-telegram-supercharged/) |
| [terranc/claude-telegram-bot-bridge](https://github.com/terranc/claude-telegram-bot-bridge) | 136 | A lightweight Telegram bot that bridges Claude Code to any local folder, with autostart support for remote mobile development. | [CAUTION](https://agentskillshub.top/skill/terranc/claude-telegram-bot-bridge/) |
| [kaida-palooza/ccpoke](https://github.com/kaida-palooza/ccpoke) | 102 | Bridge between AI coding agents and your phone — notifications, 2-way chat, permissions | [SAFE](https://agentskillshub.top/skill/kaida-palooza/ccpoke/) |
| [Ansh-Vortex/Vortex-Advance-RAT](https://github.com/Ansh-Vortex/Vortex-Advance-RAT) | 101 | Advance Open-Source RAT Builder Access via Telegram Bot with over 60+ commands | [SAFE](https://agentskillshub.top/skill/Ansh-Vortex/Vortex-Advance-RAT/) |
| [seedprod/openclaw-prompts-and-skills](https://github.com/seedprod/openclaw-prompts-and-skills) | 95 | Telegram bot that talks to headless Claude Code - proof of concept | [UNSAFE](https://agentskillshub.top/skill/seedprod/openclaw-prompts-and-skills/) |
| [gergomiklos/heyagent](https://github.com/gergomiklos/heyagent) | 94 | Telegram bridge for Claude Code and Codex CLI | [SAFE](https://agentskillshub.top/skill/gergomiklos/heyagent/) |
| [MaxMiksa/Tele-Bot](https://github.com/MaxMiksa/Tele-Bot) | 90 | A clean Bot running on your PC, interacting with you on Telegram via Claude or Codex. | [SAFE](https://agentskillshub.top/skill/MaxMiksa/Tele-Bot/) |
| [pavel-molyanov/telegram-ai-agent](https://github.com/pavel-molyanov/telegram-ai-agent) | 90 | Generic Claude/Codex Telegram bot runtime | [SAFE](https://agentskillshub.top/skill/pavel-molyanov/telegram-ai-agent/) |
| [areweai/tsgram-mcp](https://github.com/areweai/tsgram-mcp) | 88 | TSGram - Telegram MCP Server for local Claude Code integration - debug and vibe code on the go! | [CAUTION](https://agentskillshub.top/skill/areweai/tsgram-mcp/) |
| [permgps/herdr-telegram-agents](https://github.com/permgps/herdr-telegram-agents) | 88 | Drive your coding agents from Telegram like from the terminal. A topic per agent, live status in the topic icon, two-way chat with inline buttons for… | [SAFE](https://agentskillshub.top/skill/permgps/herdr-telegram-agents/) |
| [0xtbug/telbot](https://github.com/0xtbug/telbot) | 84 | Go-based tool for managing Telkomsel accounts via Telegram Bot, Terminal CLI, or MCP Server (for AI agents). | [CAUTION](https://agentskillshub.top/skill/0xtbug/telbot/) |
| [littlebearapps/untether](https://github.com/littlebearapps/untether) | 77 | Run your coding agents from Telegram. A bridge for Claude Code, Codex, OpenCode, Pi and Antigravity CLI: send tasks by text or voice, watch them work… | [SAFE](https://agentskillshub.top/skill/littlebearapps/untether/) |
| [b1rdmania/ghostclaw](https://github.com/b1rdmania/ghostclaw) | 67 | an AI that lives on your computer and does stuff for you. Public beta. | [SAFE](https://agentskillshub.top/skill/b1rdmania/ghostclaw/) |
| [Jeffrey0117/ClaudeBot](https://github.com/Jeffrey0117/ClaudeBot) | 65 | Not a pipe to Claude. A command center on your phone. — Telegram bot for Claude Code CLI with plugin system, multi-bot, queue, streaming, and hot-rel… | [SAFE](https://agentskillshub.top/skill/Jeffrey0117/ClaudeBot/) |
| [suzuke/AgEnD](https://github.com/suzuke/AgEnD) | 64 | Multi-agent fleet daemon — run Claude Code, Gemini CLI, Codex, and OpenCode from Telegram with cross-instance collaboration | [SAFE](https://agentskillshub.top/skill/suzuke/AgEnD/) |
| [smixs/pi-durable-telegram](https://github.com/smixs/pi-durable-telegram) | 48 | Always-on durable pi agent on your server that you talk to in Telegram. Survives crashes and restarts, keeps history in SQLite. pi-durable Telegram g… | [SAFE](https://agentskillshub.top/skill/smixs/pi-durable-telegram/) |
| [bluzir/claude-telegram](https://github.com/bluzir/claude-telegram) | 42 | A simple and modular Telegram orchestrator on top of Claude Code CLI | [SAFE](https://agentskillshub.top/skill/bluzir/claude-telegram/) |
| [alhinawi/telegram-notifier](https://github.com/alhinawi/telegram-notifier) | 38 | Universal Telegram Notifier Plugin & Skill for AI Agents (Antigravity, Claude Code, Codex, Cursor, Windsurf) + Remote Control Setup | [SAFE](https://agentskillshub.top/skill/alhinawi/telegram-notifier/) |
| [Tommertom/coderBOT](https://github.com/Tommertom/coderBOT) | 37 | CoderBOT - using Telegram to control your favorite AI coder CLI | [SAFE](https://agentskillshub.top/skill/Tommertom/coderBOT/) |
| [Imolatte/claude-cli-telegram](https://github.com/Imolatte/claude-cli-telegram) | 36 | Turn your Mac/Linux into a remote Claude Code terminal via Telegram. Spawns real CLI — sessions, streaming, approvals, voice, git panel, 30+ commands. | [SAFE](https://agentskillshub.top/skill/Imolatte/claude-cli-telegram/) |
| [archetyx/telegram-mcp-server](https://github.com/archetyx/telegram-mcp-server) | 30 | Remote control AI coding assistants (Claude Code/Codex) via Telegram | [SAFE](https://agentskillshub.top/skill/archetyx/telegram-mcp-server/) |
| [mmr710/nightmux](https://github.com/mmr710/nightmux) | 28 | The vendor-neutral night shift for AI coding agents. Claude, Codex, Gemini & more from one phone: fail over when one runs out, loop until your tests… | [SAFE](https://agentskillshub.top/skill/mmr710/nightmux/) |
| [AvivK5498/Golem](https://github.com/AvivK5498/Golem) | 27 | A self-hosted platform for creating and managing personal AI agents. Each agent gets its own Telegram bot, custom persona, tools, memory, and skills.… | [SAFE](https://agentskillshub.top/skill/AvivK5498/Golem/) |
| [jsayubi/ccgram](https://github.com/jsayubi/ccgram) | 26 | Control Claude Code from Telegram — remote notifications, permission approvals, and keystroke injection via Telegram bot | [CAUTION](https://agentskillshub.top/skill/jsayubi/ccgram/) |
| [soulknight666/telegram-account-orchestrator](https://github.com/soulknight666/telegram-account-orchestrator) | 25 | Self-hosted Telegram multi-account management with Web UI, CLI, Bot, MCP, Telethon, and Telegram Desktop tdata import. | [SAFE](https://agentskillshub.top/skill/soulknight666/telegram-account-orchestrator/) |
| [petrludwig-collab/Agent2Telegram](https://github.com/petrludwig-collab/Agent2Telegram) | 23 | Connect a coding agent (Claude Code, Codex, Antigravity) to Telegram. Dependency-free, robust, secure. | [SAFE](https://agentskillshub.top/skill/petrludwig-collab/Agent2Telegram/) |
| [Zulut30/premium-telegram-emoji](https://github.com/Zulut30/premium-telegram-emoji) | 21 | Verified Telegram custom emoji catalog and portable Agent Skill. Meaning-aware selection, stable application styles, Windows/macOS/Linux. | [SAFE](https://agentskillshub.top/skill/Zulut30/premium-telegram-emoji/) |
| [yschaub/codex-telegram](https://github.com/yschaub/codex-telegram) | 21 | A powerful Telegram bot that provides remote access to Codex CLI, enabling developers to interact with their projects from anywhere with full AI assi… | [SAFE](https://agentskillshub.top/skill/yschaub/codex-telegram/) |
| [kcisoul/remotecode](https://github.com/kcisoul/remotecode) | 18 | Control Claude Code remotely through Telegram. | [SAFE](https://agentskillshub.top/skill/kcisoul/remotecode/) |
| [TheStack-ai/mrstack](https://github.com/TheStack-ai/mrstack) | 16 | Run Claude Code from Telegram — AI dev partner that works 24/7, even when terminal is closed. pip install mrstack | [CAUTION](https://agentskillshub.top/skill/TheStack-ai/mrstack/) |
| [WireCatLabs/tg-cli](https://github.com/WireCatLabs/tg-cli) | 16 | Telegram CLI for AI agents — your whole account in the terminal, local-first search, MCP server and full Bot API. | [SAFE](https://agentskillshub.top/skill/WireCatLabs/tg-cli/) |
| [mgaitan/telegram-acp-bot](https://github.com/mgaitan/telegram-acp-bot) | 16 | A Telegram bot that implements Agent Client Protocol to interact with AI agents | [SAFE](https://agentskillshub.top/skill/mgaitan/telegram-acp-bot/) |
| [hada0127/cc-telegram](https://github.com/hada0127/cc-telegram) | 14 | telegram bot for claude-code | [SAFE](https://agentskillshub.top/skill/hada0127/cc-telegram/) |
| [guzus/tg-claude](https://github.com/guzus/tg-claude) | 13 | Telegram/Discord client for Claude Code | [SAFE](https://agentskillshub.top/skill/guzus/tg-claude/) |
| [dewil/claude-control](https://github.com/dewil/claude-control) | 12 | Manage Claude Code and Codex agents across projects: remote sessions, background tasks, Telegram control, and a web panel for answering questions and… | [UNSAFE](https://agentskillshub.top/skill/dewil/claude-control/) |
| [sleeyax/claude-code-session-bot](https://github.com/sleeyax/claude-code-session-bot) | 12 | Telegram bot to warm up your Claude code session while you're AFK | [SAFE](https://agentskillshub.top/skill/sleeyax/claude-code-session-bot/) |
| [kawaiipantsu/telegramdigger](https://github.com/kawaiipantsu/telegramdigger) | 10 | This tool is an implementation of the Telegram Bot API for Linux terminal use. It's ment for quick OSINT and grading useful information or to do thin… | [CAUTION](https://agentskillshub.top/skill/kawaiipantsu/telegramdigger/) |
| [lucashcaraujo/claude-telegram](https://github.com/lucashcaraujo/claude-telegram) | 9 |  | [SAFE](https://agentskillshub.top/skill/lucashcaraujo/claude-telegram/) |
| [moeacgx/cc-switch-bot](https://github.com/moeacgx/cc-switch-bot) | 9 | Telegram Bot for managing Claude Code / Codex / Gemini provider switching, deployed on Cloudflare Workers | [CAUTION](https://agentskillshub.top/skill/moeacgx/cc-switch-bot/) |
| [0xkaz/codex-gemini-telegram-bridge](https://github.com/0xkaz/codex-gemini-telegram-bridge) | 7 | Telegram bridges for running Codex CLI and Gemini CLI from a single authorized chat | [SAFE](https://agentskillshub.top/skill/0xkaz/codex-gemini-telegram-bridge/) |
| [choiyounggi/cliclaw](https://github.com/choiyounggi/cliclaw) | 7 | Control coding agents on your Mac — Claude Code, Codex, Pi, Gemini — from your phone via Telegram. Kick off tasks, stream progress, and approve dange… | [SAFE](https://agentskillshub.top/skill/choiyounggi/cliclaw/) |
| [kky42/anyagent](https://github.com/kky42/anyagent) | 7 | Run Codex, Claude, or Pi from Telegram. | [SAFE](https://agentskillshub.top/skill/kky42/anyagent/) |
| [switchroom/switchroom](https://github.com/switchroom/switchroom) | 7 | Run Claude Code 24/7 on your Claude Pro/Max subscription over Telegram. | [CAUTION](https://agentskillshub.top/skill/switchroom/switchroom/) |
| [azalio/claude-telegram-skill](https://github.com/azalio/claude-telegram-skill) | 6 | Telegram bridge skill for Claude Code: notify-on-done + non-blocking two-way chat, multi-session, no daemon | [SAFE](https://agentskillshub.top/skill/azalio/claude-telegram-skill/) |
| [ortegarod/openclaw-vps-deploy](https://github.com/ortegarod/openclaw-vps-deploy) | 6 | Deploy a personal OpenClaw agent to a fresh Ubuntu VPS with one command from your computer. Connects Claude and your Telegram bot, locks the server d… | [SAFE](https://agentskillshub.top/skill/ortegarod/openclaw-vps-deploy/) |
| [probelabs/afk](https://github.com/probelabs/afk) | 6 | Remote control and approval system for Claude Code via Telegram. Zero dependencies, Node.js 18+ built-ins only. | [SAFE](https://agentskillshub.top/skill/probelabs/afk/) |
| [simontt88/thronglets](https://github.com/simontt88/thronglets) | 6 | Spawn AI coding agents from Telegram. Each gets a name, pixel art avatar, and workspace. Fleet management for Cursor, Claude Code, and Codex. | [SAFE](https://agentskillshub.top/skill/simontt88/thronglets/) |
| [stebou/claude-code-telegram-gcp](https://github.com/stebou/claude-code-telegram-gcp) | 6 |  | [CAUTION](https://agentskillshub.top/skill/stebou/claude-code-telegram-gcp/) |
| [HNF-FRN/Reel-watcher-telegram-Agent](https://github.com/HNF-FRN/Reel-watcher-telegram-Agent) | 5 | Send a reel to a Telegram bot: it tells you exactly what the video shows, then plans and builds it on your Windows PC with Claude Code, asking your p… | [SAFE](https://agentskillshub.top/skill/HNF-FRN/Reel-watcher-telegram-Agent/) |
| [Hormold/cursor-telegram-bot](https://github.com/Hormold/cursor-telegram-bot) | 5 | A powerful Telegram bot for managing Cursor AI Background Composers with intelligent task management and real-time monitoring. | [SAFE](https://agentskillshub.top/skill/Hormold/cursor-telegram-bot/) |
| [KhanbalaRashidov/telepath](https://github.com/KhanbalaRashidov/telepath) | 5 | Send coding tasks to an AI coding agent on your own machine from Telegram. Watch it work in real time, approve risky actions, and get every change as… | [SAFE](https://agentskillshub.top/skill/KhanbalaRashidov/telepath/) |
| [asianviking/pochi](https://github.com/asianviking/pochi) | 5 | Multi-model AI agent Telegram bot for multi-folder workspaces. | [SAFE](https://agentskillshub.top/skill/asianviking/pochi/) |
| [danimoya/Claude-B](https://github.com/danimoya/Claude-B) | 5 | Background-capable Claude Code wrapper with async workflows, session management, and multi-host orchestration. Telegram Integration, TTS-STT with mul… | [CAUTION](https://agentskillshub.top/skill/danimoya/Claude-B/) |
| [junecv/vibeIDE](https://github.com/junecv/vibeIDE) | 5 | Code from your phone. Telegram bot that gives you Claude Code. Start on your laptop, pick up on your phone. | [SAFE](https://agentskillshub.top/skill/junecv/vibeIDE/) |
| [nguyencaotai1969/telegram-bot-router](https://github.com/nguyencaotai1969/telegram-bot-router) | 5 | Control Claude Code from Telegram: one bot, one group, each topic drives Claude Code in its own project folder. Photos & files both ways. | [SAFE](https://agentskillshub.top/skill/nguyencaotai1969/telegram-bot-router/) |
| [zalogarcia/leash](https://github.com/zalogarcia/leash) | 5 | Talk to Claude Code on your own machine, from your phone, over Telegram. No tunnel, no webhook, no cloud relay. | [SAFE](https://agentskillshub.top/skill/zalogarcia/leash/) |
| [zertac/TeleClaude](https://github.com/zertac/TeleClaude) | 5 | A Windows Telegram bot for Claude CLI. Control Claude remotely via Telegram with conversation persistence, working directory management, file transfe… | [SAFE](https://agentskillshub.top/skill/zertac/TeleClaude/) |

<a id="type-framework"></a>
## 🧱 Frameworks & MCP

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-framework)

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [aiogram/aiogram](https://github.com/aiogram/aiogram) | 5.9k | aiogram is a modern and fully asynchronous framework for Telegram Bot API written in Python using asyncio | [SAFE](https://agentskillshub.top/skill/aiogram/aiogram/) |
| [chigwell/telegram-mcp](https://github.com/chigwell/telegram-mcp) | 2.0k | Telegram MCP server powered by Telethon to let MCP clients read chats, manage groups, and send/modify messages, media, contacts, and settings. | [SAFE](https://agentskillshub.top/skill/chigwell/telegram-mcp/) |
| [szastupov/aiotg](https://github.com/szastupov/aiotg) | 377 | Asynchronous Python library for building Telegram bots | [SAFE](https://agentskillshub.top/skill/szastupov/aiotg/) |
| [dryeab/mcp-telegram](https://github.com/dryeab/mcp-telegram) | 253 | MCP Server for Telegram | [SAFE](https://agentskillshub.top/skill/dryeab/mcp-telegram/) |
| [noXplode/aiogram_calendar](https://github.com/noXplode/aiogram_calendar) | 190 | Date Selection tool & Inline calendar for Aiogram telegram bots | [SAFE](https://agentskillshub.top/skill/noXplode/aiogram_calendar/) |
| [jossalgon/StableDiffusionTelegram](https://github.com/jossalgon/StableDiffusionTelegram) | 131 | StableDiffusionTelegram is a telegram bot that allows to generate images using the stable diffusion AI from a telegram bot, in a much more comfortabl… | [SAFE](https://agentskillshub.top/skill/jossalgon/StableDiffusionTelegram/) |
| [arturboyun/AiogramBotTemplate](https://github.com/arturboyun/AiogramBotTemplate) | 129 | This is a template for easy start of bot development for Telegram | [SAFE](https://agentskillshub.top/skill/arturboyun/AiogramBotTemplate/) |
| [BaggerFast/AiogramTemplate](https://github.com/BaggerFast/AiogramTemplate) | 114 | This is template for telegram bots by aiogram | [SAFE](https://agentskillshub.top/skill/BaggerFast/AiogramTemplate/) |
| [netbriler/aiogram-peewee-template](https://github.com/netbriler/aiogram-peewee-template) | 95 | Telegram Bot API template, with aiogram, peewee and docker | [SAFE](https://agentskillshub.top/skill/netbriler/aiogram-peewee-template/) |
| [andrew000/aiogram-template](https://github.com/andrew000/aiogram-template) | 90 | Telegram Bot Template. aiogram, i18n, SQLAlchemy+Alembic, PostgreSQL, Redis, Caddy Server, Docker, uv, FTL-Extract | [SAFE](https://agentskillshub.top/skill/andrew000/aiogram-template/) |
| [TamilBots/TamiliniMusic](https://github.com/TamilBots/TamiliniMusic) | 59 | A Free Open Source Group Music Voice Chat Bot Telegram.Give 🌟 And Fork This Repo Before Use ☺️ | [SAFE](https://agentskillshub.top/skill/TamilBots/TamiliniMusic/) |
| [realkarych/aioplate](https://github.com/realkarych/aioplate) | 56 | Template for creating Telegram bots on Python Aiogram | [SAFE](https://agentskillshub.top/skill/realkarych/aioplate/) |
| [leshchenko1979/fast-mcp-telegram](https://github.com/leshchenko1979/fast-mcp-telegram) | 50 | Telegram MCP gateway for AI agents: 8 tools, multi-tenant HTTP/stdio, MTProto | [SAFE](https://agentskillshub.top/skill/leshchenko1979/fast-mcp-telegram/) |
| [mamashin/tg-bot-fastapi-aiogram](https://github.com/mamashin/tg-bot-fastapi-aiogram) | 50 | FastAPI & Aiogram Telegram Bot Template | [SAFE](https://agentskillshub.top/skill/mamashin/tg-bot-fastapi-aiogram/) |
| [nessshon/aiogram-tonconnect](https://github.com/nessshon/aiogram-tonconnect) | 49 | aiogram-tonconnect is a user-friendly library for integrating TON Connect UI into aiogram-based Telegram bots. | [SAFE](https://agentskillshub.top/skill/nessshon/aiogram-tonconnect/) |
| [qpd-v/mcp-communicator-telegram](https://github.com/qpd-v/mcp-communicator-telegram) | 47 | An MCP server that enables communication with users through Telegram. This server provides a tool to ask questions to users and receive their respons… | [SAFE](https://agentskillshub.top/skill/qpd-v/mcp-communicator-telegram/) |
| [ifokeev/telegram-ai-agent](https://github.com/ifokeev/telegram-ai-agent) | 46 | Telegram AI Agent: A powerful Python library for creating AI-powered Telegram bots | [SAFE](https://agentskillshub.top/skill/ifokeev/telegram-ai-agent/) |
| [coderroleggg/telegram-bot-mcp](https://github.com/coderroleggg/telegram-bot-mcp) | 37 | Telegram Bot MCP | [SAFE](https://agentskillshub.top/skill/coderroleggg/telegram-bot-mcp/) |
| [serejaris/telegram-skills](https://github.com/serejaris/telegram-skills) | 37 | Telegram skills for AI agents (Claude Code, Codex, Cursor): Agent Skills that teach your agent the Telegram Bot API. Rich Messages, streaming AI repl… | [SAFE](https://agentskillshub.top/skill/serejaris/telegram-skills/) |
| [timoncool/telegram-api-mcp](https://github.com/timoncool/telegram-api-mcp) | 34 | Ultimate Telegram Bot API MCP server — full v9.6 coverage, meta-mode, rate limiting, circuit breaker. TypeScript. | [SAFE](https://agentskillshub.top/skill/timoncool/telegram-api-mcp/) |
| [EvilFreelancer/tgfake](https://github.com/EvilFreelancer/tgfake) | 19 | Offline Telegram Bot API for testing bots, Mini Apps and LLM integrations. | [SAFE](https://agentskillshub.top/skill/EvilFreelancer/tgfake/) |
| [ProKaiiddo/BotAlto](https://github.com/ProKaiiddo/BotAlto) | 18 | BotAlto is an open-source platform for hosting and managing Telegram bots with a user-friendly dashboard. It allows you to create, manage, and deploy… | [SAFE](https://agentskillshub.top/skill/ProKaiiddo/BotAlto/) |
| [mcieric/telegram-ai-bot-template](https://github.com/mcieric/telegram-ai-bot-template) | 15 | A minimal AI-powered Telegram bot template using OpenAI 🤖 | [SAFE](https://agentskillshub.top/skill/mcieric/telegram-ai-bot-template/) |
| [TheOpenPrimary/giskard](https://github.com/TheOpenPrimary/giskard) | 11 | Open Source bot engine for Telegram bots and Facebook messenger bots | [SAFE](https://agentskillshub.top/skill/TheOpenPrimary/giskard/) |
| [maratx86/aiogram-timepicker](https://github.com/maratx86/aiogram-timepicker) | 11 | A simple inline time selection tool for aiogram telegram bots written in Python. | [SAFE](https://agentskillshub.top/skill/maratx86/aiogram-timepicker/) |
| [BrainDAO/mcp-telegram](https://github.com/BrainDAO/mcp-telegram) | 8 | Model Context Protocol Server for interacting with Telegram Channels | [SAFE](https://agentskillshub.top/skill/BrainDAO/mcp-telegram/) |
| [habitual69/cutimagebg_bot](https://github.com/habitual69/cutimagebg_bot) | 7 | Background Remover Bot. A Telegram bot that uses AI image processing to remove the background from images. | [SAFE](https://agentskillshub.top/skill/habitual69/cutimagebg_bot/) |
| [pengming273/TelegramAirdropBountyBot](https://github.com/pengming273/TelegramAirdropBountyBot) | 7 | TelegramAirdropBountyBot | [SAFE](https://agentskillshub.top/skill/pengming273/TelegramAirdropBountyBot/) |
| [abbosahmad/telegram-premium-emojis](https://github.com/abbosahmad/telegram-premium-emojis) | 6 | The complete toolkit & AI Agent Skill for Telegram Bot Premium Custom Emojis, Aiogram 3 card UI, inline button custom emoji icons, and pack scanning. | [SAFE](https://agentskillshub.top/skill/abbosahmad/telegram-premium-emojis/) |
| [TgCaller/TgCaller](https://github.com/TgCaller/TgCaller) | 5 | An open-source library to handle high-quality group calls in Telegram bots. | [SAFE](https://agentskillshub.top/skill/TgCaller/TgCaller/) |
| [azdaev/tgmock](https://github.com/azdaev/tgmock) | 5 | Fake Telegram API server for testing bots — pytest plugin + Claude Code MCP server | [SAFE](https://agentskillshub.top/skill/azdaev/tgmock/) |
| [skrashevich/telegram-mock-ai](https://github.com/skrashevich/telegram-mock-ai) | 5 | Mock Telegram Bot API server with LLM-generated responses | [SAFE](https://agentskillshub.top/skill/skrashevich/telegram-mock-ai/) |
| [andrebuilds/hermes](https://github.com/andrebuilds/hermes) | 2 | Send messages from AI agents, CLI, and MCP tools - powered by one shared TypeScript core. | [SAFE](https://agentskillshub.top/skill/andrebuilds/hermes/) |

<a id="type-utility"></a>
## 🧰 Utility bots

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-utility)

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [groupultra/telegram-search](https://github.com/groupultra/telegram-search) | 4.2k | 🔍 导出并模糊搜索 Telegram 聊天记录 \| Export and fuzzy search your Telegram chat history | [SAFE](https://agentskillshub.top/skill/groupultra/telegram-search/) |
| [SpEcHiDe/AnyDLBot](https://github.com/SpEcHiDe/AnyDLBot) | 397 | An Open Source GPLv3 All-In-One Telegram Bot | [SAFE](https://agentskillshub.top/skill/SpEcHiDe/AnyDLBot/) |
| [patheticGeek/torrent-aio-bot](https://github.com/patheticGeek/torrent-aio-bot) | 328 | A bot for searching and downloading torrents easily with website and telegram bot | [SAFE](https://agentskillshub.top/skill/patheticGeek/torrent-aio-bot/) |
| [Priler/samurai](https://github.com/Priler/samurai) | 306 | Simple, yet effective auto-moderator bot for Telegram. With reports, logs, profanity filter, anti-spam AI, NSFW detection AI and more :3 | [SAFE](https://agentskillshub.top/skill/Priler/samurai/) |
| [fabston/Telegram-Airdrop-Bot](https://github.com/fabston/Telegram-Airdrop-Bot) | 215 | 🎈 Manage your Telegram Airdrops on ERC-20, BEP-20 etc. tokens. | [SAFE](https://agentskillshub.top/skill/fabston/Telegram-Airdrop-Bot/) |
| [akynazh/tg-search-bot](https://github.com/akynazh/tg-search-bot) | 204 | A smart AI telegram bot for searching and auto-saving. | [SAFE](https://agentskillshub.top/skill/akynazh/tg-search-bot/) |
| [TheCaduceus/FileStreamBot](https://github.com/TheCaduceus/FileStreamBot) | 134 | An open-source Python Telegram bot to transmit Telegram files over HTTP. | [CAUTION](https://agentskillshub.top/skill/TheCaduceus/FileStreamBot/) |
| [callsmusic/vcpb](https://github.com/callsmusic/vcpb) | 121 | [UNMAINTAINED] The first voice chat-related Telegram bot to be open-sourced. Uses MPV and has queue, stream & YouTube support. | [SAFE](https://agentskillshub.top/skill/callsmusic/vcpb/) |
| [noob-mukesh/MukeshRobot](https://github.com/noob-mukesh/MukeshRobot) | 116 | An open source telegram group management and ai bot written in python with the help of python-telegram-bot, telethon and pyrogram using sqlalchemy an… | [SAFE](https://agentskillshub.top/skill/noob-mukesh/MukeshRobot/) |
| [assimon/ai-anti-bot](https://github.com/assimon/ai-anti-bot) | 111 | AI-based anti-advertising robot for Telegram(基于AI的telegram反垃圾广告机器人) | [SAFE](https://agentskillshub.top/skill/assimon/ai-anti-bot/) |
| [joeseesun/AIGC_Telegram_Bot](https://github.com/joeseesun/AIGC_Telegram_Bot) | 103 | 编程新手用GPT4辅助开发的一个Telegram机器人，指定twitter ID，自动抓取推特消息并翻译成中文发给自己的Telegram账号。 | [SAFE](https://agentskillshub.top/skill/joeseesun/AIGC_Telegram_Bot/) |
| [ruitunion-org/feedback-bot](https://github.com/ruitunion-org/feedback-bot) | 67 | A free and open-source Telegram Bot that allows you to anonymously chat with multiple users in one Telegram Chat. | [SAFE](https://agentskillshub.top/skill/ruitunion-org/feedback-bot/) |
| [vibe-with-me-tools/agent-reachout](https://github.com/vibe-with-me-tools/agent-reachout) | 58 | Let Claude Code reach you on Telegram when it finishes work or needs decisions | [SAFE](https://agentskillshub.top/skill/vibe-with-me-tools/agent-reachout/) |
| [gth-ai/reclip-telegram-bot](https://github.com/gth-ai/reclip-telegram-bot) | 56 | Self-hosted Telegram bot for downloading media from YouTube, TikTok, Instagram, and 1000+ sites. Powered by reclip + yt-dlp. | [SAFE](https://agentskillshub.top/skill/gth-ai/reclip-telegram-bot/) |
| [sliday/telegram-ai-digest](https://github.com/sliday/telegram-ai-digest) | 56 | Automates Telegram message digests using Claude AI for summaries and Replicate API for image generation, sending results to saved messages. | [SAFE](https://agentskillshub.top/skill/sliday/telegram-ai-digest/) |
| [matterai/DataKitsune](https://github.com/matterai/DataKitsune) | 55 | Introducing DataKitsune, an open-source Telegram bot designed to enhance the way you manage and retrieve links shared within your personal or group c… | [SAFE](https://agentskillshub.top/skill/matterai/DataKitsune/) |
| [LearningBotsOfficial/NomadeHelpBot](https://github.com/LearningBotsOfficial/NomadeHelpBot) | 54 | 🤖 Nomad — Advanced Telegram Group Manager Bot built with Pyrogram. Smart Anti-Spam, Adaptive Lock System, Inline UI, and full moderation suite. Open… | [CAUTION](https://agentskillshub.top/skill/LearningBotsOfficial/NomadeHelpBot/) |
| [Derrors/reelay](https://github.com/Derrors/reelay) | 38 | 自托管的 Telegram → 115 网盘自动转存：AI 识别分享链接，审批后转存并按 Jellyfin/Emby 规范整理入库 | [SAFE](https://agentskillshub.top/skill/Derrors/reelay/) |
| [AI-XMLY/nodeseek-rss-telegram-bot](https://github.com/AI-XMLY/nodeseek-rss-telegram-bot) | 26 | RSS to Telegram bot with keyword filtering, multi-user subscriptions, SQLite and Docker support | [SAFE](https://agentskillshub.top/skill/AI-XMLY/nodeseek-rss-telegram-bot/) |
| [belaytzev/Telebrief](https://github.com/belaytzev/Telebrief) | 26 | Personal digests from Telegram channels and chats: summarizes threads, extracts key points, and delivers a clean daily/weekly brief with links and co… | [SAFE](https://agentskillshub.top/skill/belaytzev/Telebrief/) |
| [kstonekuan/telegram-notification-mcp](https://github.com/kstonekuan/telegram-notification-mcp) | 22 | Simple MCP server to send you notifications on telegram | [SAFE](https://agentskillshub.top/skill/kstonekuan/telegram-notification-mcp/) |
| [bbharathbala/actual-budget-telegram-bot](https://github.com/bbharathbala/actual-budget-telegram-bot) | 18 | Telegram bot for household expense tracking with Actual Budget. No LLMs, no AI costs. Receipt scanning, auto-learning categories, tags, transfers, da… | [SAFE](https://agentskillshub.top/skill/bbharathbala/actual-budget-telegram-bot/) |
| [sean-nicholas/parrot](https://github.com/sean-nicholas/parrot) | 13 | Telegram Bot for transcribing voice messages via wit.ai | [SAFE](https://agentskillshub.top/skill/sean-nicholas/parrot/) |
| [AIOPrivacy/AIOPrivacyBot](https://github.com/AIOPrivacy/AIOPrivacyBot) | 12 | 一个尝试在保护用户隐私的前提下，提供各类功能的类命令行Telegram机器人。 | [SAFE](https://agentskillshub.top/skill/AIOPrivacy/AIOPrivacyBot/) |
| [abirxdhack/Chat-ID-Bot-Aio](https://github.com/abirxdhack/Chat-ID-Bot-Aio) | 12 | The Chat ID Bot Aiogram is a Telegram bot built with Python and the @aiogram library. It allows users to quickly retrieve the unique IDs of Telegram… | [SAFE](https://agentskillshub.top/skill/abirxdhack/Chat-ID-Bot-Aio/) |
| [kyujin-cho/claude-code-remote](https://github.com/kyujin-cho/claude-code-remote) | 10 | Claude Code hook & Telegram Bot to notify user about active CC permission request and receive the decision via Telegram bot. | [CAUTION](https://agentskillshub.top/skill/kyujin-cho/claude-code-remote/) |
| [1995parham/ELBoT](https://github.com/1995parham/ELBoT) | 9 | A personal Telegram secretary for people and AI agents: a user-mode MTProto client with an MCP server, several accounts, drafts, reminders, tags and… | [SAFE](https://agentskillshub.top/skill/1995parham/ELBoT/) |
| [Mr-SxR/Xmnit-range-forwarder-bot](https://github.com/Mr-SxR/Xmnit-range-forwarder-bot) | 9 | Telegram bot that polls a dashboard API and forwards OTP logs — Open Source \| Mr-SxR | [SAFE](https://agentskillshub.top/skill/Mr-SxR/Xmnit-range-forwarder-bot/) |
| [pabletos/Hubot-Warframe](https://github.com/pabletos/Hubot-Warframe) | 8 | A open source warframe bot for telegram | [SAFE](https://agentskillshub.top/skill/pabletos/Hubot-Warframe/) |
| [Kiryoko/claude-code-changelog-telegram-bot](https://github.com/Kiryoko/claude-code-changelog-telegram-bot) | 6 |  | [SAFE](https://agentskillshub.top/skill/Kiryoko/claude-code-changelog-telegram-bot/) |
| [xx0x0/video-transcript-bot](https://github.com/xx0x0/video-transcript-bot) | 6 | 电报视频文案提取机器人，抖音/X(Twitter)/YouTube/B站短视频转文字、字幕提取、语音转文字，本地 Whisper + AI 梳理全程离线跑在 Mac 无需上云 \| Telegram bot for short-video transcript & subtitle extract… | [SAFE](https://agentskillshub.top/skill/xx0x0/video-transcript-bot/) |
| [jielosc/EigenDigest_bot](https://github.com/jielosc/EigenDigest_bot) | 5 | Telegram 信息聚合机器人：定时从 RSS、新闻网站、微信公众号拉取内容，通过 LLM 生成摘要，每日推送。 | [SAFE](https://agentskillshub.top/skill/jielosc/EigenDigest_bot/) |
| [smurftyy/Whispr](https://github.com/smurftyy/Whispr) | 5 | AI-powered Telegram reminder bot — NLP scheduling via chrono-node, Bull/Redis queue system, and smart notification management. Live. | [CAUTION](https://agentskillshub.top/skill/smurftyy/Whispr/) |

<a id="type-fun"></a>
## 🎲 Fun & learning

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-fun)

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [lmcsu/qq-neural-anime-tg](https://github.com/lmcsu/qq-neural-anime-tg) | 144 | A Telegram bot that converts your photos to 2D anime art via the new AI made by QQ | [SAFE](https://agentskillshub.top/skill/lmcsu/qq-neural-anime-tg/) |
| [PythonHubStudio/aiogram-3-course-telegram-bot](https://github.com/PythonHubStudio/aiogram-3-course-telegram-bot) | 128 |  | [SAFE](https://agentskillshub.top/skill/PythonHubStudio/aiogram-3-course-telegram-bot/) |
| [LlmKira/Alice](https://github.com/LlmKira/Alice) | 97 | ✨ An autonomous digital companion — pressure field engine + Telegram userbot / Infinite Axis Utility Systems | [CAUTION](https://agentskillshub.top/skill/LlmKira/Alice/) |
| [y9san9/prizebot](https://github.com/y9san9/prizebot) | 83 | Open source telegram bot to purely raffle prizes (giveaways) with random.org written in Kotlin | [SAFE](https://agentskillshub.top/skill/y9san9/prizebot/) |
| [turmyshevd/openclawgotchi](https://github.com/turmyshevd/openclawgotchi) | 53 | (▰˘◡˘▰) - AI Tamagotchi on Raspberry Pi. Agentic life-form with an E-Ink face | [SAFE](https://agentskillshub.top/skill/turmyshevd/openclawgotchi/) |
| [SWel1a/QuizBot](https://github.com/SWel1a/QuizBot) | 10 | Blossom the languagemaid is your personal language learning assistant on Telegram. | [SAFE](https://agentskillshub.top/skill/SWel1a/QuizBot/) |
| [radyakaze/teleduckai](https://github.com/radyakaze/teleduckai) | 5 | A fun and experimental Telegram bot built using Deno, powered by Duck.ai | [SAFE](https://agentskillshub.top/skill/radyakaze/teleduckai/) |

<a id="type-business"></a>
## 💼 Business

[Open this type on the live page, sorted by stars →](https://agentskillshub.top/best/telegram-bot/#type-business)

| Repo | Stars | What it does | Security |
|---|---:|---|---|
| [KEV0143/Telegram-MedicalBot](https://github.com/KEV0143/Telegram-MedicalBot) | 2.1k | Система поддержки пользователей в Telegram: обработка пользовательских вопросов через тикет-систему и генерация ответов оператору как на основе базы… | [SAFE](https://agentskillshub.top/skill/KEV0143/Telegram-MedicalBot/) |
| [MiHaKun/Telegram-interactive-bot](https://github.com/MiHaKun/Telegram-interactive-bot) | 368 | Telegram(电报/纸飞机)的开源双向机器人（客服机器人？）。避免垃圾信息；让被限制的客户可以顺利联系到你；支持后台分组，算是一个简易的CRM系统。Open-source interactive bot on Telegram. Avoid spam messages; allow restr… | [SAFE](https://agentskillshub.top/skill/MiHaKun/Telegram-interactive-bot/) |
| [ilyarolf/AiogramShopBot](https://github.com/ilyarolf/AiogramShopBot) | 253 | Open-source Telegram e-commerce bot built with Aiogram 3 for selling digital and physical goods with crypto payments and referral system. | [SAFE](https://agentskillshub.top/skill/ilyarolf/AiogramShopBot/) |
| [uerax/all-in-one-bot](https://github.com/uerax/all-in-one-bot) | 187 | A Telegram-based DeFi tool for real-time on-chain data analysis, smart money tracking, and automated trade monitoring. Empowering users with open-sou… | [CAUTION](https://agentskillshub.top/skill/uerax/all-in-one-bot/) |
| [trizin/Telegram-Airdrop-Bot](https://github.com/trizin/Telegram-Airdrop-Bot) | 133 | Very simple telegram airdrop bot | [SAFE](https://agentskillshub.top/skill/trizin/Telegram-Airdrop-Bot/) |
| [ButaiKirin/MaiMaiBot](https://github.com/ButaiKirin/MaiMaiBot) | 128 | A Telegram bot that calls the McDonald's MCP tools via Streamable HTTP. | [CAUTION](https://agentskillshub.top/skill/ButaiKirin/MaiMaiBot/) |
| [bxdoan/airdrop-tools](https://github.com/bxdoan/airdrop-tools) | 109 | Airdrop tools for all telegram bot | [SAFE](https://agentskillshub.top/skill/bxdoan/airdrop-tools/) |
| [guccidgi/AI-Stock-Technical-Analysis-n8n-x-FlowiseAI](https://github.com/guccidgi/AI-Stock-Technical-Analysis-n8n-x-FlowiseAI) | 77 | AI-powered stock analysis system: Telegram bot triggers n8n workflows with FlowiseAI to generate technical analysis reports. Stores trading opportuni… | [SAFE](https://agentskillshub.top/skill/guccidgi/AI-Stock-Technical-Analysis-n8n-x-FlowiseAI/) |
| [kaiserern/Kaiser.charon](https://github.com/kaiserern/Kaiser.charon) | 77 | Solana pump.fun trading bot — Telegram-driven screening, strategy gates, LLM entry selection, Jupiter execution. Fork of yunus-0x/charon. | [CAUTION](https://agentskillshub.top/skill/kaiserern/Kaiser.charon/) |
| [FlipZ3ro/robinhood-lp-bot](https://github.com/FlipZ3ro/robinhood-lp-bot) | 69 | 🐷 Telegram-controlled LP bot for Robinhood Chain — auto liquidity on Uniswap v2/v3/v4 (incl. USDG pairs) via KyberSwap best-route, with real-time Nit… | [SAFE](https://agentskillshub.top/skill/FlipZ3ro/robinhood-lp-bot/) |
| [Opselon/ForexTradingBot](https://github.com/Opselon/ForexTradingBot) | 57 | ForexSignalBot is an advanced, AI-driven Telegram bot meticulously engineered for the Forex market. It delivers real-time, high-precision trading sig… | [CAUTION](https://agentskillshub.top/skill/Opselon/ForexTradingBot/) |
| [SergiySW/NanoWalletBot](https://github.com/SergiySW/NanoWalletBot) | 52 | [DISCONTINUED] Open source Telegram bot for Nano currency | [SAFE](https://agentskillshub.top/skill/SergiySW/NanoWalletBot/) |
| [Kingler16/Velora](https://github.com/Kingler16/Velora) | 49 | Your AI-powered personal wealth advisor. Automated portfolio monitoring, market analysis, and investment briefings delivered via Telegram. Runs on Cl… | [CAUTION](https://agentskillshub.top/skill/Kingler16/Velora/) |
| [JumpCodeFrog/telegram-shop-bot](https://github.com/JumpCodeFrog/telegram-shop-bot) | 24 | Open-source Telegram shop bot in Go — catalog, Stars & USDT payments, subscriptions, Mini App, admin panel · Telegram-магазин на Go — каталог, оплата… | [SAFE](https://agentskillshub.top/skill/JumpCodeFrog/telegram-shop-bot/) |
| [Awaisali36/stock-analysis-telegram-bot](https://github.com/Awaisali36/stock-analysis-telegram-bot) | 13 | 📈 Telegram bot that delivers comprehensive US stock analysis combining real-time technical data, AI-powered news sentiment, and fundamental metrics.… | [SAFE](https://agentskillshub.top/skill/Awaisali36/stock-analysis-telegram-bot/) |
| [UzStack/paycue](https://github.com/UzStack/paycue) | 12 | 💳 Telegram va Humo bot orqali to‘lovlarni avtomatlashtirishga mo‘ljallangan open-source servis — yuridik shaxssiz ham tez va oson integratsiyasiz to‘… | [CAUTION](https://agentskillshub.top/skill/UzStack/paycue/) |
| [TegroTON/ai-telegram-pay-miniapp](https://github.com/TegroTON/ai-telegram-pay-miniapp) | 10 | Tegro.Money fiat-onramp helper for Telegram bots — createOrder + webhook verifier, MIT-licensed, grammY example included. | [SAFE](https://agentskillshub.top/skill/TegroTON/ai-telegram-pay-miniapp/) |
| [BlackFoxGroup/smart-support-bot](https://github.com/BlackFoxGroup/smart-support-bot) | 9 | Smart Support Bot — open-source multilingual Telegram AI support bot | [SAFE](https://agentskillshub.top/skill/BlackFoxGroup/smart-support-bot/) |
| [omniores3/phpSearch](https://github.com/omniores3/phpSearch) | 9 | Telegram搜索引擎,TG机器人,群组索引,电报搜索,Bot开发,Elasticsearch PHP,广告投放,AI审核,Swoole高性能,Redis缓存,社群工具,运营系统,搭建教程,二次开发,中文搜索 | [SAFE](https://agentskillshub.top/skill/omniores3/phpSearch/) |
| [Theraf1u/vps-multitest-bot](https://github.com/Theraf1u/vps-multitest-bot) | 8 | Telegram-бот для диагностики VPS по SSH: 25 тестов (скорость, устойчивая нагрузка, UDP/QUIC-throttling, bufferbloat, IPv6, DNS-перехват, IP-репутация… | [CAUTION](https://agentskillshub.top/skill/Theraf1u/vps-multitest-bot/) |
| [Emadhabibnia1385/KasbBook](https://github.com/Emadhabibnia1385/KasbBook) | 7 | Bookkeeping for a small business, wherever it already talks — Telegram, Bale, Rubika, a web panel and an API. Jalali calendar, double-entry ledger, p… | [CAUTION](https://agentskillshub.top/skill/Emadhabibnia1385/KasbBook/) |
| [Arash-Mansourpour/ultimate-crypto-trading-bot](https://github.com/Arash-Mansourpour/ultimate-crypto-trading-bot) | 6 | An advanced Telegram bot for cryptocurrency trading analysis, featuring multi-source data fetching, technical indicators (Heiken Ashi, Ichimoku, Fibo… | [SAFE](https://agentskillshub.top/skill/Arash-Mansourpour/ultimate-crypto-trading-bot/) |
| [mmchougule/stealth-trader](https://github.com/mmchougule/stealth-trader) | 6 | Give your AI agent its own Solana wallet — it trades for you, and nothing traces back to it. MCP server + Telegram bot, open source. | [CAUTION](https://agentskillshub.top/skill/mmchougule/stealth-trader/) |
| [sideshift/saier](https://github.com/sideshift/saier) | 6 | Cryptocurrency tipping bot for Telegram powered by SideShift.ai | [SAFE](https://agentskillshub.top/skill/sideshift/saier/) |
| [Kpavan63/telegram-bot-dash](https://github.com/Kpavan63/telegram-bot-dash) | 5 | 🤖 Welcome to AI Products Bot! 🤖 🌟 Your AI-powered shopping assistant! Find the latest Products From Amazon,Flipkart,Meesho 🔍 Search AI Products: Type… | [SAFE](https://agentskillshub.top/skill/Kpavan63/telegram-bot-dash/) |
| [zooddd/tg-proxy-shop](https://github.com/zooddd/tg-proxy-shop) | 5 | 云海代理管理后台 YunHai Proxy Admin：开源 Telegram 代理自动售卖与多节点管理平台。机器人自助购买，SSH/Agent 自动部署 MTProto/SOCKS5 实例，Web 后台统一管理节点、套餐、用户、订单、代理与支付，含多渠道收款、全量审计与登录风控。An open-… | [SAFE](https://agentskillshub.top/skill/zooddd/tg-proxy-shop/) |

**Security** is the grade of the repo's README and install steps on Agent Skills Hub. *pending* means the catalog has not graded it yet.

Preview images are reduced copies of pictures from each project's own README, included only for projects under a permissive license. Sources and licenses: [assets/previews/NOTICE.md](assets/previews/NOTICE.md). Open an issue to have one removed.

## Related collections

- [zhuyansen/awesome-claude-video-skills](https://github.com/zhuyansen/awesome-claude-video-skills), [zhuyansen/awesome-codex-ppt-skills](https://github.com/zhuyansen/awesome-codex-ppt-skills) — lists built the same way.

## Add a repo

Open an issue with the GitHub URL. It goes through the same review as every entry; the rules above decide, stars do not.

---

Machine-readable copy: [`data/skills.json`](data/skills.json). Generated 2026-11-13.
