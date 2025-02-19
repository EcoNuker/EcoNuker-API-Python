# EcoNuker's API Rewrite
EcoNuker is undergoing a major API rewrite, and as of this time, `EcoNuker.py` will not work.

# EcoNuker

EcoNuker is a Python library for interacting with the EcoNuker API, which provides routes for items, servers, and more!

PyPi: https://pypi.org/project/econuker/

## Installation

You can install the EcoNuker-API library using pip:

`pip install econuker`

## Usage

### Example

```python
# Python Example
from econuker import Client
beta = True # False
authtoken = None # "your auth token here"

if __name__ == "__main__":
    client = Client(auth_token=authtoken, beta=beta)
    status = client.status()
    print(status.name)
```

### Async Example
```python
# Python Async Example
from econuker import AsyncClient
beta = True # False
authtoken = None # "your auth token here"

if __name__ == "__main__":
    client = AsyncClient(auth_token=authtoken, beta=beta)
    async def asyncfunction():
        status = await client.status()
        print(status.name)
        return status
    asyncio.run(asyncfunction())
```

### Downtime Notifier Example
```python
# Python Downtime Notifier Example
import econuker
from econuker import AsyncClient
beta = True # get notified about downtime of our Beta bot.
authtoken = None

down = False

import guilded # pip install guilded.py
import asyncio
client = guilded.Client()
channelid = "" # the channel you want downtime notifications to be sent to! Make sure your bot has permissions.

async def monitorbot(client:AsyncClient):
    global down
    bot_name = await client.status().name
    while True:
        check = await client.ping()
        if not check:
            if not down:
                channel = await bot.fetch_channel(channelid)
                await channel.send(f'{bot_name} is down!')
                down = True
        if check and down:
            down = False
            channel = await bot.fetch_channel(channelid)
            await channel.send(f'{bot_name} is online!')
        await asyncio.sleep(10)

@bot.event
async def on_ready():
    print(f'Ready! Logged in as {bot.user.name}')
    try:
        client
    except:
        client = AsyncClient(beta=beta, auth_token=authtoken)
        bot.loop.create_task(monitorbot(client))

bot.run('guilded bot token here')
```


# Documentation
For detailed documentation on the EcoNuker API, read https://docs.econuker.xyz/

For detailed documentation on how to use the EcoNuker-API library, please wait while we write it lol.

# License
This project is licensed under the MIT License. See the LICENSE file for details.
