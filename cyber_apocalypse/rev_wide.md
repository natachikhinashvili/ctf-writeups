cyber apocalypse 2022 (CTF writeup)

![Screenshot 2022-05-19 at 16 51 14](https://user-images.githubusercontent.com/86610861/169398124-e3dcd894-f916-4e06-8393-fd42e43e584e.png)

this challenge was about finding a flag using reverse engineering.when you download the rev_wide zip file you have to unzip it via command line:

unzip rev_wide.zip

it gives you rev_wide folder where 2 files(wide and db.ex) are placed.

lets see what they can do by executing wide file with db.ex, just like shown below:

![Screenshot 2022-05-19 at 20 28 51](https://user-images.githubusercontent.com/86610861/169398218-0687e3ae-c08b-43bd-b1f4-f93353648c66.png)


it gives us list of files and very last one has star on encrypted field.that’s interesting. let’s try to open it up.

![Screenshot 2022-05-19 at 20 30 38](https://user-images.githubusercontent.com/86610861/169398266-46f5de15-587e-4ecc-b80a-e15bb4dded65.png)

by typing file’s name it says ‘our home dimension’ which is not very useful. now let’s try to open it by row number.since in programming we start counting from 0, use number 6 instead of number 5.but when i typed 6 it wanted wide decryption key which we don’t have.

so lets open wide file with radare2.


type in aaaa and then afll. It will list the functions of the binary in a verbose mode and in an easy to understand table:

![Screenshot 2022-05-19 at 20 44 22](https://user-images.githubusercontent.com/86610861/169398447-efb9ead5-9861-41c5-bc67-bfdc09410176.png)


in name field we see main. it should be interesting so open it up with command: pdf @ main

![Screenshot 2022-05-19 at 20 45 19](https://user-images.githubusercontent.com/86610861/169398397-1dfa866c-a818-4f13-9de8-a94aec3fc13a.png)


by typing pdf main we check what’s placed in main function

![Screenshot 2022-05-19 at 20 45 44](https://user-images.githubusercontent.com/86610861/169398366-da9eb1a1-eb08-4b51-b485-f7afdf91bb9e.png)

if we scroll down we can see weird function named sym.menu. i wonder what it’s going to do. so to check we type in command pdf @ sym.menu


if we scroll down to take a look and understand what it does we can see this weird, odd looking string sup3rs3cr3tw1d3

![Screenshot 2022-05-19 at 20 46 16](https://user-images.githubusercontent.com/86610861/169398665-696fc8a3-d02a-44ed-8254-84d77bbfa38e.png)


so let’s see if that’s the key we are looking for. exit radare2 by typing: quit

and open up wide with db.ex instead

![Screenshot 2022-05-19 at 20 49 11](https://user-images.githubusercontent.com/86610861/169398552-a0dc0567-c44b-4649-9a6e-95ef9602be53.png)


and here is our flag.
