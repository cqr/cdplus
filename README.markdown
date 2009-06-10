cd+
===

Intro
-----

I love BASH. I use it daily, for several hours at a time. It's
fantastic. Part of what I love most about it is my ability to
set up my workflow very, very efficiently by setting up shortcuts
for the things that I do most often.

The builtins are more complicated, and cd is the first one that
comes to mind. You can set up flags with an alias like ``cd -flags``
but you cannot set up anything to come after your arguments, such as
additonal commands.

So I threw together this little hack, which takes advantage of the
directory stack, a rarely used set of commands (``pushd`` and ``popd``),
so that you can set up a sequence of commands. I like to follow every
cd with an ls, so that is the default configuration. I intend to flesh
this out a little bit more, so that you can set up multiple aliases.

Usage
-----

The easiest way to use this script right now is not terribly easy,
so I will give you a quick rundown. Hopefully, I will be able to
make this a little bit easier to use. Please note that if you use
the command-line often, you should have no problems, and find this
very, very easy.

First, you will need to put the file somewhere. I don't know, somewhere
in PATH might be easiest, but you can also put it in a hidden directory
in your home directory. For the sake of argument, let's say it's in
.cdplus in your home directory.

    cd ~
    mkdir .cdplus
    mv cdplus .cdplus/

Next, you should crack open your .bashrc file, which is in your home
directory. If you are using OS X, you can either make these changes in
your .bash_profile instead, or add ``source ~/.bashrc`` to your
.bash_profile file. I would suggest the latter, but I'm a linux guy.

Oh, so your .bashrc file. I like ``vim`` for text editing, but you can
use whatever.

    cd ~
    vim .bashrc

Scroll all the way to the bottom and add the following line (you should
change this to reflect where you put your copy of cdplus. If it's in PATH,
you can just put ``cdplus``)

    source ~/.cdplus/cdplus

So now, you can stop if you like. You need to log out and back in for
everything to take effect, or you can type ``source .bashrc``. But all
this has gotten you is the cdplus command, which is a bear to type out, so
let's add a couple more lines:

    alias cd="cdplus"
    alias cdq="cdplus -q"

You will need to log out again, or type out the source command again, to
make your aliases take effect, but what this has bought you is pretty neat.

If you type ``cd .cdplus``, you will get a directory listing automatically
once the directory is changed. So you should see something like this:

    ~$ cd .cdplus
    cdplus*
    ~/.cdplus$ 

You can change what happens after you cd by editing cdplus in this directory.
This will likely be changed soon, so you can do everything without having to
edit that file, but why glorify a hack?

If you need to go back to standard cd (i.e. no directory listing), just use
the cdq alias we created or pass the -q (quiet) flag to cdplus (or cd).

Closing
-------

Hope you have enjoyed this brief foray into bash scripting. I'm trying to make
this _very_ easy for beginners to fall in love with the command-line as I have,
as it makes things far more efficient for systems-aministration tasks.

I also want to make clear that this probably is not the best way to do this, but
it's the only way that I was able to figure out,  and it has served me well for a
little while. You can also make it much more efficient by choosing not to cater to
all conditions, as I have, which is totally cool. Maybe this would suffice for you:

    function cd(){
      pushd "$1" > /dev/null
      ls
    }

If so, you are encouraged to go that route. This may not be the only way to get
this functionality. If you have a better way, please let me know, and publish it,
cause I had to make this up, I wasn't able to find anything on the 'net.
