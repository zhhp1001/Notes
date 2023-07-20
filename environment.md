
Logging out and back in would apply the changes – and in fact you must do this if you want all your processes to receive the new environment. All other "solutions"2 will only apply the environment to the single shell process, but not to anything you launch through the GUI including new terminal windows.1


/etc/environment is not part of POSIX, it belongs to PAM (Pluggable Authentication Module), and only programs compiled with PAM support are able to use it (primarily login systems, which subsequently start the shell or user environment). This means it isn't even read by your shell.

You can see the programs using /etc/environment with grep -l pam_env /etc/pam.d/*.

So /etc/environment is used for setting variables for programs which are usually not started from a shell.




https://superuser.com/questions/339617/how-to-reload-etc-environment-without-rebooting

https://unix.stackexchange.com/questions/130985/if-processes-inherit-the-parents-environment-why-do-we-need-export