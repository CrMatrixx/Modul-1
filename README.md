# Modul-1
Praktikum Modul 1 CRUD 2 Accounts Student and Teacher
Using Database MySql

from ast import Try, keyword
from itertools import count
from select import select
from sqlite3 import Cursor
from turtle import update
from typing import Iterator
from unicodedata import name
from unittest import result
from urllib import request
import mysql.connector
from os import system

db = mysql.connector.connect(
    host = 'localhost',
    user = 'root',
    password = '',
    database = 'Modul1'

)
def menu():
    
    print("=======================")
    print("=====  1.teacher  ===== ")
    print("=====  2.student  =====")
    jawab = input('Pilih :')
    if jawab == '1' or jawab == 'teacher':
        teacher()
    elif jawab == '2' or jawab == 'student':
        student()
    else:
        system('cls')
        menu()

def teacher():
    
    print('== wellcome teacher ==')
    print('Login dulu')
    name_Teacher = input('Nama :')
    password_Teacher = input('Password :')
    if name_Teacher == 'admin' and  password_Teacher == 'admin':
        menu_teacher()
    else :
        print("wrong password and username!!")
        teacher()
    

def student():
    cursor = db.cursor()
    print('wellcome student')

    username = input('Username :')
    id = input('Password :')
    myqeury = "SELECT * FROM dataprogram WHERE nama LIKE %s AND id LIKE %s"
    val = ("%{}%".format(username),"%{}%".format(id)) 
    if username == 'admin' and id == 'admin':
        print('Login by Administrator!!')
        menu_teacher()
    cursor.execute(myqeury,val)
    result = cursor.fetchall()
        
    if cursor.rowcount < 0:
        print('no data bro')
    else :
        for data in result:
            print(data)
            menu()
    db.commit()
    print('Anda berhasil login!')

## fungsi databse yang akan saya buaat 
def menu_teacher():
    print('=======================')
    print('Silahkan pilih menu ')
    print('1.Tambah Data')
    print('2.Ubah Data')
    print('3.Hapus Data')
    print('4.Tampilkan Data')
    print('5. Remidi murid')
    print('0.Keluar')
    menu2 = input('Pilih menu : ')
    if menu2 == '1':
        tambahdata()
    elif menu2 == '2':
        editnilai()
    elif menu2 == '3':
        print('hapus data')
    elif menu2 == '4':
        Alldata() & menu_teacher()
    elif menu2 == '0':
        menu()
    elif menu2 == '5':
        remidi()

def tambahdata():
    cursor = db.cursor()
    id = input('Id anda :')
    nama = input('Nama Mahasiswa : ')
    ulangan  = int(input('Nilai ulangan :'))
    if input == 0 :
        print('Masukkan ulangan harian maksimal 3x ')
        Sulangan(ulangan)

    uts = int(input ('Nilai uts :'))
    uas = int(input ('Nilai uas :'))
    level = input('Status : ')
    Nakhir =  ulangan+uas/2
    print('Nilai akhir :', Nakhir)
    myquery = "INSERT INTO dataprogram(id,nama,ulangan,uts,uas,level,total) VALUES ({},'{}',{},{},{},'{}',{})".format(id,nama,ulangan,uts,uas,level,Nakhir)
    cursor.execute(myquery)
    db.commit()
    print('data ditambahkan')
    menu_teacher()

def Sulangan(iterable, action):
    Iterator  = iter (iterable)
    looping  = False
    while not looping:
        try:
            item = next(Iterator)
        except StopIteration:
            looping = True
        else:
            action(item)
limit = [3]



def editnilai():
    cursor = db.cursor()
    id = int(input('Pilih data mahasiswa berdasaarkan ID : '))
    nama = input('Update nama :')
    uts = int(input ('Update uts :'))
    uas = int(input ('Update uas :'))
    level = input('Update Status : ')
    Nakhir = float(input('Nilai Akhir :'))
    sql = "UPDATE dataprogram SET nama=%s, uts=%s, uas=%s,level=%s,total=%s WHERE id =%s"
    val = (nama,uts,uas,level,Nakhir,id)
    cursor.execute(sql, val)
    # sqlid = "UPDATE dataprogram SET nama={} uts={} uas={} level={} total={} WHERE id = {}".format(nama,uts,uas,level,Nakhir,id)
    # cursor.execute(sqlid)
    db.commit() 
    print(' DATA DI UPDATE!') 
    menu_teacher()

def Alldata():
    cursor = db.cursor()
    print(' == DATA MAHASISWA == ')
    sql  = "SELECT * FROM dataprogram"
    cursor.execute(sql)
    semuadata  = cursor.fetchall()
   
    for data in semuadata:
        print(data)

def remidi():
    print('Apakah ingin remidi ?')
    rmd = input('y/n?')
    if rmd == 'y':
        namamhs = input('Nama mahasiswa yang remidi ')
        for n in count(namamhs):
            print(n)

menu()

# def teacher():
#     cursor = db.cursor()
#     show_data = "SELECT * FROM dataprogram"
#     cursor.execute(show_data)


#    # menampilkan isi dari database menggunakan method fetchall
#     results = cursor.fetchall()
#     for i in results:
#         print(i)



# def student():
#     nama = input('NIM')
#     pic = input('PIC')


# cursor = db.cursor()
# cursor.execute(
#     """
#     CREATE TABLE dataprogram(
#     id INT AUTO_INCREMENT PRIMARY KEY,
#     nama VARCHAR(100) NOT NULL,
#     uts int NOT NULL,
#     uas int NOT NULL,
#     total int NOT NULL
#     )
#     """
# )
# cursor = db.cursor()
# query = "INSERT INTO dataprogram(nama, uts, uas, total) VALUES(%s,%s, %s, %s)"
# data = ("Mochi Killer", "90", "90","95")

# cursor.execute(query, data)

# db.commit()
# print("Data berhasil di insert")
# print("Table berhasil dibuat")



# if db.is_connected():
#     print("berhasil")


# cursor = db.cursor()
# cursor.execute("CREATE DATABASE Modul1")
# print("database berhasil di buat ")
