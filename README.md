# Shoe-store

from tkinter import * #อิมพอตสิ่งที่ต้องการใช้งาน
from tkinter import ttk
import sqlite3
from tkinter import font
import tkinter.messagebox
from tkinter import messagebox
import sys
################################# app1 ############################################################
data=sqlite3.connect("shop.db") #ประกาศการเชื่อม DB
tk1=Tk() #สร้างหน้าจออ TKขึ้นมา
tk1.title("Shop") #ตั้งชื่อหน้าต่าง
imgBG = PhotoImage(file ="Z:\python\Project\Project\__pycache__\preview\Matplotlib\DB\_bg.png") #อิมพอตพื้นหลัง
GLabel_708=Label(tk1,image=imgBG).place(x=0,y=0) #ตำเเหน่งพื้นหลัง
num_1=0 #สร้างขึ้นมาเพื่อใช้ในการสร้างบล็อกไว้เก็บรูป
pho_1=0 #สร้างเพื่อเก็บรูปภาพไว้ในบล็อก
lis=[] #ใช้ลิสในการเก็บ Button
label_=[] #ใช้เก็บตัวที่ต้องการกรอกข้อมูล
# size_=[]
pho=["a"] #ใช้เก็บรูป เอาaมาใช้เพราะไม่ต้องการให้นับที่อินเด็กที่0
sss=["a"] #ใช้เก็บชื่อสินค้า
ddd=["a"] #ใช้ในการเก็บราคาสินค้า
img1 = PhotoImage(file ="Z:\python\Project\_nike.png")
img2 = PhotoImage(file ="Z:\python\Project\puma.png")
img3 = PhotoImage(file ="Z:\python\Project\_adidas.png")
img4 = PhotoImage(file ="Z:\\python\\Project\\Project\\__pycache__\\preview\\Matplotlib\DB\\_qrt.png")
_product=["a"] #จำนวนสินค้าที่ซื้อ
#size_aa=["1"]
for i in range(1,19):
    pho.append("Z:\\tiwpro\\_tiw"+str(i)+".png") #ใช้อิมพอตรูปเข้ามา
    pho[i] = PhotoImage(file =pho[i])
    
for i in range(1,19):
    _product.append(i)
    _product[i] = IntVar() #คลิกซื้อสินค้าเเล้วจะขึ้นตัวเลข
cursor= data.execute('SELECT * FROM shop') #ค้นหาDBเพื่อกับชื่อกับราคาใน sssเเละddd
for i in cursor:
    sss.append(i[1])
    ddd.append(i[2])

def a_2():  #ทำลายหน้าเดิมเเล้วสร้างหน้าใหม่
    try:
        global num_1,pho_1
        for y in range(2):
            for x in range(3):
                lis[num_1].destroy() #ทำลายกล่องสินค้าตั้งเเต่ตำเเหน่งที่1
                label_[num_1].destroy() #ทำลายกล่องข้อความตั้งเเต่ตำเเหน่งที่1
                #size_[num_1].destroy()
                num_1+=1
        num_1=0
        
        _bill.place(x=5000,y=360,width=150,height=150)
        name.place(x=5000,y=360,width=150,height=150)
        name_44.place(x=5000,y=360,width=150,height=150)
        address.place(x=5000,y=360,width=150,height=150)
        GLabel_269.place(x=5000,y=360,width=150,height=150)
        GLineEdit_973.place(x=5000,y=360,width=150,height=150)
        GLabel_708.place(x=5000,y=360,width=150,height=150)
        confirm.place(x=5000,y=670,width=254,height=89)
        billarea.place(x=5000,y=180,width=800,height=500)
    except:
        pass
def MoneyValidation(S): #ดักตัวเลข
    if S.isdigit():
        return True
    tk1.bell()
    return False
vcmd = (tk1.register(MoneyValidation), '%S')
def MoneyValidation_1(S): #ดักตัวหนังสือ
    if S.isalpha(): 
        return True
    tk1.bell()
    return False
vcmd_1 = (tk1.register(MoneyValidation_1), '%S') 


def pay():
    sssseeee=phoj_1.get()
    ss=0
    if len(str(sssseeee)) == 10 :
        
        status=messagebox.askyesno(title="ยืนยัน",message=" ยืนยันรายการสินค้า ")
        if status>0: 
            a_2()
            s=""
            for i in range(1,19):
                ss=ss+ddd[i]*_product[i].get() #ราคารวม จำนวนสินค้า*ราคาสินค้า
            for i in range(1,19):
                if _product[i].get() != 0:
                    s=s+sss[i]+"\n"           #ชื่อสินค้า+ชื่อสินค้า
                    _product[i].set(0) #set0คือเคลียข้อมูล
            c=data.cursor()
            c.execute(f"""INSERT INTO record(name,address,Tel,nameshoe,price) VALUES ("{name_1.get()}","{app_1.get()}","{phoj_1.get()}","{s}","{ss}")""")
            data.commit()
            c.close()    
            _bill.place(x=350,y=200,width=530,height=400)
    else:
        status=messagebox.askyesno(title="ยืนยัน",message=" กรอกเบอร์โทรให้ครบ ")
billarea=Frame(tk1,bd=10,relief=GROOVE,bg="#000000")
bill_title=Label(billarea,text="Bill",font=("Times",19),fg="#ffffff",bd=7,bg="#d39c2e")
bill_title.pack(fill=X)
scrol_y=Scrollbar(billarea,orient=VERTICAL)
txtarea=Text(billarea,font=("Times",15),yscrollcommand=scrol_y.set)
scrol_y.pack(side=RIGHT,fill=Y)
scrol_y.config(command=txtarea.yview)
txtarea.pack(fill=BOTH,expand=2)

def bill():
    a_2()
    billarea.place(x=0,y=180,width=800,height=500)
    ss=0 #ทำให้เป็นค่าเริ่มต้นเพื่อรอรับข้อมูล
    txtarea.delete(1.0,END) #เคลียข้อมูลเดิม
    txtarea.insert(END,f"ชื่อ\t\t\t\t\tจำนวน\t\tราคา\n")
    for i in range(1,19):
        if _product[i].get() != 0: #กดเลือกสินค้าเเล้วไปหน้าบิล
            txtarea.insert(END,f"{sss[i]}\t\t\t\t\t{_product[i].get()}\t\t{ddd[i]}\tBath \n\n") #เเสดงชื่อสินค้าราคา
            ss=ddd[i]*_product[i].get()+ss #ราคารวม
    txtarea.insert(END,f" รวม\t\t\t\t\t{ss}\tBath \n") #เเสดงราคารวม

    name.place(x=980,y=180,width=280,height=30)
    name_44.place(x=840,y=170,width=104,height=41)
    address.place(x=980,y=250,width=281,height=30)
    GLabel_269.place(x=840,y=245,width=112,height=36)
    GLineEdit_973.place(x=980,y=320,width=280,height=30)
    GLabel_708.place(x=840,y=312,width=105,height=44)
    confirm.place(x=920,y=670,width=254,height=89)

def c3(e):
    ww=0
    gender = e.widget["text"] 
    cursor= data.execute(f"""SELECT * FROM shop WHERE id="{gender}" """)  #ข้อความในtextไปลบอยู๋BD
    for i in cursor:
        ww=i[3]-1 #ตรวจสอบi3ในDb
    if ww>-1:
        d =_product[gender].get() #ลดของในDB ตามจำนวนที่เราเลือกสินค้า
        d +=1 #กดเพิ่มจำนวนสินค้า
        ww=0
        _product[gender].set(d)
        cursor= data.execute(f"""SELECT * FROM shop WHERE id="{gender}" """) 
        for i in cursor:
            ww=i[3]-1 #ลดจำนวนสินค้าในDB
        c=data.cursor()
        data.execute(f"""update shop set stock = {ww} where id="{gender}" """)
        data.commit()
        c.close()    
    else:
        tkinter.messagebox.showinfo('Hello Peeps','run out')


def c4(e):
    gender = e.widget["text"]
    if _product[gender].get() - 1 > -1:
        d =_product[gender].get()
        d -=1 #ลบสินค้าออกจากช่องจำนวนสินค้าตอนเลือก
        _product[gender].set(d)
        cursor= data.execute(f"""SELECT * FROM shop WHERE id="{gender}" """) #เลือกใช้shop
        for i in cursor:
            ww=i[3]+1 #กดยกเลิกเเล้วจะบวกเพิ่มในDB
        c=data.cursor()
        data.execute(f"""update shop set stock = {ww} where id="{gender}" """) #อัพเดตข้อมูลในshopช่องstock
        data.commit()
        c.close()    

def a_1(e):
    global num_1,a_ll,pho_1,a
    gender = e.widget["text"]
    a_2()
    if gender=="Nike":
        pho_1=1              
    elif  gender=="Adidas":
        pho_1=7
    elif  gender=="Puma":
        pho_1=13
    for y in range(2):
        for x in range(3):
            lis.append(num_1) #เก็บnum1เข้าไปในลิส
            label_.append(num_1)
            #size_.append(num_1)
            lis[num_1]=Button(text=pho_1,image=pho[pho_1]) #เพื่อหมุนรูปเพื่อใช้ในการกดปุ่ม
            lis[num_1].place(x=40+400*x,y=100+350*y,width=300,height=250)
            lis[num_1].bind("<Button-1>", c3)
            lis[num_1].bind("<Button-3>", c4)
            label_[num_1] = Entry(textvariable=_product[pho_1],font=('Times',11),bg="#ffdb93",fg="#4a1262")
            label_[num_1].place(x=150+400*x,y=370+350*y,width=80,height=50)

            # size_[num_1] = Entry(textvariable=size_aa[pho_1],font=('Times',11),bg="#ffdb93",fg="#4a1262")
            # size_[num_1].place(x=250+400*x,y=370+350*y,width=80,height=50)

            num_1+=1
            pho_1+=1
    pho_1=0  
    num_1=0

Button_387=Button(tk1,text = "Nike",image=img1)
Button_387.bind("<Button-1>", a_1)
Button_387.place(x=40,y=0,width=169,height=65)

Button_298=Button(tk1,text = "Adidas",image=img3)
Button_298.bind("<Button-1>", a_1)
Button_298.place(x=380,y=0,width=169,height=65)

Button_546=Button(tk1,text = "Puma",image=img2)
Button_546.bind("<Button-1>", a_1)
Button_546.place(x=750,y=0,width=169,height=65)

Button_770=Button(tk1,text = "Bill",command=bill,font=42)
Button_770.place(x=1090,y=0,width=169,height=65)


_bill=Button(tk1,image=img4)


name_1=StringVar()
name_44=Label(tk1,font=("Times",20))
name_44["text"] = "ชื่อ-สกุล"
name=Entry(tk1,textvariable=name_1,validate='key', vcmd=vcmd_1,font=("Times",15))

app_1=StringVar()
GLabel_269=Label(tk1,font=("Times",20))
GLabel_269["text"] = "ที่อยู่"
address=Entry(tk1,textvariable=app_1,font=("Times",15))

phoj_1=StringVar()
GLabel_708=Label(tk1,font=("Times",20))
GLabel_708["text"] = "เบอร์โทร"

GLineEdit_973=Entry(tk1,textvariable=phoj_1,validate='key', vcmd=vcmd,font=("Times",15))

confirm=Button(tk1,command=pay,font=("Times",20))
confirm["text"] = "ยืนยัน"


tk1.geometry("1280x780+0+0")
tk1.resizable(False,False)
tk1.mainloop()
