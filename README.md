# RPG---BotTelegram

from telegram.ext import Updater, CommandHandler
import telegram.update
import logging

TOKEN="Secret"

def start(update, context):
    s = "Maxwell is happy to see you!"
    update.message.reply_text(s)

def mostra_atributos(update, context):
    atributosTipo = ['Vitalidade','Inteligência','Lógica','Autocontrole','Força','Destreza','Agilidade','Vigor','Carisma']
    atributosValor =[0,1,2,3,4,5,6,7,8]
    arquivo = open("atributos.txt",'r')
    
    for i in range(0,9,1):
        valor=arquivo.readline()
        atributosValor[i]=valor

    s = "Seus atributos são\n"
    for i in range(0,9,1):
        s += "{} = {}".format(atributosTipo[i],atributosValor[i])
        
    update.message.reply_text(s)
    arquivo.close()

def altera_atributos(update,contextot):
    msg="Digite um numero"
    chat_id=telegram.message
    s = chat_id

    update.message.reply_text(s)

def main():
    logger = logging.getLogger(__name__)
    logging.basicConfig(level=logging.INFO,
                        format="%(asctime)s [%(levelname)s] %(message)s")

    updater = Updater(token=TOKEN, use_context=True)
    dp = updater.dispatcher

    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("mostrar", mostra_atributos))
    dp.add_handler(CommandHandler("alterar", altera_atributos))
    updater.start_polling()
    logging.info("=== Willian is awake ===")
    updater.idle()
    logging.info("=== Willin assleep ===")

if __name__ == "__main__":
    main()
