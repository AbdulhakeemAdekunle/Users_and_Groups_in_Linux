### Step 1: Create a user

To create a user, we use the `useradd username` command.  
`useradd abdulhakeem`: This will create a new user called abdulhakeem
![create a user](./images/create%20user.png)

We can confirm the entry in the `/etc/passwd` file
![confirm user entry](./images/confirm%20user%20entry.png)

### Step 2: Set an expiry date of 2 weeks for the user

After creating a user, to modify or change some of the user attributes, we use the `usermod [options] username` command.  
`usermod -e DATE abdulhakeem`: This will set the expiry date of abdulhakeem’s user account to the DATE specified.
![set user expiry date](./images/set%20user%20expiry%20date.png)

To confirm the expiry date of the user account we can use: `chage -l username`
![confirm user expiry date](./images/confirm%20expiry%20date.png)

### Step 3: Prompt the user to always change its password on each login

To set or change a user account password, we use the `passwd [options] username` command. The `option` to use in this case will be that which will set the user’s password to expire, so that after each login the current password expires automatically and will require a new password on the next login.  
`passwd -e abdulhakeem`
![set password expiry date](./images/set%20password%20expiry%20date.png)

The `passwd -e abdulhakeem` was used to set the password expiry date, then we run `chage -l abdulhakeem` to check the account aging information and it clearly shows that our password has expired by informing us that **"password must be changed"**, we then tried to switch to abdulhakeem user and it shows some information on the screen: **“You are required to change your password immediately (administrator enforced)”** prompting us to change the password.

### Step 4: Attach the user to a group called altschool

To attach a user to a group, we first need to create the group, and then modify the user by adding it to the group.

To create a group, we use the `groupadd` command.  
`groupadd altschool`: This will create a group called altschool
![create altschool group](./images/create%20a%20group.png)  
We can confirm the group entry in the /etc/group file
![confirm group entry](./images/confirm%20group%20entry.png)  
Then attach the user to the group using the usermod [OPTION][GROUPS] username command  
`usermod -aG altschool abdulhakeem`: This will -a append abdulhakeem user to altschool -G group members.
![add user to group](./images/attach%20user%20to%20a%20group.png)
We have been able to create our group, added a user to it, and confirm the entry in `/etc/group` file.

### Step 5: Allow altschool group to be able to run only cat command in the /etc directory.

To set a specific access right for users or group on a particular directory, it is required that such access be defined in the `/etc/sudoers` file.
From the terminal: cd into /etc directory `cd /etc` then: do `sudo vi sudoers` this opens the sudoers file with a text editor, then you can append the rule on a new line, if you wish you can also add comments above as shown in the example below `%altschool ALL=(ALL) /bin/cat /etc/*` and save the file.
![set privilege permission](./images/set%20group%20sudo%20privilege.png)

To confirm that the privilege access we gave to altschool members was applied, we can switch to the user and try to cat the `etc/sudoers` file.
![confirm sudo privilege](./images/test%20group%20privilege.png)

### Step 6: Create another user. make sure that this user doesn't have a home directory.

To create a user without a home directory, we use `useradd -M username command`. Alternatively we can also use `useradd username` as this is the default behavior of the useradd command, it doesn’t create a home directory for the user unless it is specified with the `-m` option. But we will use the first option here.  
`useradd -M adekunle`
![create user without home directory](./images/create%20user%20without%20home%20directory.png)
