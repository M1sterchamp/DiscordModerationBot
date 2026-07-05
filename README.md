Modular Discord Moderation Framework

A professional-grade, white-label Discord bot framework built for high-performance moderation, comprehensive audit logging, and automated security. This bot is designed to be fully portable; all branding and logic can be adjusted through configuration files without touching the source code.

## 🚀 Quick Start Instructions

1.  **Install Node.js**: Ensure you have [Node.js 18.x or higher](https://nodejs.org/) installed on your system.
2.  **Environment Setup**: 
    - Rename the `.env.example` file to `.env`.
    - Fill in your `DISCORD_TOKEN`, `CLIENT_ID` (The Bot's ID), and `GUILD_ID` (Your Server's ID).
3.  **Install Dependencies**:
    Open your terminal in the bot folder and run:
    ```bash
    npm install
    ```
4.  **Configure The Bot**: Follow the **Configuration Guide** below to set up your channels and roles.
5.  **Initialize Data**: Ensure the `data/` folder exists and contains `punishment-history.json` and `banned-words.json` (both initialized as `[]`).
6.  **Launch**:
    ```bash
    npm start
    ```

---

## ⚙️ Configuration Guide

All customization is done within the `config/` folder. The bot will check for these files on startup and will not run if any are missing.

### 1. `branding.json`
*Defines the visual identity of the bot.*
- `footerText`: The text appearing at the bottom of every embed.
- `footerIcon`: A direct URL to your server or bot logo.
- `embedColor`: The default hex color for logs and general embeds.
- `modColor`: The hex color used for successful moderation actions.
- `errorColor`: The hex color used for bans and errors.

### 2. `logging.json`
*Routes audit events to specific channels.*
- Enter the **Channel IDs** for each category. 
- Categories include: `mod`, `members`, `messages`, `voice`, `actions`, `files`, `roles`, and `channels`.

### 3. `permissions.json`
*Controls who can use the bot.*
- Add the **Role IDs** of your staff members to the corresponding arrays.
- Users with the **Administrator** permission bypass these role checks automatically.

### 4. `welcome.json`
*Configures the join message system.*
- `welcomeChannelId`: The channel where new members are announced.
- `aboutSection`: An array of strings. Each item in the array is a new paragraph in the "About Us" section of the embed.
- `links`: An array of objects containing `label` and `url`. The bot will automatically create clickable buttons (up to 5) below the welcome embed.

### 5. `honeypot.json` & `honeypot-embed.json`
*Automated security trap.*
- `honeypotChannelId`: The ID of the restricted channel.
- `safeRoles`: Role IDs (Staff) that will receive a **Timeout** instead of a **Ban** if they type in the channel.
- `honeypot-embed.json`: Set the Title, Description, and Banner for the warning post.

---

## 🛠️ Commands & Usage

### Slash Commands (`/`)
- `/kick`, `/ban`, `/unban`, `/mute`, `/unmute`: Core moderation tools.
- `/purge [amount]`: Deletes messages manually. Bypasses the Discord 14-day limit, allowing you to clean old messages.
- `/history [user]`: Displays the last 10 moderation actions taken against a user.
- `/filter-add`, `/filter-remove`, `/filter-list`: Context-based banned word management.

### Text Commands (`!`)
- `!setup-honeypot`: Execute this in your trap channel to post the automated warning embed. The bot will delete your command message instantly to keep the channel clean.

---

## 📂 Project Architecture

- **`commands/`**: Subfolders for Slash (`moderation/`) and Text (`text/`) commands.
  - `utilities/`: Contains `log-manager.js` (Central logging brain) and `mod-utils.js` (Permission logic).
- **`events/`**:
  - `logs/`: Individual logic files for `messageLogs`, `voiceLogs`, `roleLogs`, etc.
  - `welcome.js`: The dynamic welcome message builder.
  - `honeypot.js`: The automated trap listener.
- **`data/`**: JSON files for persistent storage of punishments and the word filter.

---

## 🛡️ Role Hierarchy Warning
For the moderation tools and the Honeypot trap to function, the **Bot's highest role must be placed above the members it is moderating** in your Server Settings. The bot cannot moderate users who have a higher role than itself.

---
*Developed by Misterchamp.*
