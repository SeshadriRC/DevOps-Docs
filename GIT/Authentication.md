- Settings --> ssh and gpg keys --> New ssh key -> then copy and paste the public key from your terminal

<img width="1842" height="823" alt="image" src="https://github.com/user-attachments/assets/c65248a5-d205-4410-b799-5a677f1b2000" />

<img width="1308" height="106" alt="image" src="https://github.com/user-attachments/assets/9d58ad98-289a-4b47-8462-625e0f30f777" />

```bash
# Before
root@LAPTOP-QMBUJPPJ:~/httpd# git remote -v
origin  https://github.com/SeshadriRC/dummy-role.git (fetch)
origin  https://github.com/SeshadriRC/dummy-role.git (push)

# Set url from https to ssh
git remote set-url origin git@github.com:SeshadriRC/dummy-role.git

# After
root@LAPTOP-QMBUJPPJ:~/httpd# git remote -v
origin  git@github.com:SeshadriRC/dummy-role.git (fetch)
origin  git@github.com:SeshadriRC/dummy-role.git (push)

Now we can push and do whatever we can
```
