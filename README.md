# Privacy Policy for the Translation Bot

This Privacy Policy explains how our **Translation Bot** collects, uses, and manages your data. By using this bot, you acknowledge and agree to the terms outlined in this document. Your privacy and data security are our top priorities, and we are committed to full transparency regarding our data handling practices.

---

## 1. Data We Store & Why

We categorize stored data into two types:  
- **Persistent Data** stored securely in our database  
- **Temporary Data** held transiently in the bot’s memory for specific functionalities

### A. Persistently Stored Data (In Our Database)

We save certain data permanently so that the bot can remember your preferences and function properly, even after restarts.

| Data Stored               | Purpose / Usage                                                    |
| -------------------------| ----------------------------------------------------------------- |
| **Chat ID**               | Numerical identifier for your Telegram private chat or group. This acts as the primary key enabling the bot to identify and apply your personalized settings. Without it, the bot would be unable to determine the language preferences or mode for your chat. |
| **Language & Mode Settings** | Includes your chosen language pairs (e.g., English to Spanish) and options such as “Force Translate.” These allow the bot to perform translations tailored to your chat’s requirements. |
| **User Interface & Media Preferences** | Settings like enabling/disabling the “🔄 Try Again” button (`retranslate_button_enabled`), and auto-translation preferences for media types such as voice notes, videos, photos, and documents (`autotranslate_voice`, etc.). These tailor the bot’s behavior to your preferences. |

> **Important:** We **never** store the actual content of your messages, photos, voice notes, or any media in our database. Only your `chat_id` and above-mentioned configuration settings are recorded.

---

### B. Temporarily Stored Data (In the Bot’s Memory)

This data is kept only briefly to enable advanced features. It is purely volatile and deleted permanently when the bot restarts (e.g., during maintenance or updates).

| Temporary Data                       | Purpose                                                             | Details                                          | Retention Period                                  |
|------------------------------------|--------------------------------------------------------------------|-------------------------------------------------|--------------------------------------------------|
| **Conversation History for Summaries** | Required for the `/summarize` command to generate summaries from recent chat | Stores a list of up to last 100 messages, including user's first name, message text, and timestamp | Continuously updated during runtime; **cleared completely on bot restart** |
| **Original Text for Re-translation** | Powers the “🔄 Try Again” feature by caching the original untranslated message for alternate translation calls | Temporarily caches only the original text of messages with retry requests | Automatically cleared after 24 hours or on bot restart |

---

## 2. How We Use Third-Party Services

The bot utilizes trusted, secure third-party APIs to provide features like translation, transcription, and summarization. Your content is sent **only** when required and processed securely.

| Service         | Data Sent                              | Purpose                                         | Privacy Link                                              |
|-----------------|--------------------------------------|------------------------------------------------|-----------------------------------------------------------|
| **DeepL API**   | Text content of the messages for translation | To deliver high-quality translations            | [DeepL Privacy Policy](https://www.deepl.com/privacy)     |
| **Google Gemini API** | Text messages, images (for OCR), audio/video (for transcription), documents, conversation logs (for summarization) | Applies fallback translations, speech-to-text, image-to-text, document reading, and summarization | [Google Privacy Policy](https://policies.google.com/privacy) |

- The bot simply acts as a secure conduit: it sends your content for processing and immediately forwards the response back to you.
- **No responses from these services are logged or stored** permanently by us.

---

## 3. Data We Explicitly DO NOT Store

To be absolutely clear, the bot **never** stores or logs the following:

- Your Telegram username, full name, or Telegram user ID (except briefly during initial activation, after which it is immediately discarded)
- Your profile pictures
- Actual message content, captions, photos, videos, or documents in the long-term database

---

## 4. Your Rights & How to Delete Your Data

You have complete control over your data and can delete it at any time:

| Context              | Data Deletion Command                      | Effect                                                            |
|----------------------|-------------------------------------------|------------------------------------------------------------------|
| **Group Chat**       | `/deactivate` (used by group admin)       | Instantly deletes all data linked to the group/chat, including your activation status and settings. This action is irreversible. |
| **Private Chat**     | `/stop`                                    | Permanently deletes all your data from our database. Irreversible.| 

Additional automated deletions occur:

- If the bot is removed from a group  
- If you block the bot

In those cases, your data associated with that chat is immediately and permanently erased.

---

## 5. Data Security

We implement multiple technical safeguards to protect your information:

- All communication between you and the bot is encrypted using **SSL/TLS** protocols.
- Sensitive keys and credentials are stored securely as environment variables, never hard-coded.
- We adhere to industry best practices for server, database, and application security to prevent unauthorized access.

---

## 6. Your Acceptance of This Policy

- **By using the bot**—adding it to your chat, messaging it, or interacting with it—you confirm that you have read, understood, and accepted this Privacy Policy.
- **If you do not agree** with the policy, your sole remedy is to immediately stop using the bot by:  
  - Using `/stop` in a private chat, or  
  - Having a group admin issue `/deactivate` in a group, or  
  - Removing (kicking) the bot from your group, or  
  - Blocking the bot.

---

Thank you for trusting our Translation Bot. We are committed to respecting your privacy and providing you with a transparent, secure experience.

---

*Last updated: July 2025*
