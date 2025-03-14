# Slack Message Backup Tool

![Slack API Status](https://img.shields.io/endpoint?url=https://status.slack.com/api/v2.0.0/current.json)

This Python script allows you to back up Slack messages (including public channels, private channels, direct messages, and group messages) to local Markdown files. It also supports downloading and organizing file attachments.

## Features

- Backs up messages from:
  - Public channels
  - Private channels
  - Direct messages (DMs)
  - Group messages (MPIMs)
- Saves messages in Markdown format with timestamps, reactions, and threads.
- Downloads file attachments and organizes them into folders.
- Handles file name conflicts by checking file content hashes.
- Supports selective backup of specific channels or users.

## Prerequisites

- Python 3.7 or higher.
- A Slack app with the necessary permissions and a User OAuth token.

## Setup

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/CafeAuLait-CC/Slack-Message-Backup.git
   cd Slack-Message-Backup
   ```

2. **Install Dependencies**:

   ```bash
   python3 -m venv ./slack_env
   source ./slack_env/bin/activate
   pip install -r requirements.txt
   ```

3. **Create a Slack App**:
   - Go to the [Slack API](https://api.slack.com/apps) and create a new app. See [this instruction](SlackAppSetup.md) for more details.
   - Install the app to your workspace and obtain the **User OAuth Token**.

4. **Edit the `config.txt` File**:
   Edit the `config.txt` file in the project directory with the following content:

   ```ini
   [Slack]
   User_OAuth_Token = xoxp-your-slack-user-oauth-token

   [Directories]
   Direct_Msg_Directory = dm
   Group_Msg_Directory = groups
   Channel_Msg_Directory = channels
   Attachment_Directory = attachments

   [Options]
   Backup_Attachments = True
   Backup_List = all
   ```

   Replace `xoxp-your-slack-user-oauth-token` with your actual Slack User OAuth token (the one starts with `xoxp`).

   You can choose whether or not you want to backup the attachments in the conversation, by setting the `Backup_Attachments` to `True` or `False`.

   The `Backup_List` could be `all` or a specific list of conversations you want to backup, e.g. `general, bob`, where `general` is the general channel and `bob` is the display name of a user in your workspace.

5. **Run the Script**:

   ```bash
   python slack_backup.py
   ```

   The script will back up messages and attachments to the specified directories.

## Configuration Options

### `config.txt`

- **`User_OAuth_Token`**: Your Slack user OAuth token.
- **`Direct_Msg_Directory`**: Directory to store direct messages (default: `dm`).
- **`Group_Msg_Directory`**: Directory to store group messages (default: `groups`).
- **`Channel_Msg_Directory`**: Directory to store channel messages (default: `channels`).
- **`Attachment_Directory`**: Directory to store downloaded attachments (default: `attachments`).
- **`Backup_Attachments`**: Whether to download attachments (default: `True`).
- **`Backup_List`**: List of specific channels or users to back up (default: `all`. E.g. `general, alice`, where `general` is the general channel and `alice` is the display name of a user in your workspace.).

## Output

- **Messages**: Saved as Markdown files in the respective directories (`dm`, `groups`, `channels`).
- **Attachments**: Downloaded to the `attachments` folder, organized by channel or user.

## Example Output

### Markdown File (`dm/alex.md`)

```markdown
#### 2023-10-10

**Alex** (12:34:56): Hello `@bob`, please check `@channel` for updates.

**Bob** (12:35:10): Got it!

_Reactions_: 👍 (x2), 😂 (x1)

[Attachment: Alex_image1.png](attachments/dm/Alex_image1.png)
```

### Attachments Folder

```
attachments/
├── dm/
│   ├── Alex_image1.png
│   └── Alex_image2.png
└── general/
    └── Team_image1.png
```

## Notes

- The script appends new messages to existing backup files, ensuring that edits and new messages are reflected.
- Files with the same content are not duplicated; instead, the existing file is reused.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgement

This project is generated by [DeepSeek-V3](www.deepseek.com).
