# Telethon

## Getting Started(开始)

### 简单安装:

```python
pip3 install telethon
```

### 创建一个客户端(client):

```python
from telethon import TelegramClient, sync

# These example values won't work. You must get your own api_id and
# api_hash from https://my.telegram.org, under API Development.
api_id = 12345
api_hash = '0123456789abcdef0123456789abcdef'

client = TelegramClient('session_name', api_id, api_hash).start()
```

### 基础操作：

```python
# 打印个人信息Getting information about yourself
me = client.get_me()
print(me.stringify())

# 发送消息给username Sending a message (you can use 'me' or 'self' to message yourself)
client.send_message('username', 'Hello World from Telethon!')

# 给username发送一个文件Sending a file
client.send_file('username', '/home/myself/Pictures/holidays.jpg')

# 接受一个消息 Retrieving messages from a chat
from telethon import utils
for message in client.iter_messages('username', limit=10):
    print(utils.get_display_name(message.sender), message.message)

# Listing all the dialogs (conversations you have open)
for dialog in client.get_dialogs(limit=10):
    print(dialog.name, dialog.draft.text)

# 下载username的头像 Downloading profile photos (default path is the working directory)
client.download_profile_photo('username')

# Once you have a message with .media (if message.media)
# you can download it using client.download_media(),
# or even using message.download_media():
messages = client.get_messages('username')
messages[0].download_media()
```

### 接收消息并回复

```python
from telethon import TelegramClient, events

client = TelegramClient('name', api_id, api_hash)

@client.on(events.NewMessage)
async def my_event_handler(event):
    if 'hello' in event.raw_text:
        await event.reply('hi!')

client.start()
client.run_until_disconnected()
```

