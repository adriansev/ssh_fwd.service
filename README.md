# ssh_fwd@.service
Systemd service for ssh port forwards

# USER usage

enable persistent processes for user   
>sudo loginctl enable-linger <user>

systemd user location is ~/.config/systemd/user/   
>cp <service file> ~/.config/systemd/user/   

add service to systemd --user services autostart
>systemctl --user enable ssh-fwd@my_configuration

user configurations are expected in ~/.ssh/port-fwd.d/   
the configuration have the following format :   
>TARGET=-p custom_port user@host  
>PORT_LOCAL=local_port  
>PORT_REMOTE=remote_port  
>OPTS=any other options  

!!! N.B. !!!
this is not a shell sourced file  
Environment variables in systemd are handled differently if used with ${MYVAR} or with $MYVAR.  
${MYVAR} will provide the target process with a single string argument made of the complete string you specified in MYVAR.  
$MYVAR in the other hand will split MYVAR around spaces it contains and feed them to the process.  
https://www.freedesktop.org/software/systemd/man/systemd.exec.html#EnvironmentFile=   
https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Environment=   

