使用python內建模塊tkinter來自製簡易計算機
============================================================
自己最近才剛開始用線上課程學習python<br />
雖然python的指令相較於c++簡單了許多<br />
但對於沒接觸過的物件，仍不熟悉他所擁有的函數和使用方式<br />
程式利用載入tkinter模塊來製作視窗和裡面的label、button等等<br />
因為目前只會簡單的語法，製作出來的成品也相當簡陋<br />
未來會繼續深入學習python語法，有機會的話再來修改這個成品<br />

首先是載入import模塊，並用tk取代，方便以後使用此類別<br />
<pre><code>import tkinter as tk</pre></code>
接著建立視窗，使用tkinter的物件Tk並指定給物件window<br />
<pre><code>window=tk.Tk()
window.title("Welcome to Alan's calculator")
window.geometry('500x500')</pre></code>
字串變數物件var作為儲存label輸入的文字<br />
<pre><code>var = tk.StringVar()</pre></code>
陣列numlist作為儲存當前輸入的所有計算(包括數字與符號)
<pre><code>numlist=[]</pre></code>
判斷是否按過符號鍵 按了之後到下一個數字輸入期間=True 
<pre><code>hit_plus=False</pre></code>
判斷是否按過清空符號
<pre><code>hit_clear=False</pre></code>
屏幕部分，使用label來顯示，textvariable即設定為var物件
<pre><code>scream=tk.Label(anchor='e',bg='blue',textvariable=var,font=('Arial,50'))
scream.place(x=65, y=10, width=380, height=60)</pre></code>
處理輸入數字的函數部分如下:
<pre><code>def pressnum(num):
    global hit_plus
    global hit_clear
    if (hit_plus==True) | (hit_clear==True):
        var.set('0')
        res=num
        var.set(res)
        hit_plus=False
        hit_clear=False
    else:
        oldnum=var.get()
        res = oldnum + num  
        var.set(res)
</pre></code>        
