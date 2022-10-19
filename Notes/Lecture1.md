# Lecture 1: Shell

Take away:


Command
* double qutotations and single qutotations both can be used in the shell
* shell is actually a programming language (I have written some batch files during daily work)
* environment variables and $PATH
* difference between files system in windows and linux (many roots based on the driver / only one namespace)
* cd / pwd / . (current directory) / .. (parent directory)
* cd ./home (change to the home directory under the current directory)
* ~ (the home directory)
* cd - (change back to the last directory)
* ls -l (permission: owner / group / other useer)
* read and write permission to the directory
* execute permission to the directory (access to the directory, being the parameter of certain command? like cd?)
* mv / cp / rm (not recursive by default) / rmdir (only works on the empty directory) / mkdir
* man (given the detailed documentation of different commands)
* ctrl-l (clear and return back to the top of the shell)
* cat (print the contents of the file, in which format?)
* tail -n1 get the last column.
* tee (redirect the input to the file and the standard output in the meantime)
* xdg-open (sudo apt install xdg-utils)

Stream
* input stream(keyboard -> terminal, output stream(keyboard -> terminal). By default, both streams are the terminal, which be redirected somehow.
* redirect the stream (rewire): < and >. For example, cat < help.txt, redirect the input of the cat program from the terminal to the text file called help.txt (in the current directory). Then what is the difference between cat hello.txt and cat < hello.txt. In the former case, no stream is redirected, so the input comes from the terminal, namely the file name hello.txt, then cat will open (?) print the contents of that file. In the latter case, the input is redirected to the hello.txt file, so the cat will directly prints the contents. >> only appends to the stream instead of creating a new one.
* pipe `|`, takes the input from the left and outputs to the right. e.x: ls -l / | tail -n1. Shell controls the connection of pipe and streams. Pipelines can be used between multiple input and outputs. One more interesting example: `curl --head --silent google.com | grep -i content-length` and `curl --head --silent google.com | grep -i content-length | cut --delimiter=' ' -f2`

Root user:
* with user id 0, which can manimuplate any file. For example, under ubuntu, sudo can be used to execute the command with the super user.
* cd /sys, access the kernal. 
* `sudo echo 500 > brightness` Redirection and pipelines are controlled by the Shell, streams know nothing about each other. In this case, the Shell executes `sudo` program with the arguments of `echo 500` and then redirect the output to the file named brightness. Thus, sudo is not expected to work on accessing to brightness. 
* sudo su (run the Shell as the super user), and then the sign is changed from `$` to `#`, which means the Shell is being run with the super user. 
