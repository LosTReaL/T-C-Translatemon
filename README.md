# Privacy Policy for the Translation Bot

This Privacy Policy provides a comprehensive explanation of how **this Translation Bot** collects, uses, processes, and stores user data. By using this bot, users indicate their understanding and acceptance of the practices and terms described herein. Protecting user privacy and ensuring robust data security are primary objectives. This policy aims to offer full transparency regarding every aspect of data handling in connection with the bot.

---

## 1. Data Stored & Purpose

All information handled by the Translation Bot is categorized as either **persistent** (long-term, saved in the database) or **temporary** (short-term, held in runtime memory).

### A. Persistently Stored Data (Database Storage)

Persistent data is stored within a secure database to ensure the bot can reliably tailor its functions and settings across sessions—even if the bot is restarted or updated. This data is essential for users to benefit from customized features and a consistent bot experience.

#### Data Types and Details

- **Chat ID**  
  - *What is it?*  
    A unique, numerical identifier assigned by Telegram for each private chat or group where the bot is used.
  - *Purpose*:  
    Serves as the primary key for all chat-specific and user-specific configuration data; allows the bot to retrieve and apply the correct settings for each chat. Without the Chat ID, no contextual settings or features could function.
  - *Security*:  
    Only the minimum chat identifier necessary for bot operation is stored; not user names or message content.
  
- **Language & Mode Settings**  
  - *What is it?*  
    The collection of language preferences selected by the user or chat, such as language pairs for translation (e.g., English ↔️ Spanish) or single target language for "Force Translate" mode.
  - *Purpose*:  
    Ensures that the bot provides translations according to the selected configuration, allowing users to communicate efficiently in their preferred languages.
  - *Details*:  
    Includes the chosen input and output languages as well as any specific mode-related settings.

- **User Interface & Media Preferences**  
  - *What is it?*  
    User choices regarding how the bot behaves and interacts, including options like enabling the "🔄 Try Again" button (internal variable: `retranslate_button_enabled`), and auto-translation toggles for different media (e.g., `autotranslate_voice`, `autotranslate_video`, `autotranslate_photo`, and `autotranslate_document`).
  - *Purpose*:  
    Customizes the bot's responses and user interface according to each user or chat’s wishes, supporting preferences for media and retry features.

> **Important Notice:** The bot’s persistent database **never** stores message contents, captions, media files, or any user-provided content apart from configuration data described above. Only the minimum necessary information for operation (such as `chat_id` and settings) is retained.

---

### B. Temporarily Stored Data (In-Memory Storage)

Transitory data is held only in the bot’s memory during runtime. This data enables features that require limited, short-term retention of chat activity. All temporary data is volatile and is automatically deleted whenever the bot is restarted (e.g., for updates or system maintenance).

#### Temporary Data Types

- **Conversation History for Summaries**
  - *What is it?*  
    A dynamically maintained list of recent messages within a chat, including each sender’s first name, the message text, and timestamp.
  - *Usage*:  
    Required to generate chat summaries via the `/summarize` command by providing relevant conversational context.
  - *Retention & Customization*:  
    The number of stored messages is configurable by the bot owner. This list is continually refreshed and completely cleared upon every bot restart to ensure memory efficiency and privacy.

- **Original Text for Re-translation**
  - *What is it?*  
    Caches the original, untranslated text of a message to support the “🔄 Try Again” button.
  - *Usage*:  
    Allows users to reattempt translation with an alternate service by retrieving the original input via a unique session identifier (UUID).
  - *Retention & Deletion*:  
    This data is retained for a maximum of 24 hours and is also purged on every bot restart.

- **Message & Translation Mappings for Edits/Deletions**
  - *What is it?*  
    A mapping that links a user's original message ID to the bot's translation message ID. A reverse mapping is also stored, linking the bot's message ID back to the original user's message ID **and the original sender's User ID**.
  - *Usage*:  
    This mapping is essential for two key features: (1) allowing the bot to find and update its translation when you edit your message, and (2) allowing the bot to identify the correct messages for deletion when the `/deltrans` command is used. The stored `original_user_id` is used exclusively to verify that only the original sender or a group admin can authorize a deletion.
  - *Retention & Deletion*:  
    All mapping data is stored for a maximum of 24 hours and is also completely purged on every bot restart.

- **Extracted Media Text for Caption Edits**
  - *What is it?*  
    If you send a media file (image, audio, etc.) that the bot processes for text, that extracted text is cached temporarily.
  - *Usage*:  
    This allows the bot to efficiently update the translation if you edit the media's caption. By caching the text from the media, the bot avoids having to download and re-process the entire file again, making caption edits fast and resource-friendly.
  - *Retention & Deletion*:  
    This cache is also cleared after 24 hours and upon every bot restart.

---

## 2. Use of Third-Party Services

External APIs are employed to provide core functions such as translation, transcription, image-to-text, and summarization. Data transmission to these services is limited to what is necessary for the requested operation, and content is not stored beyond the processing request.

| Service | Data Sent | Purpose & Usage | Relevant Policy |
| :--- | :--- | :--- | :--- |
| **DeepL API** | Only the source text of messages explicitly flagged for translation. | Delivers high-quality, neural machine translations between languages (when selected as the active engine). | [DeepL Privacy Policy](https://www.deepl.com/privacy) |
| **Microsoft Azure Translator** | Only the source text of messages explicitly flagged for translation. | Delivers neural machine translations between a broad range of languages (when selected as the active engine). | [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement) |
| **Google Gemini API** | The text of messages, images (for optical character recognition), audio/video files (for transcription), documents requiring reading, and conversation history when `/summarize` is requested. | Provides fallback translations, speech-to-text transcription, image-to-text conversion, document content extraction, and chat summarization. | [Google Privacy Policy](https://policies.google.com/privacy) |

- The bot functions strictly as a conduit: input provided by users is forwarded to the designated API, and the response is used only to reply to the user’s request.

---

## 3. Data Explicitly Not Stored or Logged

For enhanced user privacy and transparency, the bot **never** stores the following in its **persistent database** or application logs:

- Telegram usernames or display names.
- User IDs, except temporarily in memory as described in Section 1B for the explicit purpose of checking `/deltrans` permissions.
- Profile pictures, user avatars, or any photos.
- The contents of messages, captions, photographs, audio recordings, videos, or any documents, apart from what is held temporarily in memory for specific features as described above.

---

## 4. User Data Rights & Deletion Controls

Complete user control over stored data is provided, both via explicit commands and through automatic triggers based on changes in bot participation.

| Scenario | Command / Event | Effect |
| :--- | :--- | :--- |
| **In Group Chats** | `/deactivate` (must be used by a group admin) | Permanently deletes all data and configuration associated with the group, including all settings and activation status. This action cannot be reversed. |
| **In Private Chats** | `/stop` | Instantly and permanently removes all user and chat-specific data from the bot database. This is irreversible. |
| **Deleting a Message** | `/deltrans` (reply to a msg or its translation) | Deletes the bot's translation. If the bot is a group admin with deletion rights, it will also delete the original message. This action is irreversible and can only be performed by the original sender or a group admin. |

In any of these scenarios, data for that specific chat or user is deleted beyond recovery, including all language, mode, and interface preferences.

---

## 5. Data Security Measures

To safeguard all user-associated data (both transient and persistent), the following security practices are observed:

- All communications between Telegram users and the bot are protected by **SSL/TLS encryption**, ensuring that data in transit cannot be easily intercepted or tampered with.
- Secret keys, API credentials, and other sensitive configuration information are **never** stored in the codebase; instead, they are kept securely as environment variables.
- **Log Sanitation:** Sensitive credentials, such as API keys, are rigorously masked in system logs to prevent accidental exposure. System logs used for maintenance and debugging (which may be forwarded to the bot administrator) are stripped of sensitive tokens.
- Database and application design follows industry best practices, including access control, least-privilege principles, and regular review of security configurations, to minimize risk of unauthorized data access or breaches.

---

## 6. Acceptance of Terms and Policy Updates

- **Use of the bot constitutes acceptance:**  
  Adding the bot to a chat, sending a message, or interacting in any way confirms acceptance of this privacy policy and its terms.
- **Policy Rejection:**  
  Users who do not agree with these terms should immediately discontinue use of the bot. This can be done by:
    - Issuing the `/stop` command in a private chat
    - Having a group administrator use the `/deactivate` command in a group

---

## 7. User Responsibility and Disclaimer

The use of this service is entirely at the user’s own discretion and responsibility. The creator, owner, and any affiliates of this bot expressly disclaim any responsibility or liability for any direct or indirect actions, consequences, or outcomes arising from the use of this service. By using this bot, users acknowledge and accept that any actions taken or decisions made based on information or outputs provided by the bot rest solely with the user. Users are strongly encouraged to review this privacy policy on a regular basis in order to remain informed of any updates, changes, or revisions.

---

*Last updated: December 2025*