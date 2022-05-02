## Task 1

As suggested we experimented with listing environment variables and setting and unsetting variables.

[Screenshot - Task 1](/screenshots/logbook4-task1.png)

## Task 2

The first program that is given prints a list of environment variables.

[Screenshot - Task 2 - Part 1](/screenshots/logbook4-task2-1.png)

After commenting the printenv() line on the child process case and uncommenting the same line in the parent process case, the program also printed a list of environment variables.

[Screenshot - Task 2 - Part 2](/screenshots/logbook4-task2-2.png)

After using the diff command to compare both output files we arrived at the conclusion that child and parent processes share the same environment variables (since the programs' output was the same).

[Screenshot - Task 2 - Part 3](/screenshots/logbook4-task2-3.png)

## Task 3

The first program program that is given doesn't print out anything.

[Screenshot - Task 3 - Part 1](/screenshots/logbook4-task3-1.png)

After making the changes that are suggested the program prints out a list of environment variables.

[Screenshot - Task 3 - Part 2](/screenshots/logbook4-task3-2.png)

After analyzing the different outputs, as well as the functioning of the execve() system call function we realized that the reason that in the first step there was no output was because the last argument of the execve function is an array of pointers to strings which are passed as the environment of the new program.

Since in the first step no array was passed, the environment wasn't conserved and therefore there was nothing for the /urs/bin/env program to print. When we changed the last argument from NULL to environ (an array of strings) we passed the environment to the new execution which explains the change observed.

## Task 4

As expected the system() function passed the environment variables therefore when we ran it, a list of environment variables was printed.

[Screenshot - Task 4](/screenshots/logbook4-task4.png)

## Task 5

After checking all the environment variables we observed that both the PATH and arbitrary environment variables we had set had been passed down to the Set-UID child process, however the LD_LIBRARY_PATH wasn't set in the Set-UID child process.

[Screenshot - Task 5](/screenshots/logbook4-task5.png)

## Task 6

We compiled the program given to us, changed its ownership to root and made it a Set-UID program. Because we changed the PATH environment variable, by adding the /home/seed directory, when we ran the program given, we were able to run an alternative program also named ls that we wrote ourselves and placed on the /home/seed directory.

[Screenshot - Task 6](/screenshots/logbook4-task6.png)


## CTF

### Challenge 1

As suggested we browsed through the website until we found the version of wordpress that was being used, as well as the versions of the plug-ins. After a few Google searches we found a CVE in the WooCommerce Booster Plugin 5.4.3. We then looked for exploits in the exploit-db.com website and found one that after the executing provided us with a link that would grant us admin access to the website.

## Challenge 2

After having admin website, we accessed the private post and the flag to solve the second challenge.