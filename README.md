# bot.py
import telebot
from telebot.types import ReplyKeyboardMarkup, KeyboardButton

TOKEN = "123456789:AAF1b2C3d4E5f6G7h8I9j0KLMnopqrstuvwxyz"  # ← o'zingiznikini qo'ying!

bot = telebot.TeleBot(TOKEN)

# Tugmalar yaratamiz
def main_menu():
    markup = ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add(KeyboardButton("Salomlashish"), KeyboardButton("Yordam"))
    return markup

@bot.message_handler(commands=['start'])
def start(message):
    bot.reply_to(message,
                 "Assalomu alaykum! Men GitHub'da yaratilgan oddiy botman 😄",
                 reply_markup=main_menu())

@bot.message_handler(func=lambda message: True)
def echo_all(message):
    text = message.text.lower()
    if "salom" in text or "salomlashish" in text:
        bot.reply_to(message, "Va alaykum assalom! Qalaysiz bugun?")
    elif "yordam" in text:
        bot.reply_to(message, "Hozircha faqat salomlashaman va yozganingizni qaytaraman 😅")
    else:
        bot.reply_to(message, f"Siz yozdingiz: {message.text}")

print("Bot ishga tushdi...")
bot.infinity_polling(allowed_updates=telebot.util.update_types)