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

### C. **Log File Analysis with AWK, Grep & Sed**
#### 1️⃣.Create /devops_workspaceUse grep to find all occurrences of the word "authentication failure".

<img width="512" height="585" alt="Screenshot from 2026-02-06 14-26-35" src="https://github.com/user-attachments/assets/6b86220a-5acd-425a-b8f0-34a71a1153a3" />

#### 2️⃣ Use awk to extract timestamps and log levels.

<img width="512" height="585" alt="Screenshot from 2026-02-06 14-31-27" src="https://github.com/user-attachments/assets/a0f913c6-cc37-4d61-9cc1-ebb65105515d" />

#### 3️⃣ Use sed to replace all IP addresses with [REDACTED] for security.

<img width="512" height="586" alt="Screenshot from 2026-02-06 14-38-22" src="https://github.com/user-attachments/assets/444111b8-82f4-4ccb-a125-c74961f9b654" />

#### 4️⃣ Find the most frequent log entry using sort | uniq -c | sort -nr | head -10.


<img width="512" height="517" alt="Screenshot from 2026-02-06 14-42-34" src="https://github.com/user-attachments/assets/9225d5cb-a189-47b9-8efe-21a3ab58f72d" />

### D. **Volume Management & Disk Usage**

#### 1️⃣.Create a volume on aws.

<img width="512" height="768" alt="Screenshot (542)" src="https://github.com/user-attachments/assets/b9b0e1f3-0146-409a-b44a-191f9ea31e9f" />

#### 2️⃣ Create a directory /mnt/devops_data.

<img width="512" height="116" alt="Screenshot (543)" src="https://github.com/user-attachments/assets/54dec6ee-38a3-4284-bdbf-10e41971a0c0" />

#### 3️⃣ Mount a new volume (or loop device for local practice).

<img width="512" height="420" alt="Screenshot (544)" src="https://github.com/user-attachments/assets/01f28605-892c-45a6-b83a-e8c5045d0918" />

#### 4️⃣ Verify using df -h.

<img width="512" height="178" alt="Screenshot (545)" src="https://github.com/user-attachments/assets/63ad0a23-1022-403b-8361-ab24b17a03e1" />

### E. **Process Management & Monitoring**

#### 1️⃣.Start a background process (ping google.com > ping_test.log &).

<img width="512" height="57" alt="Screenshot (547)" src="https://github.com/user-attachments/assets/e5c74d34-fa44-4206-88dd-07e09308e7dc" />

#### 2️⃣ Use ps, top, and htop to monitor it.

1.ps -> ps aux | grep ping


<img width="512" height="84" alt="Screenshot (548)" src="https://github.com/user-attachments/assets/8bbe1b2a-20ba-45f9-b228-4361abc147e5" />

2.top

<img width="512" height="668" alt="Screenshot (549)" src="https://github.com/user-attachments/assets/ffa0668a-1c8f-44f7-b9cb-812d5af2f98a" />

3.htop 

<img width="512" height="702" alt="Screenshot (550)" src="https://github.com/user-attachments/assets/0c36d0b8-f784-48fb-a03b-f9d79283f8d7" />

#### 3️⃣ Kill the process and verify it's gone.

<img width="512" height="172" alt="Screenshot (551)" src="https://github.com/user-attachments/assets/3c909011-b0ad-4ec3-9613-e08b1996a455" />

