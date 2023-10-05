# MusicApp
A light web application of music which was created by using Python( tkinter &amp; pygame modules ) which provides a GUI attractive interface to the user to play, paused, or stop the music .


from tkinter import *
from PIL import Image,ImageTk
import tkinter.messagebox

from pygame import mixer
mixer.init()
class musicplayer:
    def __init__(self,Tk):
        self.root=Tk
        self.root.title('Music Player Sweta App')
        self.root.geometry('1255x944')
        self.root.configure(background='white')

        # Menu---
        self.menubar=Menu(self.root)
        self.root.configure(menu=self.menubar)

        self.submenu=Menu(self.menubar,tearoff=0)
        self.menubar.add_cascade(label='File',menu=self.submenu)
        self.submenu.add_command(label='Open')
        self.submenu.add_command(label='Exit',command=self.root.destroy)
        
        def About():
            tkinter.messagebox.showerror('About Us','Music Player created by Sweta Mishra date -28 september 2023 when I learn python and really I fall in love with python ')

         
        self.submenu2=Menu(self.menubar,tearoff=0)
        self.menubar.add_cascade(label='Help',menu=self.submenu2)
        #self.submenu2.add_command(label='Cut')
        self.submenu2.add_command(label='About',command=About)
        
        

        #adding  label---
        self.label=Label(text='Lets play the music and feel the love',bg='black',fg='white',font=22).place(x=10,y=10)
        
        #a\adding img---
        self.photo=ImageTk.PhotoImage(file='mainimg.png')
        photo=Label(self.root,image=self.photo,bg='white').place(x=109,y=106)

        #label--
        self.label1=Label(self.root,text='Lets play it.',bg='black',fg='white',font=22)
        self.label1.pack(side=BOTTOM,fill=X)

        #function---
        def playmusic():
            try:
                paused
            except NameError:
                try:
                    mixer.music.load('maan.mp3')
                    mixer.music.play()
                    #print('musicplaying')
                    self.label1['text']='Music_Playing..'
                except:
                    pass
            else:
                mixer.music.unpause()
                self.label1['text']='Music_Unpaused'

            
        #button--
        self.photo_B1=ImageTk.PhotoImage(file='playreal.png')
        photo_B1=Button(self.root,image=self.photo_B1,bd=0,bg='white',command=playmusic).place(x=154,y=92)
       
        def pausedmusic():
           global pausedmusic
           paused=True
           mixer.music.pause()
           self.label1['text']='Music_Playing..'
       
        #button--
        self.photo_B2=ImageTk.PhotoImage(file='pausereal.png')
        photo_B2=Button(self.root,image=self.photo_B2,bd=0,bg='white',command=pausedmusic).place(x=447,y=87)


        def stopmusic():
            mixer.music.stop()
            #print('musicplaying')
            self.label1['text']='Music_Stoped..'
         #button--
        self.photo_B3=ImageTk.PhotoImage(file='stopreal.png')
        photo_B3=Button(self.root,image=self.photo_B3,bd=0,bg='white',command=stopmusic).place(x=733,y=85)
        
        def mute():
            self.scale.set(0)
        

        #volume bar---
        self.volimg=ImageTk.PhotoImage(file='vol.png')
        volimg=Button(self.root,image=self.volimg,command=mute, bg='white',bd=0).place(x=45,y=560)
       
        def volume(vol):
           volume=int(vol)/100
           mixer.music.sset_volume(volume)
       
        #volume--
        self.scale=Scale(self.root,from_=0,to=100,bg='white',orient=HORIZONTAL,length=360,command='volume')
        self.scale.set(25)
        self.scale.place(x=200,y=650)




root = Tk()
obj=musicplayer(root)
root.mainloop()
