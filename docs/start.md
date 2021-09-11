## No começo, é só /start

O bot mais simples vai dar uma única resposta quando receber um comando */start*

Antes de iniciar a programação, você deve criar o bot. No Telegram, isso é feito conversando com o *BotFather*.

Lá, use */newbot*. Dê um nome e um nome de usuário. Aí seu bot já estará vivo. 

O mais importante é guardar o token de acesso. Qualquer um que tenha esse token pode controlar seu bot.

Criei. E agora?

Agora vamos usar uma API, uma interface HTTP para fazer a interação. A API está disponível em várias linguagens, como PHP, Node.js, Java. Aqui vamos usar Python.

https://github.com/python-telegram-bot/python-telegram-bot

Para instalar, é só usar `pip`, mas recomendo que você crie um ambiente virtual separado (*venv*). Então, faça assim:

Se você não tiver o *venv* instalado, `sudo apt install python3-venv`

```bash
python -m venv  venv
source venv/bin/activate
pip install python-telegram-bot
pip install configparser # para deixar o token em um arquivo separado
```

Agora vamos criar o Updater. Eu recomendo deixar o token em um arquivo separado.

```python
import configparser

config = configparser.ConfigParser()
config.read('token.ini') #Token is in a separate ini file

from telegram.ext import Updater
updater = Updater(token=config['TELEGRAM']['Token'], use_context=True)

dispatcher = updater.dispatcher
import logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

def start(update, context):
...     context.bot.send_message(chat_id=update.effective_chat.id, text="Oi! Me acordasse!")

from telegram.ext import CommandHandler
start_handler = CommandHandler('start', start)
dispatcher.add_handler(start_handler)

updater.start_polling()
```

(explicar os passos anteriores)