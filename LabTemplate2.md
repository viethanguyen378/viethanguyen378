## Lab 02

- Name: Thi Viet Ha Nguyen
- Email: nguyen.378@wright.edu

## Part 1 Answers

Full / absolute path to your private key file: 
/Users/vietha/.ssh/labsuser.pem

Command to SSH to AWS instance:
``` ssh -i /Users/vietha/.ssh/labsuser.pem ubuntu@52.54.185.226

## Part 2 Answers

1. `chmod u+r bubbles.txt`
    - Means: Give the user read permission on bubbles.txt.
    - Assessment: The goal is to ensure the file the user can read the file
2. `chmod u=rw,g-w,o-x banana.cabana`
    - Means: Set the user permissions to read and write, remove write permission from the group, remove execute permission from others for banana.cabana
    - Assessment: The goal is to make the file readable or writable, restrict group to read-only, and restrict others from executing
3. `chmod a=w snow.md`
    - Means: Give write-only permission to all on snow.md. Removes all other permissions.
    - Assessment: Users can write (overwrite) but cannot read or execute (not typical for normal files)
4. `chmod 751 program`
    - Means: User has full permissions (read, write, execute), group has read and execute, and others have execute only
    - Assessment: The goal is to allow the user full permissions, group limited access, and others only the ability to run the program
5. `chmod -R ug+w share`
    - Means: Recursively give write permission to user and group for the share directory and all of its contents
    - Assessment: The goal is to allow both the owner and group members to write to everything under share

## Part 3 Answers

1. Command to create new user: sudo adduser bob
2. Path to new user's home directory: /home/bob
3. Evaluate if `ubuntu` can add files to new user's home directory: I cannot add files because /home/bob is owned by bob and usually not writable by others
4. Command to switch to new user: su - bob
5. Command(s) to go to new user's home directory: cd /home/bob
6. Evaluate if new user can add files to user's home directory: No, because /home/ubuntu is owned by ubuntu and not writable by bob
7. Command to return to `ubuntu` user: exit
8. Command to return to `ubuntu` home directory: cd /home/ubuntu

## Part 4 Answers

1. Command(s) to create group named `squad` and add members:
sudo groupadd squad
sudo usermod -aG squad bob
sudo usermod -aG squad ubuntu
2. Command(s) to add `ubuntu` & user to group `squad`: I used the usermod -aG command. The -a flag means append (so existing groups are not removed), and the -G flag specifies the target group.
3. Command(s) to allow `squad` to view the `ubuntu` user's home directory contents: sudo setfacl -m g:squad:rx /home/ubuntu
4. Command(s) to modify `share` to have group ownership of `squad`: sudo chgrp -R squad /home/ubuntu/share
5. Describe your tests and commands with the user account: 
Logged in as `bob`, tried listing `/home/ubuntu` → success after group permission added
Created/edit file inside `/home/ubuntu/share` to confirm group `squad` access
6. Describe the full set of permissions / settings that enable the user to make edits:
Group ownership of `share` set to `squad`.
Write permission for group on `share` (chmod -R g+w /home/ubuntu/share)
`bob` is added to `squad`

## Part 5 Answers

For each, write the command used or answer the question posed.

1. Command(s) to make file using `sudo`: sudo touch madewithsudo.txt
2. Command(s) to make file with `root`: 
sudo su -
touch madebyroot.txt
3. Describe / compare ownership and permissions of files:
`madewithsudo.txt` was created with `sudo` but in `bob`’s home (owned by root, group root)
`madebyroot.txt` created in `/root` (owned by root, group root)
After `chmod`, ownership and permissions can be reassigned.
4. Which account can do what actions? (Type Y or N in columns)

Contents inside of `share`
| Account   | Can View  | Can Edit  | Can Change Permissions    |
| ---       | ---       | ---       | ---                       |
| `root`    | Y         | Y         | Y                         |
| `ubuntu`  | Y         | Y         | Y (if user)               |
| `BOB`     | Y (after added to squad)    | Y (if g+w)          |     N  |
`madewithsudo.txt`
| Account   | Can View  | Can Edit  | Can Change Permissions    |
| ---       | ---       | ---       | ---                       |
| `root`    |  Y        | Y         |  Y                        |
| `ubuntu`  |  Y (after chmod) | Y  |  Y ( if user)             |
| `BOB`     |  Y        |  N ( unless permissions changed)   |  N        |

5. Command(s) to modify permissions:
sudo chmod 664 /home/bob/madewithsudo.txt
sudo chmod 644 /home/bob/madebyroot.txt
6. How to give user account `sudo`: sudo usermod -aG sudo bob


## Citations

To add citations, provide the site and a summary of what it assisted you with.  If generative AI was used, include which generative AI system was used and what prompt(s) you fed it.

