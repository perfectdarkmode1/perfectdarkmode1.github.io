Why you don't run all processes on the same OS
- Blast radius
- Dependency deconfliction
	Different versions of programs
- emulate hardware
	- use different processing architectures. 

Why use containers instead of vms
- Less CPU 
- Less overhead

Do you use Podman more? Does not use Docker
Redhat doesn't support Docker (not in repos)

podman feature complete with docker including docker compose
kubernetes does not work with docker?

docker runs a daemon as root on system

kubernetes doesn't work with docker anymore
kubernates = manage containers and resources, smart enought to move containers around to best use resources in a cluster. 
not including paravirtualization drivers
just running the process you want to run in 
