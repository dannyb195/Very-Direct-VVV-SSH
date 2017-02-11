# Very-Direct-VVV-SSH
This repo provides instructions on allowing for directly ssh-ing into VVV to your currently local directory

#### Note these instruction have only been tested with VVV (https://github.com/Varying-Vagrant-Vagrants/VVV)

##### Thank you to Ben Lobaugh (https://twitter.com/benlobaugh) and Brad Parbs (https://twitter.com/bradparbs) for pointing me in the right direction

## Step 1 (local):
If you do not already have a `bin` dir in your $HOME locally create one:

```cd ~```

```mkdir bin```

## Step b (local):
Create a new file, the file name will be the name of the command you type to execute this script

```cd ~/bin```

```touch <name-of-command--this-is-up-to-you>```

## Step 3 (local):
Open you newly create file in your favorite editor, or VIM and paste

```
#!/bin/bash
local_path=$(pwd);
local_path=${local_path##*www/}; # http://stackoverflow.com/questions/19482123/extract-part-of-a-string-using-bash-cut-split
ssh -t <sshuser>@<domain>.<extension> "export LOCAL=$local_path; bash"
```

## Step IV (local):
Test that this is working by closing your terminal window and opening a new one. If you can tab-complete the name that you chose for the script we can move forward.

## Step 5 (remote server):
SSH into the server you will be using this functionality on, if using VVV the domain is `vagrant@vvv.dev` and the password is `vagrant` or more simply `vagrant ssh`.

## Step VI (remote server):
After ssh-ing in you *should* be in your users home directory, if not simply `cd ~`.

## Step G (remote server):
Open ~/.bashrc in your favorite editor and paste `cd /srv/www/$LOCAL`

Now when (in VVV) you are in a project such as `<your-local>/www/<project-name>/wp-content/plugins` and you run the bash script by typing the name you chose earlier you *should* be taken directly to `/srv/www/<project-name>/wp-content/plugins` within vagrant. 
