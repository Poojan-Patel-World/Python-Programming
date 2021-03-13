# Python-Programming
import datetime
import smtplib
import speech_recognition as sr
import pyttsx3
import webbrowser
import os
def speak(audio):
    engine=pyttsx3.init("sapi5")
    voices=engine.getProperty("voices")
    engine.setProperty("voice",voices[0].id)
    engine.say(audio)
    engine.runAndWait()
def wish():
    hour=int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning Sir")
    elif hour>=12 and hour<18:
        speak("Good Afternoon sir")
    else:
        speak("Good Morning")
r=sr.Recognizer()
def take_command():
    with sr.Microphone() as source:
        print("Listening")
        r.pause_threshold=0.8
        r.energy_threshold=200
        audio=r.listen(source)
        try:
            print("Recognizing sir...")
            text=r.recognize_google(audio,language="en-in")
            print(f"You said:{text}")
            return text
        except Exception as e:
            print(e)
            speak("Unable to recognise it please speak it again")
            return "None"

if __name__=="__main__":
    wish()
    speak("I am Poojan and I am your assistant what I can do for you")
    
    while True:
        query=take_command().lower()

        if "time" in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            print(f"Sir the time is {strTime}")
        elif "open google" in query:
            webbrowser.open("google.com")
        elif "open youtube" in query:
            webbrowser.open("youtube.com")
        elif "open notepad" in query:
            os.startfile("C:\\Windows\\system32\\notepad.exe")
        elif "open spotify" in query:
            os.open("C:\\Users\\DELL\\AppData\\Roaming\\Spotify\\Spotify.exe")
        elif "send email" in query:
            try:
                server=smtplib.SMTP("smtp.gmail.com",587)
                server.ehlo()
                server.starttls()
                server.login("poojanpatel02112002@gmail.com","Poojan@123")
                speak("What should I write in subject")
                subject=take_command()
                if subject !="None":
                    speak("What should I write in main body")
                    body=take_command()
                    if body !="None":
                        message=f"Subject:{subject}\n\n{body}"
                        server.sendmail("poojanpatel02112002@gmail.com","nilampoojan@gmail.com",message)
                        speak("Mail sended successfully sir")
                        server.quit()
            except Exception as e:
                print(e)
        elif "sleep" in query:
            speak("Thank you sir for giving me time")
            break
        elif "open code" in query:
            os.startfile("C:\\Users\\DELL\\AppData\\Local\Programs\\Microsoft VS Code\\Code.exe")
        elif "how are you" in query:
            speak("I am good what about you")
            c=take_command().lower()
            if "good" in c:
                speak("That great sir, how may I help you")
            else:
                speak("Dont worry sir I will always ready to help you")

