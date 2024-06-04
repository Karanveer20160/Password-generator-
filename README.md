# Password-generator-
import tkinter as tk
from tkinter import messagebox
import random
import string

# Function to generate a password
def generate_password():
    length = int(length_var.get())
    complexity = complexity_var.get()
    password = ""

    if complexity == "Low":
        password = ''.join(random.choices(string.ascii_lowercase, k=length))
    elif complexity == "Medium":
        password = ''.join(random.choices(string.ascii_letters, k=length))
    elif complexity == "Strong":
        password = ''.join(random.choices(string.ascii_letters + string.digits + string.punctuation, k=length))
    
    password_entry.delete(0, tk.END)
    password_entry.insert(0, password)

def copy_to_clipboard():
    root.clipboard_clear()
    root.clipboard_append(password_entry.get())
    messagebox.showinfo("Copied", "Password copied to clipboard")

# Create the main window
root = tk.Tk()
root.title("Password Generator")
root.geometry("400x300")

# Label for password length
length_label = tk.Label(root, text="Password Length:")
length_label.pack(pady=10)

# Entry for password length
length_var = tk.StringVar(value="8")
length_entry = tk.Entry(root, textvariable=length_var, width=5)
length_entry.pack(pady=10)

# Label for password complexity
complexity_label = tk.Label(root, text="Password Complexity:")
complexity_label.pack(pady=10)

# Dropdown for password complexity
complexity_var = tk.StringVar(value="Low")
complexity_options = ["Low", "Medium", "Strong"]
complexity_menu = tk.OptionMenu(root, complexity_var, *complexity_options)
complexity_menu.pack(pady=10)

# Button to generate password
generate_button = tk.Button(root, text="Generate Password", command=generate_password)
generate_button.pack(pady=10)

# Entry to display the generated password
password_entry = tk.Entry(root, width=40)
password_entry.pack(pady=10)

# Button to copy password to clipboard
copy_button = tk.Button(root, text="Copy to Clipboard", command=copy_to_clipboard)
copy_button.pack(pady=10)

# Run the application
root.mainloop()
