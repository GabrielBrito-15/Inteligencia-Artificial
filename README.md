# Inteligencia-Artificial
Assistente virtual 

import speech_recognition as sr
import pyttsx3
import datetime
import wikipedia
import pywhatkit



audio = sr.Recognizer()
maquina = pyttsx3.init()
maquina.say('Olá mestre Gabriel')
maquina.say('Como posso ajudar')
maquina.runAndWait()

    
def executa_comando():

    try:
        with sr.Microphone() as source:
                 print('Ouvindo..')
                 voz = audio.listen(source)
                 comando = audio.recognize_google(voz, language='pt-BR')
                 comando = comando.lower()       
                 if 'Éva' in comando:
                  comando = comando.replace('Éva', '')
                  maquina.say(comando)
                  maquina.runAndWait()           
    except:
        print('Microfone não está ok')
    return comando

def comando_voz_usuario():
    comando = executa_comando()
    if 'horas' in comando:
        hora = datetime.datetime.now().strftime(':%H %M')
        maquina.say('Agora são' + hora)
        maquina.runAndWait()                           
    if 'hoje' in comando:
        data_atual = datetime.datetime.now() 
        dia_atual = data_atual.strftime('%d/%m/%Y')
        print('Hoje é ' + dia_atual)
        maquina.say('Hoje é ' + dia_atual)
        maquina.runAndWait()                                                    
    elif 'procure por' in comando: 
        procurar = comando.replace('procure por', '')
        wikipedia.set_lang('pt')
        resultado = wikipedia.summary(procurar,2)
        print(resultado)
        maquina.say(resultado)
        maquina.runAndWait()     
    elif 'toque' in comando:
        musica = comando.replace('toque', '')
        resultado = pywhatkit.playonyt(musica)
        maquina.say('Tocando musica')
        maquina.runAndWait()    
        
comando_voz_usuario()
