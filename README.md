# Wayland GDK (DPI) SCALE
## Workaround for GDK_DPI_SCALE and GDK_SCALE plasmashell (Plasma with Wayland)

These are 2 simple workarounds to handle GDK scaling problems with Plasma/Wayland.

First you should type the following:

    echo $DESKTOP_SESSION

If "wayland" appears and not "x11" then it might be worthwhile for you to read on here!

If you think you can solve the problem with a sh-file or profile, you are wrong. These scaling factors are DEFAULT always overwritten, because they were defined in the code to avoid other problems with Wayland - see link (https://invent.kde.org/plasma/plasma-workspace/-/blob/e6cab5d96f7b51a5cf4be3d93a7e2d4fee1cddae/startkde/startplasma-wayland.cpp#L64).


Therefore you should not be surprised that when you type

    printenv | grep GDK

you will see this most of the time:

    GDK_DPI_SCALE=1
    GDK_SCALE=1

Now there are 2 useful workarounds

## #1 Redirect GDK to x11.
Attention Xwayland must be running for this workaround.
please enter:

    ps -ef | grep "Xwayland" | grep -v "grep" | wc -l
    
  0 as result is bad - it should be read here (https://wiki.archlinux.org/title/wayland#XWayland) to find a solution!
  1 as result is great, you are on the right way, it gets warmer! °)

Now open the .bash_profile file with e.g. the following command

    nano ~/.bash_profile

and add the following line

    export GDK_BACKEND=x11
  
close / log out / log in / done
Now that an x11 environment is used with the help of Xwayland the scaling should have adjusted. 
### Note: Regarding Security: XWayland is an X Server, so it does not have the security features of Wayland!

## #2 With a script from me 4kDPI (https://github.com/MTrage/4kDPI)
you can easily access single programs, which you call directly, e.g. via a SH-file, and force a scaling under Wayland. Furthermore 4kDPI can create a startup script for you, which is very useful if you don't want to configure 1 or 2 programs but several.
### This is not a global solution like the #1, but the solution #2 has a big advantage, because it keeps the Wayland security features!
