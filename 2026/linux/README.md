# ⭐Week 2: Linux System Administration & Automation <br>

## Tasks

### A. **User & Group Management**

Create a user devops_user and add them to a group devops_team.

#### 1️⃣ Create group devops_team

<img width="512" height="172" alt="Screenshot (534)" src="https://github.com/user-attachments/assets/18de4822-b181-4873-9f7f-06f971f97137" />

<img width="512" height="46" alt="Screenshot (535)" src="https://github.com/user-attachments/assets/aec5b118-b6dc-450f-a801-6599b9167950" />

#### 2️⃣ Create user devops_user and add to group

<img width="512" height="115" alt="Screenshot (536)" src="https://github.com/user-attachments/assets/fddea1a4-08ac-4634-963c-66310e92926b" />

<img width="512" height="114" alt="Screenshot (537)" src="https://github.com/user-attachments/assets/539be666-f940-44f9-86e2-4adfab72d9c3" />

#### 3️⃣ Set password for devops_user

<img width="512" height="72" alt="Screenshot (538)" src="https://github.com/user-attachments/assets/b289f055-3a2e-4753-a22f-515d26db634f" />

#### 4️⃣ Grant sudo access
-commands
$sudo usermod -aG sudo devops_user

$su - devops_user
sudo whoami

#### 5️⃣ Restrict SSH login for certain users

Edit SSH config:

$sudo nano /etc/ssh/sshd_config

Allow only a group 

$AllowGroups devops_team

### B. **File & Directory Permissions**


#### 1️⃣.Create /devops_workspace

  command-> mkdir devops_workspace
  
<img width="512" height="67" alt="Screenshot (539)" src="https://github.com/user-attachments/assets/7e029fa4-14b7-4fb3-95ef-a0fcba9e39d8" />

#### 2️⃣ Create a file project_notes.txt.

 command-> touch project_notes.txt

<img width="512" height="99" alt="Screenshot (540)" src="https://github.com/user-attachments/assets/a145e530-3279-4761-b8ad-4657af17f69e" />

#### 3️⃣ Set permissions: Owner can edit, group can read, others have no access.

#### 4️⃣ Use ls -l to verify permissions

 command-> chmod 640 project_notes.txt

<img width="512" height="112" alt="Screenshot (541)" src="https://github.com/user-attachments/assets/6ef53fb0-4afa-49a5-b460-ea77d385f8fe" />

