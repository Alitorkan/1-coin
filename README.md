from telegram import Update
from telegram.ext import Application, CommandHandler, CallbackContext
import os
import logging
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()

# Enable logging
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    level=logging.INFO
)
logger = logging.getLogger(name)

# Load your bot token directly
TOKEN = '7347215805:AAHhTPY4jXEJR4EIXTyfA_mLVVxfJZtnjo-s'

if not TOKEN:
    logger.error("No token found! Please set the TOKEN environment variable.")
    exit(1)

# Start function
def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('سلام! به ایردارپ ما خوش آمدید.')

# Airdrop function
def airdrop(update: Update, context: CallbackContext) -> None:
    user = update.message.from_user
    update.message.reply_text(f'تبریک {user.first_name}! شما در ایردارپ شرکت کردید.')

def main() -> None:
    # Create the Application and bot
    application = Application.builder().token(TOKEN).build()

    # Command handlers
    application.add_handler(CommandHandler("start", start))
    application.add_handler(CommandHandler("airdrop", airdrop))

    # Start the bot
    application.run_polling()

if name == 'main':
    main()
