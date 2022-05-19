cyber apocalypse 2022 (CTF writeup)

this challenge was about finding a flag using reverse engineering.when you download the rev_wide zip file you have to unzip it via command line:

unzip rev_wide.zip

it gives you rev_wide folder where 2 files(wide and db.ex) are placed.

lets see what they can do by executing wide file with db.ex, just like shown below:


it gives us list of files and very last one has star on encrypted field.that’s interesting. let’s try to open it up.


by typing file’s name it says ‘our home dimension’ which is not very useful. now let’s try to open it by row number.since in programming we start counting from 0, use number 6 instead of number 5.but when i typed 6 it wanted wide decryption key which we don’t have.

so lets open wide file with radare2.


type in aaaa and then afll. It will list the functions of the binary in a verbose mode and in an easy to understand table:


in name field we see main. it should be interesting so open it up with command: pdf @ main


by typing pdf main we check what’s placed in main function
if we scroll down we can see weird function named sym.menu. i wonder what it’s going to do. so to check we type in command pdf @ sym.menu


if we scroll down to take a look and understand what it does we can see this weird, odd looking string sup3rs3cr3tw1d3


so let’s see if that’s the key we are looking for. exit radare2 by typing: quit

and open up wide with db.ex instead


and here is our flag.