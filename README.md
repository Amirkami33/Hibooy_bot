from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import ApplicationBuilder, CommandHandler, CallbackQueryHandler, ContextTypes

# توکن ربات
TOKEN = "7788726059:AAHnDiNODjkGtXB0ok3H2xwZtxc0-rCjmXo"

# لیست آهنگ‌ها
songs = [
    {"name": "مافیا - شایع", "file_url": "https://dl.sarzamindownload.com/music/Shayea-Mafia.mp3"},
    {"name": "ای کاش - محسن یگانه", "file_url": "https://dl.sarzaminmusic.ir/1401/Mohsen%20Yeganeh%20-%20Ey%20Kash.mp3"},
    {"name": "نگو نه - زدبازی", "file_url": "https://dl.behmelody.in/2023/12/Zedbazi-Nagoo-Nah-320.mp3"}
]

# هندلر /start
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    keyboard = [
        [InlineKeyboardButton(song["name"], callback_data=song["file_url"])]
        for song in songs
    ]
    reply_markup = InlineKeyboardMarkup(keyboard)
    await update.message.reply_text("سلام! یکی از آهنگ‌های زیر رو انتخاب کن:", reply_markup=reply_markup)

# هندلر انتخاب آهنگ
async def button_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    query = update.callback_query
    await query.answer()
    await query.message.reply_audio(audio=query.data)

# اجرای برنامه
app = ApplicationBuilder().token(TOKEN).build()
app.add_handler(CommandHandler("start", start))
app.add_handler(CallbackQueryHandler(button_handler))

print("ربات اجرا شد...")
app.run_polling()
