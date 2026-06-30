# -instagram-video-bot
async def download(update: Update, context: ContextTypes.DEFAULT_TYPE):
    url = update.message.text

    if "instagram.com" not in url:
        await update.message.reply_text("Instagram havolasini yuboring.")
        return

    await update.message.reply_text("⏳ Video yuklanmoqda...")

    ydl_opts = {
        "outtmpl": "video.%(ext)s"
    }

    try:
        with yt_dlp.YoutubeDL(ydl_opts) as ydl:
            info = ydl.extract_info(url, download=True)
            filename = ydl.prepare_filename(info)

        with open(filename, "rb") as video:
            await update.message.reply_video(video)

        os.remove(filename)

    except Exception:
        await update.message.reply_text("❌ Videoni yuklab bo‘lmadi.")


app = Application.builder().token(TOKEN).build()
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, download))

print("Bot ishga tushdi")
app.run_polling()
from telegram import Update
from telegram.ext import Application, MessageHandler, filters, ContextTypes

TOKEN = "8237539576:AAEYtfer2m2DdFbLqGHj8nBoZD4xlFlJ5w"

async def download(update: Update, context: ContextTypes.DEFAULT_TYPE):
url = update.message.text

if "instagram.com" not in url:  
    await update.message.reply_text("Instagram link yuboring.")  
    return  

await update.message.reply_text("⏳ Yuklanmoqda...")  

try:  
    await update.message.reply_text("📥 Video olish funksiyasi ishlayapti (test).")  
except Exception:  
    await update.message.reply_text("❌ Xatolik chiqdi.")

app = Application.builder().token(TOKEN).build()
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, download))

print("Bot ishga tushdi")
app.run_polling()
