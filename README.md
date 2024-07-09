import speech_recognition as sr
import pyttsx3
try:
    import pywhatkit
except:
    print("No internet connection")
import datetime
import wikipedia
import pyjokes
import webbrowser

listener = sr.Recognizer()
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(audio):
    engine.say(audio)
    engine.runAndWait()
def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        talk("Good Morning!")

    elif hour>=12 and hour<18:
        talk("Good Afternoon!")   

    else:
        talk("Good Evening!")  

    talk("Hi I am Fedora how may I help you")
wishMe()
def take_command():
    #It takes microphone input from the user and returns string output
    listener = sr.Recognizer()
    with sr.Microphone() as source:
        print('listening...')
        listener.pause_threshold=1
        voice = listener.listen(source)
    try:
        command = listener.recognize_google(voice,language='en_in')
        command = command.lower()
        print("User said:",command)
        if 'alexa' in command:
            command = command.replace('fedora', '')
            print(command)
    except:
        print("Say it again")   
    return command

try:
    def run_fedora():
        command = take_command()
        print(command) 
        if 'play' in command:
            song = command.replace('play', '')
            talk('playing ' + song)
            pywhatkit.playonyt(song)
        elif 'time' in command:
            time = datetime.datetime.now().strftime('%H:%M %p')
            talk('Current time is ' + time)
        elif 'tell me about' in command:
            person = command.replace('wikipedia', ' ')
            info = wikipedia.summary(command,sentences=1)
            print(info)
            talk("according to wikipedia")
            talk(info)
        elif 'date' in command:
            date = datetime.datetime.now().strftime('%d/%m/%Y')
            talk('Today\'s date is'+date)
            print(date)
            talk('Today\'s date is'+date)
        elif 'are you single' in command:
            talk('I am in relationship with wifi')
        elif 'how are you fedora' in command:
            talk('I am good what about you')
        
        elif 'i am getting bore' in command:
            talk('Do you need my help')
            if 'yes' in command:
                talk('waiting for your answer')
            else:
                talk("Please ask something else")
        elif 'joke' in command:
            jokes=pyjokes.get_joke()
            print(jokes)
            talk(jokes)
        elif 'open youtube' in command:
            webbrowser.open("youtube.com")
        elif 'open google' in command:
            webbrowser.open("google.com")
        elif 'open whatsapp' in command:
            webbrowser.open("whatsapp.com")
        elif'open instagram' in command:
            webbrowser.open("instagram.com")
        elif 'who is your creator' in command:
            talk('khushi')
        elif 'who is your favourite cricketer' in command:
            talk('Mahendra singh Dhoni')
        elif 'what will be the best place to visit in india' in command:
            talk("uttrakhand")
        else:
            talk('Please say the command again.')
except:
    pass

try:
    while True:
        run_fedora()
except:
    print("Please say the command again")
