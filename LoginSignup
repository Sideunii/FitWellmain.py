from tkinter import *
from tkinter import messagebox
import mysql.connector
from subprocess import call  # Import subprocess to run external Python scripts
from PIL import Image, ImageTk  # Import Pillow for image handling

# Database connection
db_connection = mysql.connector.connect(
    host="localhost",
    user="root",
    database="hidb"
)
cursor = db_connection.cursor()

# Create the users table if it doesn't exist
cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    username VARCHAR(255) PRIMARY KEY,
    password VARCHAR(255)
)
""")
db_connection.commit()

# Function to run the three.py file after signup or login
def open_py_file():
    call(["python", "three.py"]) 

# Main application window
root = Tk()
root.title("Login")
root.geometry('925x500+300+200')
root.configure(bg="#C6D1D2")  # Nagset background color to #C6D1D2
root.resizable(False, False)

# Function to handle login
def signin():
    username = user.get()
    password = code.get()

    cursor.execute("SELECT * FROM users WHERE username = %s AND password = %s", (username, password))
    result = cursor.fetchone()

    if result:
        messagebox.showinfo('Success', "Login successful!")
        root.destroy()  # Close the login window
        open_py_file()  # Magrun three.py after ng successful login
    else:
        messagebox.showerror('Invalid', "Invalid Username or Password")

# Function to open the signup window
def open_signup():
    root.withdraw()  # Hide the login window
    signup_window.deiconify()  # Show the signup window

# Function to handle signup
def signup():
    username = signup_user.get()
    password = signup_code.get()
    confirm_password = signup_confirm_code.get()

    if password == confirm_password:
        cursor.execute("SELECT * FROM users WHERE username = %s", (username,))
        result = cursor.fetchone()

        if result:
            messagebox.showerror('Error', 'Username already exists')
        else:
            cursor.execute("INSERT INTO users (username, password) VALUES (%s, %s)", (username, password))
            db_connection.commit()
            messagebox.showinfo('Signup', 'Successfully signed up')
            signup_window.withdraw()  # Close the signup window
            root.destroy()  # Close the login window
            open_py_file()  # Magrun ang three.py pag nagsuccessful signup
    else:
        messagebox.showerror('Invalid', "Passwords do not match")

# Function to return to the login window from signup
def return_to_login():
    signup_window.withdraw()
    root.deiconify()

# Placeholder handling functions
def on_enter(entry, placeholder):
    if entry.get() == placeholder:
        entry.delete(0, 'end')

def on_leave(entry, placeholder):
    if entry.get() == '':
        entry.insert(0, placeholder)

# Load and resize the image
image_path = "Fitwell.png"  # Replace with the actual path to your image
try:
    img = Image.open(image_path)
    img = img.resize((200, 200))  # Resize the image to fit nicely
    img = ImageTk.PhotoImage(img)
except Exception as e:
    print(f"Error loading image: {e}")
    img = None

# Login window UI
if img:
    Label(root, image=img, bg="#C6D1D2").place(x=550, y=150)  # Place on the right side
frame = Frame(root, width=350, height=350, bg='white')  # White background for the login frame
frame.place(x=100, y=70)

heading = Label(frame, text='Sign in', fg='#57a1f8', bg='white', font=('Microsoft YaHei UI Light', 23, 'bold'))
heading.place(x=100, y=5)

# Username Entry with placeholder
user = Entry(frame, width=25, fg='black', border=0, bg="white", font=('Microsoft YaHei UI Light', 11))
user.place(x=30, y=80)
user.insert(0, 'Username')
user.bind("<FocusIn>", lambda e: on_enter(user, 'Username'))
user.bind("<FocusOut>", lambda e: on_leave(user, 'Username'))
Frame(frame, width=295, height=2, bg='black').place(x=25, y=107)

# Password Entry with placeholder
code = Entry(frame, width=25, fg='black', border=0, bg="white", font=('Microsoft YaHei UI Light', 11))
code.place(x=30, y=150)
code.insert(0, 'Password')
code.bind("<FocusIn>", lambda e: on_enter(code, 'Password'))
code.bind("<FocusOut>", lambda e: on_leave(code, 'Password'))
Frame(frame, width=295, height=2, bg='black').place(x=25, y=177)

# Login and Sign Up Buttons
Button(frame, width=39, pady=7, text='Sign in', bg='#57a1f8', fg='white', border=0, command=signin).place(x=35, y=204)
Label(frame, text="Don't have an account yet?", fg='black', bg='white', font=('Microsoft YaHei UI Light', 8)).place(x=75, y=270)
Button(frame, width=6, text='Sign up', border=0, bg='white', cursor='hand2', fg='#57a1f8', command=open_signup).place(x=215, y=270)

# Signup window UI
signup_window = Toplevel(root)
signup_window.title("Sign Up")
signup_window.geometry('925x500+300+200')
signup_window.configure(bg="#C6D1D2")  # Set the background color to #C6D1D2 for signup window
signup_window.resizable(False, False)
signup_window.withdraw()  # Hide signup window initially

if img:
    Label(signup_window, image=img, bg="#C6D1D2").place(x=550, y=150)  # Same placement as login

frame_signup = Frame(signup_window, width=350, height=390, bg='white')  # White background for the signup frame
frame_signup.place(x=100, y=50)

heading_signup = Label(frame_signup, text='Sign up', fg='#57a1f8', bg='white', font=('Microsoft Yahei UI Light', 23, 'bold'))
heading_signup.place(x=100, y=5)

# Signup fields
signup_user = Entry(frame_signup, width=25, fg='black', border=0, bg='white', font=('Microsoft YaHei UI Light', 11))
signup_user.place(x=30, y=80)
signup_user.insert(0, 'Username')
signup_user.bind("<FocusIn>", lambda e: on_enter(signup_user, 'Username'))
signup_user.bind("<FocusOut>", lambda e: on_leave(signup_user, 'Username'))
Frame(frame_signup, width=295, height=2, bg='black').place(x=25, y=107)

signup_code = Entry(frame_signup, width=25, fg='black', border=0, bg='white', font=('Microsoft YaHei UI Light', 11))
signup_code.place(x=30, y=150)
signup_code.insert(0, 'Password')
signup_code.bind("<FocusIn>", lambda e: on_enter(signup_code, 'Password'))
signup_code.bind("<FocusOut>", lambda e: on_leave(signup_code, 'Password'))
Frame(frame_signup, width=295, height=2, bg='black').place(x=25, y=177)

signup_confirm_code = Entry(frame_signup, width=25, fg='black', border=0, bg='white', font=('Microsoft YaHei UI Light', 11))
signup_confirm_code.place(x=30, y=220)
signup_confirm_code.insert(0, 'Confirm Password')
signup_confirm_code.bind("<FocusIn>", lambda e: on_enter(signup_confirm_code, 'Confirm Password'))
signup_confirm_code.bind("<FocusOut>", lambda e: on_leave(signup_confirm_code, 'Confirm Password'))
Frame(frame_signup, width=295, height=2, bg='black').place(x=25, y=247)

# Signup Button
Button(frame_signup, width=39, pady=7, text='Sign up', bg='#57a1f8', fg='white', border=0, command=signup).place(x=35, y=280)
Label(frame_signup, text='I have an account', fg='black', bg='white', font=('Microsoft YaHei UI Light', 9)).place(x=90, y=340)
Button(frame_signup, width=6, text='Sign in', border=0, bg='white', cursor='hand2', fg='#57a1f8', command=return_to_login).place(x=200, y=340)

root.mainloop()

# Close the database connection
cursor.close()
db_connection.close()
