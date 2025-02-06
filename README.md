# voiced-based-email-for-blind
Design for model that gives an opportunity for the blind to send voice based emails  
def talk(text):
  engine.say(text)
  engine.runAndWait()


def get_info():
  with sr.Microphone() as source:
    print('listening...')
    r.adjust_for_ambient_noise(source)
    talk(text)
    voice = r.listen(source)
    try:
      info = r.recognize_google(voice)
      print(info)
      return info.lower()
    except:
        text= "sorry could not recognize what u said"
        talk(text)



def send_email():
  rec = "9921004629@klu.ac.in"
  text="please speak the body of the email"
  talk(text)
  msg=get_info()

  text="you have spoken the message"
  talk(text)
  talk(msg)
  server = smtplib.SMTP('smtp.gmail.com', 587)
  
  server.login(un,pwd)
  server.sendmail(un,rec,msg)
  server.quit()
  text="the email has been sent"
  text(talk)



def readmail():
    server= e.connect("imap.google.com",un,pwd)
    server.listids() #list of emailids in lifo order
    text="please say the serial number of the email u wanted to read"
    talk(text)
    a=get_info()
    if(a=='tu'):
      a="2"
    b=int(a)-1
    email=server.mail(server.listids()[b])
    text="the email is from :"
    talk(text)
    talk(email.fromn_addr)
    text="the subject of the email is:"
    talk(text)
    talk(email.title)
    text="the body of email iss"
    talk(text)
    talk(email.body)

text= "welcome to voice controlled email service"
talk(text)
while(1):
  text="what do u want to do?"
  talk(text)
  text=" speak SEND to send email   speak READ to read email   speak EXIT to exit"
  talk(text)
  ch=get_info()
  if (ch=='send'):
    text="you have decided to send an email"
    talk(text)
    send_email()
  elif(ch=='read'):
    text="you have chosen to read"
    talk(text)
    readmail()
  elif(ch=='exit'):
    text="you have chosen to exit. BYE have a beautiful day "
    talk(text)
    exit(1)
  else:
    text="u have said an invalid command"
    talk(text)
    talk(ch)
