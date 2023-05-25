
import statistics;
import tkinter as tk
import random
from tkinter import *
from tkinter import filedialog
from PIL import ImageTk, Image
import numpy as np
from skimage import io
from scipy.fft import dctn
from bitarray import bitarray
import cv2
from matplotlib import pyplot as plot;
from tkinter import ttk
from tkinter.filedialog import askopenfilename
from tkinter import filedialog as tkFileDialog
import math

win = tk.Tk()
win.title("Adaptive Median Filter")
win.geometry("750x750")
scale_percent = 50

def original():
    path = tkFileDialog.askopenfilename()
    img = cv2.imread(path)
    width = int(img.shape[1] * scale_percent / 100)
    height = int(img.shape[0] * scale_percent / 100)
    dim = (width, height)
    resized = cv2.resize(img, dim, interpolation=cv2.INTER_AREA)
    im = Image.fromarray(resized)
    imgtk1 = ImageTk.PhotoImage(image=im)
    label1.configure(image=imgtk1)
    label1.image = imgtk1
    return img;

def med(arr,window):
   n=0;
   a = np.zeros(window*window);
   t=0;
   for x in range(window):
     for y in range(window):
       if(t<window*window):
         a[t]=arr[x][y];
         t=t+1;
   a.sort();
   n=statistics.median(a);
   return n;

def mn(arr,window):
   m=arr[0][0];
   for x in range(window):
       for y in range(window):
           if(arr[x][y]<m):
               m=arr[x][y];
   return m;


def mx(arr,window):
    m = arr[0][0];
    for x in range(window):
        for y in range(window):
            if (arr[x][y] > m):
                m = arr[x][y];

    return m;


def add_noise():

 img=original()
 m=img.shape[0];
 n=img.shape[1];
 for x in range(10000):
      i=random.randint(0,m-1);
      j=random.randint(0,n-1);
      img[i][j]=255;


 for x in range(10000):
      i=random.randint(0,m-1);
      j=random.randint(0,n-1);
      img[i][j]=0;

 cv2.imshow('i',img);


def adm_filter():
  m = img.shape[0];
  n = img.shape[1];
  window_max=7;
  window_size=3
  a = np. zeros((3,3),dtype=np.uint8);
  midx=0;
  midy=0;
  midX=0;
  midY=0;
  midO=0;
  dx=0;
  dy=0;
  o=0;
  do=0;
  for x in range(m):
      for y in range(n):
          for k in range(window_size):
            o=0;
            for l in range(window_size):
               if(x<m and y<n and o<3):
                 a[k][l]=img[x][y][o];
                 if(k==l):
                     midx=k;
                     midy=l;
                     midX=x;
                     midY=y;
                     midO=o;
                     dx=x;
                     dy=y;
                     do=o;
                 x=x+1;
                 y=y+1;
                 o=o+1;

      g_min=mn(a,window_size);
      g_max=mx(a,window_size);
      g_median=med(a,window_size);

      if(g_min<g_median<g_max):
          if(g_min<img[dx][dy][do]<g_max):
           img[dx][dy][do]=img[dx][dy][do]
          else:
             img[dx][dy][do]=g_median
      else:
          for w in range(window_size):
            np.delete(a, w, 0);

          window_size=window_size+2;
          a = np.zeros((window_size,window_size), dtype=np.uint8);
          if(window_size<window_max):
              if (g_min < g_median < g_max):
                  if (g_min < img[dx][dy][do] < g_max):
                      img[dx][dy][do] = img[dx][dy][do]
                  else:
                      img[dx][dy][do] = g_median
          else:
              img[dx][dy][do] = img[dx][dy][do];


  cv2.imshow('o',img);



def Close():
    win.destroy()


# Convert To PhotoImage
# img1= ImageTk.PhotoImage(Image.open("default.jpg")


button = Button(win, text="add_noise", font=('Helvetica 13 bold'), command=add_noise)
button.pack(side=BOTTOM)
button1 = Button(win, text="adm_filter", font=('Helvetica 13 bold'), command=adm_filter)
button1.pack(side=BOTTOM)

button2 = Button(win, text="EXIT", font=('Helvetica 13 bold'), command=Close)
button2.pack(side=BOTTOM)

path = tkFileDialog.askopenfilename()
img = cv2.imread(path)
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
width = int(img.shape[1])  # * scale_percent / 100)
height = int(img.shape[0])  # * scale_percent / 100)
dim = (width, height)
resized = cv2.resize(img, dim, interpolation=cv2.INTER_AREA)
im = Image.fromarray(resized)
im.save('originale_image.jpg')
imgtk = ImageTk.PhotoImage(image=im)
# Create a Label widget
label1 = Label(win, image=imgtk)
label1.place(relx=0.5, rely=0.5, anchor='e')
label1.pack()

# Create a Button to handle the update Image event

win.bind("<Return>")
win.mainloop()

cv2.waitKey(0)


