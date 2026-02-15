# ⭐Week 3 Challenge 1: User Account Management <br>

## Tasks <br>

### Part 1: Account Creation

1.Implement an option -c or --create that allows the script to create a new user account. The script should prompt the user to enter the new username and password.

2.Ensure that the script checks whether the username is available before creating the account. If the username already exists, display an appropriate message and exit gracefully.

3.After creating the account, display a success message with the newly created username.

#### Shell-script

<img width="512" height="713" alt="Screenshot (553)" src="https://github.com/user-attachments/assets/80fda964-7346-4e0b-a1d8-160655b84878" />

#### Output

<img width="512" height="713" alt="Screenshot (553)" src="https://github.com/user-attachments/assets/68fc6020-72b1-4adc-b705-393af0a1a7db" />

### Part 2: Account Deletion

1.Implement an option -d or --delete that allows the script to delete an existing user account. The script should prompt the user to enter the username of the account to be deleted.

2.Ensure that the script checks whether the username exists before attempting to delete the account. If the username does not exist, display an appropriate message and exit gracefully.

3.After successfully deleting the account, display a confirmation message with the deleted username.

#### Shell-script

<img width="512" height="721" alt="Screenshot (557)" src="https://github.com/user-attachments/assets/729ed6cb-a4e8-4909-ad1b-73a847d95379" />

#### Output

<img width="512" height="267" alt="Screenshot (556)" src="https://github.com/user-attachments/assets/fe853f73-aba3-4f9d-9f5e-d1e0b421ca61" />

### Part 3: Password Reset

1.Implement an option -r or --reset that allows the script to reset the password of an existing user account. The script should prompt the user to enter the username and the new password.

2.Ensure that the script checks whether the username exists before attempting to reset the password. If the username does not exist, display an appropriate message and exit gracefully.

3.After resetting the password, display a success message with the username and the updated password.

#### Shell-script

<img width="512" height="475" alt="Screenshot (559)" src="https://github.com/user-attachments/assets/ba7d1ec6-008d-41de-b40b-43a2efe7d48b" />

#### Output

<img width="512" height="202" alt="Screenshot (558)" src="https://github.com/user-attachments/assets/2b4188b9-e3d4-4bd9-82dc-4bee3aeb3323" />

### Part 4: List User Accounts

1.Implement an option -l or --list that allows the script to list all user accounts on the system. The script should display the usernames and their corresponding user IDs (UID).

#### Shell-script

<img width="512" height="229" alt="Screenshot (561)" src="https://github.com/user-attachments/assets/e3d7e27b-3ed8-4086-b9c8-aa44faf8e327" />

#### Output

<img width="512" height="656" alt="Screenshot (560)" src="https://github.com/user-attachments/assets/9d9b726b-199d-49c8-8add-0a83fa70bf5d" />

### Part 5: Help and Usage Information

1. Implement an option -h or --help that displays usage information and the available command-line options for the script.

#### Shell-script

<img width="512" height="495" alt="Screenshot (562)" src="https://github.com/user-attachments/assets/3b72a5a4-88e7-4def-8dc3-cd2fa453ab0c" />

#### Output

<img width="512" height="393" alt="Screenshot (563)" src="https://github.com/user-attachments/assets/b438fe26-b208-4056-b017-fd389251add9" />

# ⭐ Week 3 Challenge 2: Automated Backup & Recovery using Cron <br>

## Tasks <br>

Your task is to create a bash script that takes a directory path as a command-line argument and performs a backup of the directory. The script should create timestamped backup folders and copy all the files from the specified directory into the backup folder.

Additionally, the script should implement a rotation mechanism to keep only the last 3 backups. This means that if there are more than 3 backup folders, the oldest backup folders should be removed to ensure only the most recent backups are retained.

<img width="512" height="393" alt="Screenshot (564)" src="https://github.com/user-attachments/assets/44f90ba2-c37e-465b-8ead-fd49ecbd0a18" />

<img width="512" height="730" alt="Screenshot (565)" src="https://github.com/user-attachments/assets/0ef1df46-d9e4-4bff-a648-a9be6db3e3b3" />








