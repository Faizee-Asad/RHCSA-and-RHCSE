# Run-levels

* In Linux the current operating state of the OS is known as a **run-level**.
* Run-level defines what all serivces can run on the system.
* Run-levels are known by numbers and there are total 7 run-levels:
```
Run-level 0    used to power-off the server.
Run-level 1    used to rescue a crashed server.
Run-level 2    used to run a linux server with minimal services (w/o networking)
Run-level 3    used to run a full-fledged Linux server but w/o graphics
Run-level 4    unused
Run-level 5    used to run a linux server with graphics
Run-level 6    used to reboot server.
```
[Introduction to Linux Runlevels](https://www.youtube.com/watch?v=LPu3IZwbOA8)

* To know previous and current run-level
```
# runlevel
5(previous) 3(current)
```

* To switch to a run-level
```
# init 3
```

# Targets
* In lastest linux kernels running with system , run-levels are enhanced to targets.
* Targets are known by names.
* The targets available in Linux are:
  1. **halt.target** is equivalent to run-level 0.
  2. **rescue.target** is equivalent to run-level 1. (recovery console with read/write access)
  3. **emergency.target** is equivalent to run-level 1. (recovery console with read-only access)
  4. **multi-user.target** is equivalent to run-level 3.
  5. **graphical.target** is equivalent to run-level 5.
  6. **reboot.target** is equivalent to run-level 6.

* To know current target
```
# runlevel
```

* To switch to a target
```
# systemctl isolate multi-user.target
```
* To know the default target
```
# systemctl get-default
```
```
* Out of all the target, any 1 target will be the default target.
* The default target is the target in which the system boots.
* The default target should be either multi-user.target or graphical.target
```

# Service

* A serivce is a script that is responsible to start, stop or restart process of a program.
* All service files are stored in /usr/lib/systemd/system directory.
* If your server is ruuning with **init** program, **serivce** command is used to manage services.
* If your server is ruuning with **systemd** program, **systemctl** command is used to manage services.
* Service can be started, stopped or restarted in run time.
* We can also enable a service to start automatically when server boots.

* To list all active services
```
# systemctl list-units --type=service
```
* To list all installed services
```
# systemctl list-units --type=service --all
```
* To check status of a service
```
# systemctl status crond
```
* To stop a service
```
# systemctl stop crond
```
* To start a service
```
# systemctl start crond
```
* To restart service
```
# systemctl restart crond
```
* To mask a service
```
# systemctl mask crond
```
* To unmask a service
```
# systemctl unmask crond
```
* To enable a service every system boot
```
# systemctl enable --now crond
```
* To disable a service every system boot
```
# systemctl disable --now crond
```
![1740995466850](https://github.com/user-attachments/assets/3699c5b3-bf9e-4038-8f4c-ff77d6556a09)
