import tkinter as tk
import json
import requests
from bs4 import BeautifulSoup as soup  # HTML data structure
from urllib.request import urlopen as uReq  # Web client
import xlwt
from xlwt import Workbook
import requests

def website_exists(url):
    request = requests.get(url)
    if request.status_code == 200:
        return True
    else:
        False

def output_data(data):
    x = data[0]
    y = data[1]
    games = x[0][1:]
    points = x[2][3:]
    rebounds = x[4][3:]
    assists = x[6][3:]
    fg_perc = y[0][3:]
    x = "Games: " , games + '\nPoints: ' , points, '\nrebounds: ',rebounds, '\nAssists: ',assists, '\nField Goal %: ',fg_perc
    bar = map(str, x)
    final = ''.join(bar)
    label['text'] = final
    
    

def generate_url(player_name):
    player_name = player_name.split()
    first_name = player_name[0]
    last_name = player_name[1]
    c = 0
    url_link1 = "https://www.basketball-reference.com/players/" + str(last_name[0]).lower() + '/' + last_name.lower() + str(first_name[0:2]).lower() + '01.html'
    url_link = "https://www.basketball-reference.com/players/" + str(last_name[0]).lower() + '/' + last_name[:-2].lower() + str(first_name[0:2]).lower() + '01.html'
    url_link2 = "https://www.basketball-reference.com/players/" + str(last_name[0]).lower() + '/' + last_name[:-1].lower() + str(first_name[0:2]).lower() + '01.html'
    links = [url_link,url_link1]
    while True:
        if website_exists(links[c]) is True:
            url = links[c]
            uClient = uReq(url)
            break
        else:
            c+=1
            if c is 2:
                label['text'] = 'Player must be active'
                return
                
    page = soup(uClient.read(), "html.parser")
    uClient.close()
   
    summary_container =  page.findAll("div", {"class":"p1" })
    for i in summary_container:
        x = i.get_text()
        x = x.split()
    summary_container1 =  page.findAll("div", {"class":"p2" })
    for a in summary_container1:
        y = a.get_text()
        y = y.split()
    output_data([x,y])




window = tk.Tk()

window.title("Welcome to the NBA directory!")

window.geometry('500x500')


entry = tk.Entry(window, font = 40)
entry.place(relwidth = .4,relheight = .1,relx = .3,rely=.1)

button = tk.Button(window, text= 'Enter Player name:',command = lambda:generate_url(entry.get()))
button.place(relwidth = .3,relheight = .2,relx = .3,rely = .2)

lower_frame = tk.Frame(window, bg='#80c1ff', bd=10)
lower_frame.place(relx=0.5, rely=0.25, relwidth=0.75, relheight=0.6, anchor='n')

label = tk.Label(lower_frame)
label.place(relwidth=1, relheight=1)

window.mainloop()
