# Assignment-1
Registration and Login system using Python, file handling.
step 1: Registration 
1.email/username should have "@" and followed by ".",
2.There should not be any "." immediate next to "@"
3.it should not start with special characters and numbers
4.password (5 < password length > 16) Must have minimum one special character,one digit,one uppercase and one lowercase character

soluion:
  # Registration registration Block
      user = input("Create your username : ")
                count=0
                file=open('Assignment.txt','r')
                for i in file:
                    if user in i:
                        count=1
                        print("Same username already exists, Please try different username")
                if user[0].isdigit()==True:
                    count=1
                    print("username should not start with number")
                if " " in user:
                    count= 1
                    print("username should not have space")
                import re
                spcr1 = '[@_!#$%^&*()<>?/\|}{~:]'
                for each in spcr1:
                    if each==user[0]:
                        count=1
                        print("invalid - Username should not start with special character ")
                l = re.findall('.+@.+\.[a-z]',user)
                if l!=[]:
                    if count==0:
                        print('Valid username')
     # Password Registration Block
                        print("Password must have minimum one special character,one digit,one uppercase and lowercase character")
                        pw = input("Create your Password : ")
                        b = re.findall('[@_!#$%^&*()<>?/\|}{~:]', pw)
                        if b == []:
                            print("Special character is missing")
                        c = re.findall('[a-z]', pw)
                        if c == []:
                            print("Lowercase character is missing")
                        d = re.findall('[A-Z]', pw)
                        if d == []:
                            print("Uppercase character is missing")
                        e = re.findall('[0-9]', pw)
                        if e == []:
                            print("Digit character is missing")
                        if len(b) > 0 and len(c) > 0 and len(d) > 0 and len(e) > 0:
                            if len(pw) > 5 and len(pw) < 16:
                                count1=0
                                if count==0 and count1==0:

                                    file=open("Assignment.txt", "r+")
                                    file.readlines()
                                    file.write(name)
                                    file.write(',')
                                    file.write(user)
                                    file.write(',')
                                    file.write(pw)
                                    file.write('\n')
                                    file.close()
                                    print("Registration process completed.")



  step 2: storing the data
  1.Once the username and password are validated, store that data in a file

  solution:

                                  file=open("Assignment.txt", "r+")
                                  file.readlines()
                                  file.write(name)
                                  file.write(',')
                                  file.write(user)
                                  file.write(',')
                                  file.write(pw)
                                  file.write('\n')
                                  file.close()
                                  print("Registration process completed.")

step 3: Login
1. When the user chooses to Login, check whether his/her credentials exist in the file or not based on the user input. If it doesn’t exist then ask them to go for Registration or If they have chosen forget password you should be able to retrieve their original password based on their username provided in the user input
or else you can ask them to provide a new password (only if their username matches with the data exists in the file).
2. If nothing matches in your file you should ask them to Registration

Solution:
  # Login Block
    def reg(welcome):
        if welcome=='login':
            x=input("Enter your Username : ")
            y=input("Enter your Password : ")
            import os.path
            if os.path.exists('Assignment.txt'):
                pass
            else:
                f = open('Assignment.txt', 'x')
                f.close()
            file = open("Assignment.txt", "r+")
            countone=0
            l= file.readlines()
            for i in l:
                l2=i.split(',')
                if x in l2:
                    countone=1
                    l2[-1]=l2[-1].replace("\n","")
                    if y in l2:
                        countone=2
                        if countone==2:
                            print('Login successful')
                            break
                    else:
                        print('Username is correct and Password is incorrect')
                        countone=3
    #Retrieve Old Password
                        if countone == 3:
                            print("To get or create password Please answer the following questions")
                            name=input("Security question-Enter your name : ")
                            pwc = input("Incorrect password - choose Retrieve password-'rp' or Forget password-'fp' : ")
                            if pwc == 'rp':
                                file = open("Assignment.txt", "r+")
                                for i in file:
                                    h = i.split(',')
                                    if x == h[1]:
                                        h[-1] = h[-1].replace("\n", "")
                                        if name == h[0]:
                                            print(h[2])
                                            break

                                        else:
                                            print("Security answer is incorrect ")
                                            break
    #Forget Password
                            if pwc == 'fp':
                                with open("Assignment.txt", "r+") as file:
                                    total_datas=file.readlines()
                                    countone=4
                                    file.seek(0)
                                    for i in file:
                                        if x in i:
                                            z=total_datas.index(i)
                                            countone=5
                                            break
                                    if countone==5:
                                        newpw = input("Enter new Password : ")
                                        newpw1 = input("Re-Enter new Password : ")
                                        if newpw == newpw1:
                                            import re
                                            p = re.findall('[@_!#$%^&*()<>?/\|}{~:]', newpw)
                                            if p == []:
                                                print("Special character is missing")
                                            q = re.findall('[a-z]', newpw)
                                            if q == []:
                                                print("Lowercase character is missing")
                                            r = re.findall('[A-Z]', newpw)
                                            if r == []:
                                                print("Uppercase character is missing")
                                            s = re.findall('[0-9]', newpw)
                                            if s == []:
                                                print("Digit character is missing")
                                            if len(p) > 0 and len(q) > 0 and len(r) > 0 and len(s) > 0:
                                                if len(newpw) > 5 and len(newpw) < 16:
                                                    total_datas[z]=(name + ',' + x + ',' + newpw+'\n')
                                                    file=open('Assignment.txt','w+')
                                                    file.seek(0)
                                                    file.writelines(total_datas)
                                                    file.close()
                                                    print("Password successfully updated. Login now")
                                        else:
                                            print("Password mismatching. Please enter password correctly")
                                            break

            if countone==0:
                print("Your Username is Not valid, Kindly Go for the 'Registration'")
      
            
            
            



            
