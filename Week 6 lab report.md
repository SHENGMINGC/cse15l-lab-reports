# Streamlining ssh Configuration

1) Editing the `.ssh/config` file:

![Image](option1-1.png)

2) Simplified `ssh` command using the new alias:
![Image](option1-2.png)

3) `scp` using the new alias:
![Image](option1-3.png)

# Setup Github Access from ieng6(the user account)

The purpose of this step is to use command line to modify, commit and push  the file.

1) Storing my public key on Github:
![Image](option2-1.png)

2) Storing my public and private key on my user account:
![Image](option2-2.png)

3) Running git commands to commit and push a change to
Github while logged into my user account:
![Image](option2-3.png)

4) Link for the resulting commit:
[link](https://github.com/SHENGMINGC/Josh/commits/main/test-file.md)

# Copy whole directories with scp -r

1) Copying my whole directory to my user account:
![Image](option3-1.png)

2) Logging into my user account and compiling and running the tests:
![Image](option3-2.png)

3) Combining `scp`, `;`, and `ssh` in one line and compile and run: 
![Image](option3-3.png)

