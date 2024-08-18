# passwordManager
def load_key():
    file = open("key.key", "rb")
    key = file.read()
    file.close()
    return key
Function load_key:
Opens the file key.key in binary read mode ("rb").
Reads the key stored in the file and assigns it to the variable key.
Closes the file after reading.
Returns the key. The key is used later for encryption and decryption.
python
Copy code
key = load_key()
fer = Fernet(key)
Load the key and create a Fernet object:
Calls the load_key() function to retrieve the encryption key.
Creates a Fernet object named fer using the retrieved key. The Fernet object is used for symmetric encryption and decryption, allowing secure handling of passwords.
view Function
python
Copy code
def view():
    with open('passwords.txt', 'r') as f:
        for line in f.readlines():
            data = line.rstrip()
            user, passw = data.split("|")
            print("User:", user, "| Password:", fer.decrypt(passw.encode()).decode())
View function:
Opens the passwords.txt file in read mode ('r').
Reads each line of the file using f.readlines().
Strips any trailing newline characters with rstrip().
Splits each line by the delimiter "|", separating the username (user) and the encrypted password (passw).
Decrypts the password using fer.decrypt(passw.encode()) and decodes it back to a readable string.
Prints the username and decrypted password.
add Function
python
Copy code
def add():
    name = input('Account Name: ')
    pwd = input("Password: ")

    with open('passwords.txt', 'a') as f:
        f.write(name + "|" + fer.encrypt(pwd.encode()).decode() + "\n")
Add function:
Prompts the user to enter an account name (name) and a password (pwd).
Opens the passwords.txt file in append mode ('a'), which adds new content to the end of the file without deleting existing data.
Encrypts the password with fer.encrypt(pwd.encode()) and then decodes it back to a string for storage.
Writes the account name and encrypted password to the file, separated by "|", followed by a newline character.
Main Loop
python
Copy code
while True:
    mode = input("Would you like to add a new password or view existing ones (view, add), press q to quit? ").lower()
    if mode == "q":
        break

    if mode == "view":
        view()
    elif mode == "add":
        add()
    else:
        print("Invalid mode.")
        continue
Infinite loop: Runs until the user decides to quit by pressing "q".
Prompts the user to select a mode: "view" (to view existing passwords), "add" (to add a new password), or "q" (to quit the program).
If the mode is "view", it calls the view() function.
If the mode is "add", it calls the add() function.
If the user enters an invalid mode, it prints "Invalid mode." and continues the loop.
Summary
The code implements a simple password manager that stores account names and encrypted passwords in a file (passwords.txt).
Passwords are encrypted using the Fernet encryption from the cryptography library, and the key used for encryption and decryption is securely stored in a file (key.key).
Users can add new passwords or view existing ones, with all password data being securely encrypted.
