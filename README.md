import telebot

TOKEN = '8075470797:AAES20Gys0J72mMqeAfEc0gi8jfy7FoV5Sw'
bot = telebot.TeleBot(TOKEN)

@bot.message_handler(func=lambda message: True)
def echo_all(message):
    bot.reply_to(message, f"شما گفتید: {message.text}")

bot.polling()
