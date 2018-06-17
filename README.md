使用python內建模塊tkinter來自製簡易計算機
============================================================
程式語言:使用python  ， 撰寫:Alan Tao<br />
自己最近才剛開始用線上課程學習python<br />
雖然python的指令相較於c++簡單了許多<br />
但對於沒接觸過的物件，仍不熟悉他所擁有的函數和使用方式<br />
程式利用載入tkinter模塊來製作視窗和裡面的label、button等等<br />
因為目前只會簡單的語法，製作出來的成品也相當簡陋<br />
未來會繼續深入學習python語法，有機會的話再來修改這個成品<br />
以下為這次製作的成品:<br />
![Imgur](https://i.imgur.com/J3anoLX.png)

首先是載入import模塊，並用tk取代，方便以後使用此類別<br />
<pre><code>import tkinter as tk</pre></code>
接著建立視窗，使用tkinter的物件Tk並指定給物件window<br />
<pre><code>window=tk.Tk()
window.title("Welcome to Alan's calculator")
window.geometry('500x500')</pre></code>
字串變數物件var作為儲存label輸入的文字
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
如果鍵入新數字前已經按過"符號鍵"或"清除鍵"<br />
則要把label上顯示的數值清空，故使用var.set('0')<br />
同時使用剛鍵入的數字num指定給res，成為label顯示的數值<br />
如果剛才沒有按"符號鍵"或"清除鍵"，才先將var.get()儲存的數值傳給oldnum<br />
並且將oldnum與剛才鍵入的數值字串物件將加，並指定給res後重新var.set(res)<br />
處理符號鍵的函數部分如下:
<pre><code>def presign(sign):
    global hit_plus
    oldnum = var.get()
    numlist.append(oldnum)
    numlist.append(sign)    
    print(numlist)   
    hit_plus=True</pre></code>
同樣先將var.get()入前所儲存的數值傳給oldnum<br />
並且將此oldnum附加到numlist陣列的最後面<br />
最後再附加剛剛鍵入的符號<br />
最後print(numlist)只是方便我監看陣列內容是否正確而已<br />
並將hit_plus旗標設為True<br />
處理解答(按下等號)的函數部分如下:
<pre><code>def presseq(signeq):
    oldnum = var.get()
    numlist.append(oldnum)
    print(numlist)
    result = ''.join(numlist)
    var.set(eval(result))
    print(numlist)</pre></code>
同樣是將目前var.get()值放入陣列numlist最後面<br />
然後將字串轉換為可以計算的形式<br />
這部分的語法我目前還沒學到，有參考網路上撰寫<br />
然後print(numlist)也是方便監看正確性而已<br />
當按下clear鍵後的函數部分如下:
<pre><code>def special():
    global hit_clear
    var.set('0')
    numlist.clear()
    hit_clear=True</pre></code>
將陣列numlist給清空，方便下次再放入進數值<br />
然後是製作按鍵button的程式部分:
<pre><code>#按鍵0
b0 = tk.Button(text='0', command=lambda:pressnum('0'))
b0.place(x=10, y=400, width=260, height=80)
#按鍵1
b1 =tk.Button(text='1', command=lambda:pressnum('1'))
b1.place(x=10, y=305, width=80, height=80)
#按鍵2
b2 =tk.Button(text='2', command=lambda: pressnum('2'))
b2.place(x=100, y=305, width=80, height=80)
#按鍵3
b3 = tk.Button(text='3', command=lambda: pressnum('3'))
b3.place(x=190, y=305, width=80, height=80)
#按鍵4
b4 = tk.Button(text='4', command=lambda: pressnum('4'))
b4.place(x=10, y=210, width=80, height=80)
#按鍵5
b5 = tk.Button(text='5', command=lambda: pressnum('5'))
b5.place(x=100, y=210, width=80, height=80)
#按鍵6
b6 = tk.Button(text='6', command=lambda: pressnum('6'))
b6.place(x=190, y=210, width=80, height=80)
#按鍵7
b7 = tk.Button(text='7', command=lambda: pressnum('7'))
b7.place(x=10, y=115, width=80, height=80)
#按鍵8
b8 = tk.Button(text='8', command=lambda: pressnum('8'))
b8.place(x=100, y=115, width=80, height=80)
#按鍵9
b9 = tk.Button(text='9', command=lambda: pressnum('9'))
b9.place(x=190, y=115, width=80, height=80)
#按鍵+
bplus = tk.Button(text='+', command=lambda: presign('+'))
bplus.place(x=295, y=305, width=80, height=80)
#按鍵-
bminus = tk.Button(text='-', command=lambda: presign('-'))
bminus.place(x=390, y=305, width=80, height=80)
#按鍵*
bmul = tk.Button(text='X', command=lambda: presign('*'))
bmul.place(x=295, y=210, width=80, height=80)
#按鍵/
bdiv = tk.Button(text='÷', command=lambda: presign('/'))
bdiv.place(x=390, y=210, width=80, height=80)
#按鍵=
bequal = tk.Button(text='=', command=lambda: presseq('='))
bequal.place(x=295, y=400, width=175, height=80)
#按鍵c
bclear = tk.Button(text='Clear',command = lambda :special())
bclear.place(x=390, y=115, width=80, height=80)</pre></code>
最後是讓程式持續執行的寫法:
<pre><code>window.mainloop()</pre></code>
    




