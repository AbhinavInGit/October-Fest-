#hum pe to hai hi 9
# October-Fest-
# Project Name          : Hotel Management System
# Made by               : rakesh kumar
# session               : your session name
# roll  no              : your roll no

import mysql.connector
from datetime import date
#global variables
hotel_name =''
addr =''
phone=''
email =''
gst=0
st =0

def settings():
  global hotel_name
  global addr
  global phone
  global email
  global gst
  global st
  conn = mysql.connector.connect(
      host='localhost', database='hotel', user='root', password='')
  cursor = conn.cursor()
  sql = "select * from setting;"
  cursor.execute(sql)
  records = cursor.fetchall()
  for record in records:
    if record[1]=='hotel_name':
       hotel_name = record[2]
    if record[1] == 'address':
       addr = record[2]
    if record[1] == 'phone':
       phone = record[2]
    if record[1] == 'email':
       email = record[2]
    if record[1] == 'gst':
       gst = record[2]
    if record[1] == 'st':
       st = record[2]
  
def system_settings():
    conn = mysql.connector.connect(
      host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    clear()
    print(' Change System Settings ')
    print('*'*120)
    print('1.   Hotel Name')
    print('2.   Hotel Address')
    print('3.   Phone Number(s)')
    print('4.   Email ID')
    print('5.   Current GST Rate')
    print('6.   Current Service Rate')

    choice = int(input('Enter your choice :'))
    field_name =''
    if choice ==1:
       field_name='hotel_name'
    if choice ==2:
       field_name='address'
    if choice ==3:
       field_name='phone'
    if choice ==4:
       field_name='email'
    if choice ==5:
       field_name='gst'
    if choice ==6:
       field_name='st'
    value = input('Enter new value :')   
    sql ='update setting set value= '+value+' where field_name = "'+ field_name+'";'
    cursor.execute(sql)
    conn.close()
    wait = input('\n\n\n Record Updated .............Press any key to continue......') 
  
     

def clear():
  for _ in range(65):
     print()

def room_exist(room_no):
    conn = mysql.connector.connect(
      host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    sql ="select * from rooms where room_no ="+room_no+";"
    cursor.execute(sql)
    record = cursor.fetchone()
    return record


def customer_exist(cust_no):
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    sql = "select * from customer where id ="+cust_no+";"
    cursor.execute(sql)
    record = cursor.fetchone()
    return record

def add_room():
  conn = mysql.connector.connect(
      host='localhost', database='hotel', user='root', password='')
  cursor = conn.cursor()
  clear()
  print('Add New Room - Screen')
  print('-'*120)
  room_no = input('\n Enter Room No :')
  room_type = input('\n Enter Room Type( AC/DELUX/Super Delux/Queen Delight/ Kings Special/Super Rich Special) :')
  room_rent = input('\n Enter Room Rent (INR) :')
  room_bed = input('\n Enter Room Bed Type(Single/Double/Triple) :')
  sql = 'insert into rooms(room_no,room_type,room_rent,room_bed,status) values \
        ('+room_no+',"'+ room_type.upper()+'",'+room_rent+',"'+room_bed.upper()+'","free");'
  
  result = room_exist(room_no)
  if result is None:
    cursor.execute(sql)
  else:
    print('\n\n\nRoom No ',room_no, ' already exists in our database')
  conn.close()
  wait = input('\n\n\n Press any key to continue....')


def modify_room():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    clear()
    print(' Change Room Information ')
    print('*'*120)
    print('1.   Room Type')
    print('2.   Room Rent')
    print('3.   Room Bed')
    choice = int(input('Enter your choice :'))
    field_name = ''
    if choice == 1:
       field_name = 'room_type'
    if choice == 2:
       field_name = 'room_rent'
    if choice == 3:
       field_name = 'room_bed'
    room_no  = input('Enter room No :')   
    value = input('Enter new value :')
    sql = 'update rooms set ' +field_name +' = '+ value +' where  room_no =' + room_no +';'
    cursor.execute(sql)
    wait = input('\n\n\n Record Updated .............Press any key to continue......')

def add_customer():
  conn = mysql.connector.connect(
      host='localhost', database='hotel', user='root', password='')
  cursor = conn.cursor()
  clear()
  print('Add New Customer - Screen')
  print('-'*120)
  name = input('\n Enter Customer Name :')
  address = input('\n Enter Customer Address:')
  phone = input('\n Enter Customer Phone NO :')
  email = input('\n Enter Customer Email ID :')
  id_proof = input('\n Enter Customer ID(Aadhar/Passport/DL/VoterID)  :')
  id_proof_no = input('\n Enter Customer ID proof NO :')
  males = input('\n Enter Total Males :')
  females = input('\n Enter Total Females :')
  children = input('\n Enter Total Childeren :')

  sql = 'insert into customer(name,address,phone,email,id_proof,id_proof_no,males,females,children) values \
        ("'+name+'","' + address.upper()+'","'+phone+'","'+email.upper()+'","'+id_proof.upper()+'","'+id_proof_no.upper()+'",'+males+','+females+','+children+');'

  cursor.execute(sql)
  print('\n\n\nCustomer Added success fully ...............')
  conn.close()
  wait = input('\n\n\n Press any key to continue....')


def modify_customer():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    clear()
    print(' Change Customer Information ')
    print('*'*120)
    print('1.   Name')
    print('2.   Address')
    print('3.   Phone No')
    print('4.   Email ID')
    print('5.   ID Proof')
    print('6.   ID Proof No')
    print('7.   Males')
    print('8.   Females')
    print('9.   Childeren')
    choice = int(input('Enter your choice :'))
    field_name = ''
    if choice == 1:
       field_name = 'name'
    if choice == 2:
       field_name = 'address'
    if choice == 3:
       field_name = 'phone'
    if choice == 4:
       field_name = 'email'
    if choice == 5:
       field_name = 'id_proof'
    if choice == 6:
       field_name = 'id_proof_no'
    if choice == 7:
       field_name = 'males'
    if choice == 8:
       field_name = 'females'
    if choice == 9:
       field_name = 'children'
    cust_no = input('Enter Customer No :')
    value = input('Enter new value :')
    sql = 'update customer set ' + field_name + ' = ' + \
        value + ' where  id =' + cust_no + ';'
    cursor.execute(sql)
    wait = input(
        '\n\n\n Record Updated .............Press any key to continue......')

def room_booking():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    room_id =input('Enter room no to book :')
    cust_id = input('Enter customer ID :')
    date_of_occ = input('Enter date of occupancy (yyyy-mm-dd) :')
    advance = input('Enter advance amount :')
    sql1 = 'update rooms set status = "occupied" where id ='+room_id +';'
    sql2 = 'insert into booking(room_id,cust_id,doo,advance) values ('+room_id+','+cust_id+',"'+date_of_occ+'",'+advance+');'
    #print(sql2)
    #print(sql1)
    result = room_exist(room_id)
    result1 = customer_exist(cust_id)

    if result[5]=='free' and result1 is not None: 
      cursor.execute(sql1)
      cursor.execute(sql2)
      print('\n\n\nRoom no ', room_id, 'booked for', cust_id)
    
    if result[5] !='free':
       print('\n Room is not available for booking. Right now it is :',result[5])
    if result1 is None:
       print('Customer does not exist....Please add customer first in our database')
    conn.close()
    wait = input('\n\n\n Press any key to continue....')


def bill_generation():
    global gst
    global st
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    room_id = input('Enter room no to book :')
    cust_id = input('Enter customer ID :')
    sql = 'select * from booking where cust_id='+cust_id +' and room_id = '+room_id+' and dol is NULL;'
    cursor.execute(sql)
    record = cursor.fetchone()
    clear()
    print('Bill Generation ')
    print('-'*100)
    print(' Rooms occupied  :',room_id)
    dol = date.today()
    book_id = record[0] # book_id
    doo = record[3]
    advance = record[5]
    total_days = (dol-doo).days
    result = room_exist(room_id)
    rent = result[3]
    amount = total_days*rent
    gst_amount = amount*int(gst)/100
    st_amount = amount*int(st)/100
    payable_amount = total_days*rent - advance + gst_amount+st_amount

    print('Date of Occupancy :',doo, '\nDate of Leaving :',dol)
    print('Total Payable Days : ', total_days)
    print('Room Rent Per Day : ', rent)
    print('Total Amount  :',amount)
    print('Advance :',advance,'\nGST ({}) : {} '.format(gst,gst_amount), '\nService Tax ({}) : {}'.format(st,st_amount))
    print('Amount Payable :',payable_amount)
    sql1 = 'update rooms set status ="free" where room_no ='+room_id +';'
    sql2 = 'update booking set dol ="'+str(dol)+'" where room_id='+room_id+' and cust_id ='+cust_id +';'
    
    sql3 = 'insert into bill(book_id,amount,bill_date,gst,st) values('+str(book_id)+','+str(payable_amount)+',"'+str(dol)+'",'+str(gst)+','+str(st)+');'
    cursor.execute(sql1)
    cursor.execute(sql2)
    cursor.execute(sql3)
    conn.close()
    wait = input('\n\n\n Press any key to continue....')


def search_rooms():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    room_no = input('Enter Room No :')
    sql ='select * from rooms where room_no ='+room_no +';'
    cursor.execute(sql)
    record = cursor.fetchone()
    clear()
    print('Room Status')
    print('*'*120)
    print('Room NO :',record[1])
    print('Room Rent :',record[2])
    print('Room Bed :',record[3])
    print('Room Status :',record[4])
    conn.close()
    wait = input('\n\n\nPress any key to continue......')


def search_customer():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    
    clear()
    print('Search Customer DataBase')
    print('*'*120)
    print('1.   Customer Name')
    print('2.   Customer Address')
    print('3.   Customer Phone')
    print('4.   Customer Email')
    print('5.   Address Proof')
    print('6.   Address Proof ID')
    choice = int(input('Enter your choice : '))
    field_name =''
    if choice ==1:
      field_name = 'name'
    if choice ==2:
      field_name = 'address'
    if choice ==3:
      field_name = 'phone'
    if choice ==4:
      field_name = 'email'
    if choice ==5:
      field_name = 'id_proof'
    
    if choice ==6:
      field_name = 'id_proof_no'
    
    value = input('Enter value that you want to search :')
    if field_name =='id':
      sql = 'select * from customer where '+ field_name +' = '+ value + ';'
    else:
      sql = 'select * from customer where ' + field_name + ' like "%' + value + '%";'
    print(sql)
    cursor.execute(sql)
    records = cursor.fetchall()
    clear()
    print('Search Result for {} = {}'.format(field_name,value))
    print('*'*140)
    print('{} {:20s} {:30s} {:15s} {:30s} {:20s} {:15s}'.format('ID','Name','Address','Phone','Email','ID Used','ID No'))
    for record in records:
      print('{} {:20s} {:30s} {:15s} {:30s} {:20s} {:15s}'.format(
          record[0], record[1], record[2], record[3], record[4], record[5], record[6]))

    conn.close()
    wait = input('\n\n\nPress any key to continue......')


def search_booking():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    cust_no = input('Enter Customer No :')
    sql = 'select book_id,r.room_no,c.name,doo,advance from booking b, customer c,rooms r where b.room_id = r.id AND b.cust_id = '+cust_no+' and dol is NULL;'
    cursor.execute(sql)
    records = cursor.fetchall()
    clear()
    print('Booking information for customer ID :{}'.format(cust_no))
    print('{} {} {} {} {}'.format('ID','RoomID', 'Customer Name','Date of Occupancy','Advance'))
    print('*'*140)
    for record in records:
      print('{} {} {} {} {}'.format(
          record[0], record[1], record[2], record[3], record[4]))
    conn.close()
    wait = input('\n\n\nPress any key to continue......')


def search_bills():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    bill_no = input('Enter Bill No :')
    sql = ' select bill.bill_id,bill.amount,bill_date,gst,st,b.book_id,doo,dol,advance, name,address,phone,email,room_no \
            from bill, booking b, customer c , rooms r \
            where bill.book_id = b.book_id \
            and b.room_id = r.id and b.cust_id = c.id AND NOT dol is NULL AND \
            bill_id = '+bill_no +';'
    cursor.execute(sql)
    record = cursor.fetchone()
    clear()
    print('Bill information for Bill No :{}'.format(bill_no))
    print('*'*140)
    print('Bill NO ', record[0])
    print('Amount ', record[1])
    print('Bill Date ', record[2])
    print('GST Charged ', record[3])
    print('Service Tax Charged ', record[4])
    print('Booking ID ', record[5])
    print('Room Used ID ', record[13])
    print('Date of Occupancy ', record[6])
    print('Date of Leaving ', record[7])
    print('Advance Paid ', record[8])
    print('Customer Name ', record[9])
    print('Customer Address ', record[10])
    print('Customer Phone ', record[11])
    print('Customer Email ID ', record[12])

    conn.close()
    wait = input('\n\n\nPress any key to continue......')


def search_menu():
    while True:
      clear()
      print(' Search Menu')
      print('*'*120)
      print("\n1.  Room Status")
      print('\n2.  Booking Status')
      print('\n3.  customer Details')
      print('\n4.  Bills')
      print('\n5.  Back to Main Menu')
      print('\n\n')
      choice = int(input('Enter your choice ...: '))
      if choice==1:
        search_rooms()
      if choice==2:
        search_booking()
      if choice==3:
        search_customer()
      if choice==4:
        search_bills()
      if choice==5:
        break


def report_room_status():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    sql = 'select * from rooms'
    cursor.execute(sql)
    records = cursor.fetchall()
    clear()
    print(' Rooms Status - Report')
    print('-'*120)
    print('{:10s} {:10s} {:20s} {:20s} {:>40s} {:>30s}'.format('Room ID','Room No', 'Room Type', 'Rent','Bedding', 'Status'))
    for idr,no,rtype,rent,bed,status in records:
        print('{:<10d} {:<10d} {:20s} {:<7.2f} {:>40s} {:>30s}'.format(idr, no, rtype, rent, bed, status))
    conn.close()
    wait = input('\n\n\n Press any key to continue....')


def report_booking_status():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    sql = 'select b.book_id,room_no,doo,dol,advance, name,address,phone \
           from booking b, customer c ,rooms r \
           where b.room_id = r.id and b.cust_id = c.id and dol is NULL;'
    cursor.execute(sql)
    records = cursor.fetchall()
    clear()
    print(' Booking Status - Report')
    print('-'*120)
    print('{:10s} {:10s} {:20s} {:20s} {:>30s} {:20s} {:30s} {:15s}'.format(
        'Booking ID', 'Room No', 'DOO', 'DOL', 'Advance', 'Name','Address','Phone'))
    for idr, no, doo,dol,advance,name,addr,phone in records:
        print('{:10d} {:10d} {:20s} {:20s} {:10.2f} {:20s} {:30s} {:15s}'.format(
            idr, no, str(doo), str(dol), advance, name, addr, phone))
    conn.close()
    wait = input('\n\n\n Press any key to continue....')

def report_menu():
    while True:
      clear()
      print('Report Menu')
      print("\n1.  Room Status")
      print('\n2.  Booking Status')
      print('\n3.  Today\'s Collection')
      print('\n4.  Monthly Collection')
      print('\n5.  Back to Main Menu')
      print('\n\n')
      choice = int(input('Enter your choice ...: '))
      if choice == 1:
        report_room_status()
      if choice == 2:
        report_booking_status()
      if choice == 3:
        report_todays_collection()
      if choice == 4:
        report_monthly_collection()
      if choice == 5:
        break

def change_room_status():
    conn = mysql.connector.connect(
        host='localhost', database='hotel', user='root', password='')
    cursor = conn.cursor()
    clear()
    room_no = input('Enter Room No :')
    status = input('Enter current status(Renovation/modification ) :')
    sql = 'update rooms set status="'+status+'" where room_no ='+room_no+';'
    cursor.execute(sql)
    print('\n\nRoom Status Updated')
    wait = input('\n\n\n Press any key to continue....')

def main_menu():
    while True:
      clear()
      print(' H O T E L   M A N A G E M E N T   S Y S T E M ')
      print('*'*120)
      print("\n1.   Add New Room")
      print('\n2.   Add Customer')
      print('\n3.   Modify Room Information')
      print('\n4.   Modify Customer Information')
      print('\n5.   Room Booking')
      print('\n6.   Bill Generation')
      print('\n7.   Search Database')
      print('\n8.   Report Menu')
      print('\n9.   Settings')
      print('\n10.  Close application')
      print('\n\n')
      choice = int(input('Enter your choice ...: '))
      if choice == 1:
        add_room()
      if choice == 2:
        add_customer()
      if choice == 3:
        modify_room()
      if choice == 4:
        modify_customer()
      if choice ==5 :
        room_booking()
      if choice == 6:
        bill_generation()
      if choice ==7 :
        search_menu()
      if choice == 8:
        report_menu()
      if choice == 9:
        system_settings()
      if choice ==10:
        break

if __name__ == "__main__":
    settings()
    main_menu()
