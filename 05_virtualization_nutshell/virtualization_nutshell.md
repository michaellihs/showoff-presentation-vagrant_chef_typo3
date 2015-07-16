!SLIDE section_slide
<h1>Virtualization</h1>

<h2>In a Nutshell</h2>



!SLIDE

# No Virtualization

## LAMP, WAMP, MAMP

* install apache, mysql, php "on your machine"
* your development machine "acts as a webserver"

!SLIDE

# PROs

* fairly easy to set up
* fast
* no overhead (diskspace, ram, cpu)

!SLIDE

# CONs

* interferes with your OS
* no production-like environment
* depends on packages for your OS
* big damage if you break it
* not easily disposable



!SLIDE

# Heavy Weight Virtualization

## VMWare Fusion, VirtualBox, Parallels

* full hardware virtualization
* complete isolation of instances
* each vm requires full OS

!SLIDE

# PROs

* well established tools
* production-like environment
* multiple package / OS versions
* every project has its own environment

!SLIDE

# CONs

* cpu, ram and diskspace overhead
* slow(er)
* not-so-easy setup
* filesharing is biggest (?) problem



!SLIDE

# Lightweight Virtualization

## Docker, Jails, Rocket

* container = isolated process
* share kernel with host
* no device emulation
* resource restrictions (ram, cpu, disk, networking)


!SLIDE

# PROs

* little to no overhead
* starts and stops within seconds
* containerization
* fast file shares
* new tools every day


!SLIDE

# CONs

* new tools every day
* very little production usage
* (Docker) only available on some Linux distributions
* legacy applications "don't fit in"



!SLIDE section_slide
<h1>We'll talk about heavy weight virtualization here!</h1>



!SLIDE section_slide
<h1>Through Virtualization Infrastructure becomes</h1>

* manageable through software
* disposable
* hardware independent



!SLIDE section_slide
<h1>VM Management can still be cumbersome...</h1>

* networking
* virtual devices &amp; shares
* bootstraping VMs
* distributing VMs



!SLIDE section_slide
<h1>Here comes Vagrant...</h1>
