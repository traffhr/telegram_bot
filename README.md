[bot.py.py](https://github.com/user-attachments/files/28046934/bot.py.py)
import logging
from telegram import Update
from telegram.ext import ApplicationBuilder, MessageHandler, filters, ContextTypes

# ===== 8712840855:AAFcLpM0nknpRZ2gf9XnG4rDhHUOorbaYbM =====
BOT_TOKEN = "8712840855:AAFcLpM0nknpRZ2gf9XnG4rDhHUOorbaYbM"
# ===================================

# Множество пользователей, которым уже ответили
answered_users = set()

# Текст ответа бота
REPLY_TEXT = """👋 Привет! Рады, что ты откликнулся!

🏢 Мы — украинская рекрутинговая компания. Помогаем людям найти стабильную работу с достойной оплатой.

📍 *Локации:* Киев, Чернигов, Черногория

💼 *Формат работы:* Офис

💰 *Зарплата:*
• Старт — от $1000
• В среднем $2000–$3000 в месяц
• + еженедельные бонусы и плюшки 🎁

✅ *Что мы предлагаем:*
• Опыт не нужен — всему обучим
• Оплата переезда ✈️
• Жильё предоставляем 🏠

📚 Обучение проходит прямо на месте — с нуля до результата.

Напиши нам @Turbo_0115 и мы расскажем подробнее о вакансии, которая подойдёт именно тебе! 🚀"""

logging.basicConfig(level=logging.INFO)

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id

    # Отвечаем только на первое сообщение
    if user_id not in answered_users:
        answered_users.add(user_id)
        await update.message.reply_text(REPLY_TEXT, parse_mode="Markdown")

if __name__ == "__main__":
    app = ApplicationBuilder().token(BOT_TOKEN).build()
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
    print("Бот запущен ✅")
    app.run_polling()
[requirements.txt](https://github.com/user-attachments/files/28046946/requirements.txt)
python-telegram-bot==20.7
