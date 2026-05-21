# tic-tac-toe-game
import tkinter as tk
from tkinter import messagebox

gui=tk.Tk()
gui.geometry('500x500')
gui.title('Tic-Tac-Toe(x-o)')

player='X'
buttons=[]

#winner checker function
def check_winner():
    #rows
    for i in range(3):
        if buttons[i][0]['text']==buttons[i][1]['text']==buttons[i][2]['text']!='':
            return buttons[i][0]['text']
    #columns
    for i in range(3):
        if buttons[0][i]['text']==buttons[1][i]['text']==buttons[2][i]['text']!='':
            return buttons[0][i]['text']
    #diagonals
    if buttons[0][0]['text']==buttons[1][1]['text']==buttons[2][2]['text']!='':
        return buttons[0][0]['text']

    if buttons[0][2]['text']==buttons[1][1]['text']==buttons[2][0]['text']!='':
        return buttons[0][2]['text']
    return None
    
#game stopper function
def finish_game(winner):
    messagebox.showinfo('game ended',f'{winner} won')
    for row in buttons:
        for b in row:
            b.config(state='disabled')

#click
def click(button):
    global player
    if button['text']=='':
        button['text']=player
        winner=check_winner()
        if winner:
            finish_game(winner)
            return
        #change player
        player='O' if player=='X' else 'X'

#create buttons 
for i in range(3):
    row=[]
    for j in range(3):
        b=tk.Button(gui, text='',width=13,height=6,font=('Arial',15,'bold'))
        b.grid(row=i, column=j)
        b.config(command=lambda button=b: click(button))
        row.append(b)
    buttons.append(row)
gui.mainloop()
