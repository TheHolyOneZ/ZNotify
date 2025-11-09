# ZNotify
ZNotify is a feature-rich **Discord.py cog** developed for **ZygnalBot**, enabling keyword-triggered notifications with powerful customization and embedded message designs. Built for server automation, it lets administrators and authorized users configure, test, and style automated alert messages through an intuitive interactive hub.
> 💡 **Built for the Zygnal Ecosystem — to download and use this extension, you must be part of the Zygnal Ecosystem.**  
> This extension (cog) is part of the **Zygnal Ecosystem** and is only available through its supported platforms.  
> You can use it with:  
> - The **[Discord Bot Framework](https://github.com/TheHolyOneZ/discord-bot-framework)** — ideal for developers who want full control and flexibility *(includes an integrated extension marketplace)*, or  
> - The **[ZygnalBot](https://zygnalbot.de)** — a prebuilt, plug-and-play Discord bot *(also includes an integrated extension marketplace)*.  
>
> Browse and install extensions at [zygnalbot.com/extension](https://zygnalbot.com/extension).  
> For help or community discussions, join us on Discord: [discord.gg/sgZnXca5ts](https://discord.gg/sgZnXca5ts)

# 📬 ZNotify — Advanced Keyword Notification System for ZygnalBot

ZNotify is a feature-rich **Discord.py cog** developed for **ZygnalBot**, enabling keyword-triggered notifications with powerful customization and embedded message designs. Built for server automation, it lets administrators and authorized users configure, test, and style automated alert messages through an intuitive interactive hub.

> 🧾 **License Notice:**
> The full custom license agreement is located between **lines 16–100** in the source file `ZNotify.py`.
> Usage is subject to the terms defined by **TheHolyOneZ (TheZ)**.

---

## ⚙️ Overview

ZNotify provides a centralized interface — the **ZNotify Hub** — that allows guild administrators to:

* Create and manage keyword triggers.
* Assign roles that receive or trigger notifications.
* Test configurations safely.
* Customize embedded notifications with a design suite.
* Control permissions at a role level.

This cog ensures that keyword-triggered notifications are sent as **embeds via DM** to members of the configured notification role.

---

## 🚀 Commands (All hybrid)

### `/znotify` OR `!znotify`

**Description:** Opens the ZNotify interactive hub.

When executed, this command displays the **ZNotify Hub Embed** and a set of interactive buttons for navigation and configuration.

---

## 🧭 ZNotify Hub Interface

The hub is a dynamic, paginated Discord embed view using `discord.ui.View` components. Each page is tied to a specific function, and buttons or selects navigate between configuration areas.

### 🖼️ Embed Structure

Each embed in the hub follows a consistent format:

* **Title:** Context-dependent (e.g., Setup, Manage, Design Suite)
* **Description:** Overview of the current function
* **Fields:** Provide details, usage tips, and live statistics
* **Footer:** `Made By TheHolyOneZ / ZNotify`
* **Thumbnail:** Server icon (when available)

### 💠 Main Embed Fields

| Field              | Description                                                      |
| ------------------ | ---------------------------------------------------------------- |
| **📊 Statistics**  | Shows active keyword count, total recipients, and guild name     |
| **🔐 Your Access** | Displays user permissions based on roles or admin status         |
| **💡 Quick Guide** | Describes each feature: Setup, Manage, Test, Design, Permissions |

---

## 🔘 Buttons & Their Functions

### Main Navigation Buttons

| Button              | Emoji | Function                            |
| ------------------- | ----- | ----------------------------------- |
| **Setup Keywords**  | 🔧    | Create new keyword triggers         |
| **Manage Keywords** | 📋    | Edit or delete existing keywords    |
| **Test Keywords**   | 🧪    | Send simulated notifications        |
| **Design Suite**    | 🎨    | Customize embed appearance          |
| **Permissions**     | 🔐    | Manage who can access hub functions |

### Navigation Controls

| Button              | Emoji   | Description                                          |
| ------------------- | ------- | ---------------------------------------------------- |
| **Back**            | ◀️      | Returns to the main hub                              |
| **Next / Previous** | ➡️ / ⬅️ | Navigate paginated lists (e.g., keywords or designs) |

### Keyword Management

| Button                      | Emoji | Action                                                          |
| --------------------------- | ----- | --------------------------------------------------------------- |
| **Create Keyword**          | ➕     | Opens a modal to define keyword, trigger roles, and notify role |
| **Edit Settings**           | ✏️    | Opens a modal to modify existing keyword setup                  |
| **Delete**                  | 🗑️   | Removes keyword after confirmation                              |
| **Confirm Delete / Cancel** | ✓ / ✗ | Confirms or aborts deletion                                     |

### Design Suite

| Button                 | Emoji | Action                                                |
| ---------------------- | ----- | ----------------------------------------------------- |
| **Global Design**      | 🌐    | Customize the default embed for all notifications     |
| **Keyword Designs**    | 🔑    | Apply unique designs to selected keywords             |
| **Edit Global Design** | ✏️    | Opens modal for global embed customization            |
| **Reset to Default**   | 🔄    | Restores global design to factory defaults            |
| **Edit Selected**      | ✏️    | Modify the design of multiple keywords simultaneously |
| **Remove Design**      | 🗑️   | Revert selected keywords to global design             |

### Permissions

| Button           | Emoji | Function                                        |
| ---------------- | ----- | ----------------------------------------------- |
| **Setup Roles**  | ➕     | Defines roles allowed to create keywords        |
| **Manage Roles** | 📋    | Defines roles allowed to manage keywords        |
| **Test Roles**   | 🧪    | Defines roles allowed to run test notifications |

---

## 🧩 Modals (Forms)

ZNotify uses interactive **modals** (`discord.ui.Modal`) to collect input from users.

### SetupKeywordModal

Fields:

* **Keyword:** The trigger word/phrase (case-insensitive)
* **Trigger Role IDs:** Comma-separated IDs of roles allowed to trigger it (empty = admins only)
* **Notify Role ID:** Role to be notified via DM

### EditKeywordModal

Allows editing of an existing keyword's trigger and notify roles.

### GlobalDesignModal & KeywordDesignModal

Customize the visual design of notification embeds:

* **Title / Description:** Text templates supporting variables `{keyword}`, `{content}`, `{user}`, `{channel}`, `{server}`
* **Color (hex):** Embed color (e.g., `0x5865F2`)
* **Footer Text:** Optional footer text added before branding
* **Toggles:** Comma-separated list to control which fields appear (`triggered_by`, `channel`, `server`, `thumbnail`)

### PermissionModal

Used to assign role IDs for specific permissions (`setup_roles`, `manage_roles`, `test_roles`).

---

## 🎨 Design Suite Details

ZNotify offers two design customization levels:

### 🌐 Global Design

The base embed template applied to all keywords without a specific override.

### 🔑 Keyword-Specific Design

Customizes individual keywords with unique embeds. Supports multi-select editing.

### 🧩 Embed Variables

| Variable    | Description                    |
| ----------- | ------------------------------ |
| `{keyword}` | Triggered keyword              |
| `{content}` | Original message content       |
| `{user}`    | Mention of the triggering user |
| `{channel}` | Mention or name of the channel |
| `{server}`  | Server (guild) name            |

---

## 🧰 Data & File Structure

ZNotify creates structured directories in `data/znotify`:

```
data/znotify/
├── configs/        # Stores per-guild keyword configurations
├── permissions/    # Stores role-based permission settings
├── designs/        # Stores embed design templates
├── backups/        # Backup copies of modified files
```

Each configuration is JSON-based and safely written using atomic operations with automatic backup recovery.

---

## 🔐 Permissions System

ZNotify supports fine-grained role-based permissions. Default access:

* **Administrators** have full control.
* Other roles require explicit assignment through the Permissions menu.

| Permission       | Description                    |
| ---------------- | ------------------------------ |
| **setup_roles**  | Can create new keywords        |
| **manage_roles** | Can modify or delete keywords  |
| **test_roles**   | Can trigger test notifications |

---

## 📡 Notification Delivery

When a message contains a configured keyword:

1. The cog verifies whether the user is allowed to trigger notifications.
2. A DM embed is sent to all members of the assigned **Notify Role**.
3. The embed includes:

   * Title & description templates
   * Optional fields (Triggered By, Channel, Server)
   * A jump link to the original message
   * Branding footer: `Made By TheHolyOneZ / ZNotify`

---

## 🧪 Testing Notifications

Accessible via **Test Keywords** page in the hub.

* Sends simulated messages to all notify-role members.
* Uses the same design logic as live triggers.
* Ideal for verifying formatting, permissions, and delivery reliability.

---

## 💡 Use Cases

* Alert systems (e.g., announcements, updates, moderation)
* Event triggers for community management
* Keyword-based emergency or support pings
* Custom server automation for brand notifications

---

## 🧑‍💻 Developer Information

* **Cog Name:** `discord`
* **Built For:** ZygnalBot
* **Framework:** Discord.py
* **Developer:** TheHolyOneZ (TheZ)
* **License:** Custom License (Lines 16–100 in source)

---

## 🧱 Summary

| Feature          | Description                         |
| ---------------- | ----------------------------------- |
| Keyword Triggers | Custom words that send DM alerts    |
| Design Suite     | Embed customization for alerts      |
| Permission Roles | Controlled access for trusted roles |
| Interactive Hub  | Button & modal-based control system |
| Backup System    | Atomic saves with recovery options  |

---

### 🪪 Credits

Developed by **TheHolyOneZ (TheZ)**
Part of the **ZygnalBot Extension Suite**
All rights reserved under the **Custom License Agreement (lines 16–100)**.
