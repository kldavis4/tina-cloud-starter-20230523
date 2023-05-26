---
title: Introduction To Linux Commands
slug: introduction-to-linux-commands
image: null
date: 2012-01-23T11:53:53.000Z
author: paul-tero
description: >-
  At the heart of every modern Mac and Linux computer is the “terminal.” The
  terminal evolved from the [text-based computer
  terminals](https://en.wikipedia.org/wiki/VT52) of the 1960s and ’70s, which
  themselves replaced punch cards as the main way to interact with a computer.
  It’s also known as the command shell, or simply “shell.” Windows has one, too,
  but it’s called the “command prompt” and is descended from the MS-DOS of the
  1980s.
categories:
  - Coding
  - Linux
---
At the heart of every modern Mac and Linux computer is the “terminal.” The terminal evolved from the <a href="https://en.wikipedia.org/wiki/VT52">text-based computer terminals</a> of the 1960s and ’70s, which themselves replaced punch cards as the main way to interact with a computer. It’s also known as the command shell, or simply “shell.” Windows has one, too, but it’s called the “command prompt” and is descended from the MS-DOS of the 1980s.

Mac, Linux and Windows computers today are mainly controlled through user-friendly feature-rich graphical user interfaces (GUIs), with menus, scroll bars and drag-and-drop interfaces. But all of the basic stuff can still be accomplished by typing text commands into the terminal or command prompt.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Develop Websites On Linux](https://www.smashingmagazine.com/2009/08/how-to-develop-web-sites-on-linux/)
*   [VI Editor / Linux Terminal Cheat Sheet (PDF)](https://www.smashingmagazine.com/2010/05/vi-editor-linux-terminal-cheat-sheet-pdf/)

Using Finder or Explorer to open a folder is akin to the <code>cd</code> command (for “change directory”). Viewing the contents of a folder is like <code>ls</code> (short for “list,” or <code>dir</code> in Microsoft’s command prompt). And there are hundreds more for moving files, editing files, launching applications, manipulating images, backing up and restoring stuff, and much more.

{{% feature-panel %}}

So, why would anyone want to bother with these text commands when you can use the mouse instead? The main reason is that they are very useful for controlling remote computers on which a GUI is not available, particularly Web servers, and especially Linux Web servers that have been stripped of all unnecessary graphical software.

Sometimes these lean Linux servers are managed through a Web browser interface, such as cPanel or Plesk, letting you create databases, email addresses and websites; but sometimes that is not enough. This article provides a broad introduction to text commands and the situations in which they are useful. We’ll cover the following:

*   Why knowing a few commands is useful;
*   Issuing commands on your own computer;
*   Using SSH to log into your Web server;
*   Getting your bearings: `pwd`, `cd ls`;
*   Viewing and moving files: `cat`, `more`, `head`, `tail`, `mv`, `cp`, `rm`;
*   Searching for files: `find`;
*   Looking through and editing files: `grep`, `vi`;
*   Backing up and restoring files and databases: `tar`, `zip`, `unzip`, `mysqldump`, `mysql`;
*   File permissions: `chmod`.</p>

## Why Knowing A Few Linux Commands Is Useful

As a website developer or server administrator, you would gain a big asset in becoming comfortable with these commands: for website emergencies, to configure a server and for your CV. It can also save you money. Many hosting companies offer fully managed servers but at a high monthly premium. Or else they charge by the hour for technical support.

Perhaps you need to archive some big files or make a change to the <code>httpd.conf</code> file or figure out why your website’s images have suddenly stopped loading. You might not want to pay $50 to your server’s administrator for a five-minute job. This article gives you the tools to make such changes yourself.

And why “Linux” commands? Two main types of servers are available today: Windows and UNIX. UNIX-based servers include Linux (which split off in 1991), Mac OS X (2002) and several more traditional UNIX systems, such as BSD, Solaris and HP-UX. Linux commands are basically UNIX commands and so will run on all of them. In fact, I use the term “Linux” here only because it is more common and less frightening than “UNIX.” Windows servers, on the other hand, have a much smaller market share and are more often controlled through GUIs, such as <a href="https://en.wikipedia.org/wiki/Remote_Desktop_Protocol">Remote Desktop</a> and <a href="https://en.wikipedia.org/wiki/Virtual_Network_Computing">VNC</a>, rather than the command line.

In fact, a November 2011 survey showed that <a href="https://news.netcraft.com/archives/2011/11/07/november-2011-web-server-survey.html">Apache accounted for about 65% of all Web servers</a>. Apache usually runs in the popular LAMP configuration: Linux, Apache, MySQL and PHP. Microsoft was a distant second, with 15%. Third place nginx runs on Linux, UNIX, Mac and Windows. So, the commands in this article will work on at least two thirds of all servers.</p>

## Issuing Commands To Your Own Computer

You can quickly experiment with text commands on your own computer. On Mac with OS X, go to Applications → Utilities, and run Terminal. On a PC with Windows, go to Start → All Programs → Accessories, and choose “Command Prompt.” On Ubuntu Linux, go to Applications → Accessories, and choose Terminal.

On Windows you should see this:

<img class="116394" title="Windows Command Prompt" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71b38912-069e-4c49-bd70-06fe5bfc5a36/command-prompt.png" alt="" width="500" /><br>
<em>The Windows command prompt</em>

This is the command line (i.e. shell, prompt or terminal) on your own computer. You can type <code>dir</code> on Windows or <code>ls</code> on Linux or Mac followed by “Enter” to see a list of the files in the current “directory” (i.e. folder, location or path).

All we will be doing for the rest of this article is opening up one of these terminals on a remote computer: your Web server.

You may have used VNC or Remote Desktop, which allow you to actually view the desktop on someone else’s computer: your screen shows their screen, your mouse controls their mouse, your keyboard mimics their keyboard.

The terminal is similar to this but without the fancy menus or scroll bars. If you were to plug a keyboard and screen into your Web server, sitting in a fireproof basement somewhere, you would probably see one of these terminals, waiting patiently for your user name and password.</p>

## Using SSH To Log Into Your Web Server

The application SSH, or Secure Shell, is used to log into Web servers. It often takes the same user name and password as FTP, but it has to be allowed by your host. If you have a dedicated Web server, it is probably already allowed. If you use cloud hosting, then you might need to request it first. If you are on [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222), you’ll definitely need to request it, and the administrator may refuse.

On Linux or Mac, open up Terminal as described above and type the following:

<pre><code class="language-php">ssh -l username www.myserver.com</code></pre>

The <code>-l</code> stands for “log in as,” and your user name goes after it. If SSH is allowed, then it will ask for a password. If not, you’ll get an error message, like this one:

<img loading="lazy" decoding="async" class="116396" title="SSH Command and Connection Error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe7c5806-c40f-48a5-a002-1a70057ad82d/home-ssh-to-smashing.png" alt="SSH Command and Connection Error" width="500" /><br>
<em>Running the <code>ssh</code> command and being denied access</em>

On Windows, you will need to download some SSH software. <a href="https://www.putty.org/">Putty</a> is a popular and easy choice. It downloads as a single EXE file, which you can save to your desktop and run right away. Type your website as the host name, check the SSH box under “Connection Type,” and click “Open.” It will ask for your user name and then your password.

<img class="116398" title="Running Putty on Windows" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97c7fa02-622e-4c2d-98d7-c07ed16cfd13/linux-commands-putty.png" alt="Running Putty on Windows" width="458" height="441" /><br>
<em>Running Putty on Windows in order to SSH to your Web server</em>

Once successfully logged in, you will usually see a welcome message. After that, you will be presented with a few letters and a <code>$</code> sign (or a <code>#</code> sign if you have logged in as root). The letters often represent your user name and where you’ve come from, or the name of the server. A <code>~</code> indicates that you are in your home directory. The <code>$</code> is the prompt; it indicates that you can start typing commands now, something like:

<img loading="lazy" decoding="async" class="116399" title="Successful SSH to a server" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ab0607-bd7c-4cfa-9760-d5834feeacd2/home-ssh-successful.png" alt="Successful SSH to a server" width="500" /><br>
<em>A successful SSH log-in to a Web server. The <code>$</code> means we can start typing commands.</em>

The next section introduces a few basic commands.

## Getting Your Bearings

On Windows, when you go to “My Documents” from the Start menu, it opens your “My Documents” directory in Windows Explorer and shows the contents. If some nosy colleague walked by and asked “What directory are you in?” you could say “I’m <em>in</em> my documents.”

If you SSH’ed to a server as the user “admin,” you would land <em>in</em> admin’s home directory, probably <code>/home/admin</code>. You can verify this by typing the command <code>pwd</code>, which shows your current location (i.e. folder, directory or path).

<img loading="lazy" decoding="async" class="116454" title="The pwd and ls commands" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3932c9c3-dc8a-4442-9cdf-736e2560c057/ssh-pwd-cd-base2.png" alt="The pwd and ls commands" width="500" /><br>
<em>The <code>pwd</code> command tells you where you are, <code>cd</code> changes the directory and <code>ls</code> shows the contents of a directory.</em>

To change to another directory, use the <code>cd</code> command with the destination, like so:

<pre><code class="language-php">cd /</code></pre>

This will change the directory to <code>/</code>, the top of the whole UNIX directory structure. The command <code>ls</code> lists the contents of the current directory, in this case <code>/</code>.

In the screenshot above, the terminal is color-coded. Dark-blue entries are subdirectories, and black entries are files. A lot of the interesting stuff on Web servers happens in the <code>/etc</code>, <code>/home</code> and <code>/var</code> directories. Using just <code>cd</code> and <code>ls</code>, you can explore your server and find out where stuff is.

When using <code>cd</code>, you can specify the new directory absolutely (beginning with a slash, like <code>/var/www</code>) or relative to your current location (without the initial slash). You can also go up a directory with two dots. Practice with the sequence below, pressing “Enter” after each command. Can you guess what the last command will tell you?

<pre><code class="language-php">cd /var
ls
cd www
ls
cd ..
pwd</code></pre>

## Viewing And Moving Files

On many Linux servers, websites are located in <code>/var/www/vhosts</code>. You can check on your server by doing the following:

<pre><code class="language-php">cd /var/www/vhosts
ls</code></pre>

If you see a list of websites, you can move into one of them. Within the website’s main directory, you will probably see the same files that you see when you FTP to the website, things such as <code>httpdocs</code> (where your website’s files are), <code>httpsdocs</code> (if you have a separate secure website), <code>conf</code> (configuration files), <code>statistics</code> (logs and compiled statistics), <code>error_docs</code>, <code>private</code> and more.

You can then change into your website’s public-facing directory, which is <code>myserver.com/httpdocs</code> in this example:

<pre><code class="language-php">cd myserver.com
ls
cd httpdocs
ls</code></pre>

Now you have arrived, and you can run a new command, <code>cat</code>, which displays the contents of a file. For instance, if you have an <code>index.html</code> file, run:

<pre><code class="language-php">cat index.html</code></pre>

If your <code>index.html</code> file is more than a few lines long, it will rush past in a blur. You can use the <code>more</code> command to show it slowly, one page at time. After you type the command below, it will show you the first page. You can press the space bar to show the next page, “Enter” to show the next line, and Q to quit.

<pre><code class="language-php">more index.html</code></pre>

You can also show just the first few or last few lines of a file with the <code>head</code> and <code>tail</code> commands. It shows 10 lines by default, but you can pass in any number:

<pre><code class="language-php">head index.html
tail -20 index.html</code></pre>

If you would like to rename this file, use the <code>mv</code> command, short for “move”:

<pre><code class="language-php">mv index.html indexold.html</code></pre>

Similarly, the <code>cp</code> is the copy command, and <code>rm</code> removes files.

<pre><code class="language-php">cp index.html indexold.html
rm indexold.html</code></pre>

Below is a string of commands in action. In order, it confirms the current directory with <code>pwd</code>, looks at the contents with <code>ls</code>, views <code>index.html</code> with <code>cat</code>, then renames it with <code>mv</code>, and finally removes it with <code>rm</code>, with a lot of <code>ls</code> in between to show the changes.

<img loading="lazy" decoding="async" class="116455" title="The cat and mv commands" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f09a1486-28fd-4df7-bea1-97dd80f0b5f9/ssh-cat-mv-rm.png" alt="The cat and mv commands" width="500" /><br>
<em>The <code>cat</code>, <code>mv</code> and <code>rm</code> commands in action, for displaying, moving and then removing a file.</em>

### More Advanced Tip: Changing the Prompt

Note that in our initial examples, the full prompt included the current directory. For instance, in <code>[admin@myserver /]$</code>, the <code>/</code> indicated that the user was in the <code>/</code> directory. In the example directly above, it was removed, or else it would have crowded the screenshot by constantly saying <code>[admin@myserver /var/www/vhosts/myserver.com/httpdocs]$</code>.

You can change the prompt to whatever you want by setting the <code>PS1</code> environment variable. Here are a couple of examples, the latter including the user, host and current directory:

<pre><code class="language-php">PS1="[woohoooo ]$ "
PS1='[${USER}@${HOSTNAME} ${PWD}]$ '</code></pre>

## Searching For Files

On big websites, files can get lost. Perhaps you vaguely remember uploading a new version of your client’s logo about four months ago, but it has since fallen out of favor and been replaced. Now, out of the blue, the client wants it back. You could download everything from the server using FTP and search the files using Finder or Explorer. Or you could log in and search using the command line.

The <code>find</code> command can search through files by name, size and modified time. If you just give it a directory, it will list everything that the directory contains. Try this:

<pre><code class="language-php">find /var/www</code></pre>

You will probably see lots and lots of file names whizzing past. If you have many websites, it could continue for a couple of minutes. You can stop it by hitting Control + C (i.e. holding down the Control key on your keyboard and pressing the letter C). That’s the way to interrupt a Linux command. A more useful command would be:

<pre><code class="language-php">find /var/www | more</code></pre>

The pipe symbol (<code>|</code>) takes the output of one command (in this case, the long list of files produced by <code>find</code>) and passes it to another command (in this case, <code>more</code>, which shows you one page of files at a time). As above, press the space bar to show the next page, and Q to quit.

To search for a specific file name, add <code>-name</code> and the file name. You can use <code>*</code> as a wild card (the backslash is not always necessary but is good practice with the <code>find</code> command). You can combine searches using <code>-o</code> (for “or”). If you leave out the <code>-o</code>, it becomes an “and.”

<pre><code class="language-php">find /var/www -name logo.gif
find /var/www -name *.gif
find /var/www -name *.gif -o -name *.jpg</code></pre>

You can also search by size by adding <code>-size</code>. So, you could look for all GIFs between 5 and 10 KB:

<pre><code class="language-php">find /var/www -name *.gif -size +5k -size -10k</code></pre>

Similarly, to find a file that was last changed between 90 and 180 days ago, you can use <code>-ctime</code>:

<pre><code class="language-php">find /var/www -name *.gif -ctime +90 -ctime -180</code></pre>

In both of these cases, you will probably also want to know the actual file size and date last changed. For this, you can add <code>-printf</code>, which is similar to the C function <code>printf</code> in that you use the <code>%</code> sign to output various information. This command outputs the file size (up to 15 characters wide), the date and time changed (down to the nanosecond) and the file name:

<pre><code class="language-php">find /var/www -name *.gif -size +5k -size -10k -ctime +90 -ctime -180 -printf "%10s  %c  %pn"</code></pre>

With that whopper, you have hopefully found the missing file. Here is an example:

<img loading="lazy" decoding="async" class="116635" title="Variations on the find command" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23693a17-11cf-41b3-ba84-a126e98f6913/ssh-find.png" alt="Variations on the find command" width="500" /><br>
<em>Searching for all GIFs within a single website, and displaying the file sizes, changed times and file names.</em>

Another useful parameter is <code>-cmin</code>, which lets you see files that have changed in the last few minutes. So, if something goes wrong on a website, you can run this to see everything that has changed in the last 10 minutes:

<pre><code class="language-php">find /var/www -cmin -10 -printf "%c %pn"</code></pre>

This will show files and directories that have changed. Thus, it won’t show files that have been removed (because they are no longer there), but it will show the directories that they were removed from. To show only files, add <code>-type f</code>:

<pre><code class="language-php">find /var/www -cmin -10 -type f -printf "%c %pn"</code></pre>

### More Advanced Tip: Reading the Manual

I didn’t have to remember all of the variations above. I consulted the manual several times, like so:

<pre><code class="language-php">man find</code></pre>

While reading a manual page, the controls are the same as <code>more</code>: space bar for paging, “Enter” to go forward one line and Q to quit. The up and down arrows also work. You can search within a page of the manual by typing <code>/</code> and a keyword, such as <code>/printf</code>. This will jump you to the next occurrence of that term. You can search backwards with <code>?printf</code>, and you can repeat the search by pressing N.</p>

## Looking Through And Editing Files

Most visual code editors allow you to search through many files when you’re looking for a particular variable or bit of HTML. You can also do this directly on the server using the command <code>grep</code>. This is useful when something goes wrong on a complex website with hundreds of files and you have to find the error and fix it fast.

Let’s say you view the HTML source and see that the error happens right after <code>&lt;div id="left"&gt;</code>. You can let <code>grep</code> do the searching for you. Give it the thing to be searched for and the files to search in. These commands change to the website directory and grep through all files ending in <code>php</code>. You need to put quotes around the HTML because it contains spaces, and the inner quotes have to be escaped with backslashes:

<pre><code class="language-php">cd /var/www/vhosts/myserver.com/httpdocs/
grep "&lt;div id="left"&gt;" *.php</code></pre>

This will tell you which files in the current directory contain that bit of HTML. If you want to search in subdirectories, you can use the <code>-r</code> option with a directory at the end, instead of a list of files. The single dot tells it to start in the current directory.

<pre><code class="language-php">grep -r "&lt;div id="left"&gt;" .</code></pre>

Alternatively, you could use the <code>find</code> command from above to tell it which files to look in. To put a command within a command, enclose it in back apostrophes. The following searches only for the HTML in PHP files modified in the last 14 days:

<pre><code class="language-php">grep "&lt;div id="left"&gt;" `find . -name *.php -ctime -14`</code></pre>

You can also add <code>-n</code> to show the line numbers, as in this example:

<img loading="lazy" decoding="async" class="116637" title="Using grep to look for things inside files" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d193d19c-238d-475a-80ef-2d8bae4d2f25/ssh-grep.png" alt="Using grep to look for things inside files" width="500" /><br>
<em>Searching for a bit of HTML within the PHP files in the current directory</em>

And how do you quickly fix an error when you find it? To do that, you will need to start up a Linux text editor. Different editors are available, such as <code>pico</code> and <code>emacs</code>, but the one that is guaranteed to be there is <code>vi</code>. To edit a file, type <code>vi</code> and the file name:

<pre><code class="language-php">vi index.php</code></pre>

<code>vi</code> is a complex editor. It can do most of the amazing things that a fully featured visual editor can do, but without the mouse. In brief, you can use the arrow keys to get around the file (or H, J, K and L on very basic terminals where even the arrow keys don’t work). To delete a character, press X. To delete a whole line, press DD. To insert a new character, press I. This takes you into “insert mode,” and you can start typing. Press the Escape key when finished to go back to “command mode.” Within command mode, type <code>:w</code> to save (i.e. write) the file and <code>:q</code> to quit, or <code>:wq</code> to do both at the same time.

The <code>vi</code> editor also supports copying and pasting, undoing and redoing, searching and replacing, opening multiple files and copying between them, etc. To find out how, look for a good <code>vi</code> tutorial (such as “Mastering the VI Editor”). Note also that on many computers, <code>vi</code> is just a shortcut to <code>vim</code>, which stands for “vi improved,” so you can follow vim tutorials, too.

<img loading="lazy" decoding="async" class="116638" title="The Linux editor vi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85462132-a603-41e0-b832-b47834fa55cd/ssh-vi.png" alt="The Linux editor vi" width="500" /><br>
<em>Editing files with the <code>vi</code> text editor</em>

### More Advanced Tip: Tab Completion

When changing directories and editing files, you might get tired of having to type the file names in full over and over again. The Terminal loses some of its shine this way. This can be avoided with command-line completion, performed using tabs.

It works like this: start typing the name of a file or a command, and then press Tab. If there is only one possibility, Linux will fill in as much as it can. If nothing happens, it means there is more than one possibility. Press Tab again to show all of the possibilities.

For example, if above I had typed…

<pre><code class="language-php">vi i</code></pre>

… And then pressed Tab, it would have filled in the rest for me…

<pre><code class="language-php">vi index.php</code></pre>

… Unless several files started with I. In that case, I would have had to press Tab again to see the options.</p>

## Backing Up And Restoring Files And Databases

Some Linux servers do support the <code>zip</code> command, but all of them support <code>tar</code>, whose original purpose was to archive data to magnetic tapes. To back up a directory, specify the backup file name and the directory to back up, such as:

<pre><code class="language-php">cd /var/www/vhosts/myserver.com/httpdocs/
tar czf /tmp/backup.tgz .</code></pre>

The <code>czf</code> means “create zipped file.” The single dot stands for the current directory. You can also back up individual files. To back up just things changed in the last day, add the <code>find</code> command:

<pre><code class="language-php">tar cfz /tmp/backup.tgz `find . -type f -ctime -1`</code></pre>

Both of these commands put the actual backup file in the temporary <code>/tmp</code> directory — if the backup file is in the same directory that you are backing up, it will cause an error. You can move the file to where you need it afterwards. To see what is in an archive, use the <code>tzf</code> options instead:

<pre><code class="language-php">tar tfz /tmp/backup.tgz</code></pre>

<img loading="lazy" decoding="async" class="116642" title="Linux tar command" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96c9ec00-9b6e-44f9-9c25-913bed814252/ssh-tar.png" alt="Linux tar command" width="500" /><br>
<em>Creating and showing the contents of a backup file using <code>tar</code></em>

To restore things, use <code>xzf</code>, for “extract from zipped file.” First, run a listing as above to check what’s in there, and then restore one or more of the files. The second command restores all of the files from the archive into the current directory:

<pre><code class="language-php">tar xfz /tmp/backup.tgz ./index.php ./test.php
tar xfz /tmp/backup.tgz</code></pre>

If your server has the <code>zip</code> command, then run these commands to do the same thing:

<pre><code class="language-php">cd /var/www/vhosts/myserver.com/httpdocs/
zip -r /tmp/backup.zip .
zip -r /tmp/backup.zip `find . -type f -ctime -1`
unzip -l /tmp/backup.zip
unzip /tmp/backup.zip test.php
unzip /tmp/backup.zip</code></pre>

If your Web server uses MySQL, then you might want to regularly back up your data. For this, there is the <code>mysqldump</code> command. The format of the command is:

<pre><code class="language-php">mysqldump --user="username" --password="password" --add-drop-table database</code></pre>

Replace the user name, password and database with your values. Instead of specifying a database, you can use <code>-A</code> to dump all databases. If you get errors about table locking, you can add <code>--single-transaction</code>. Once you submit the user name and password, this will output a load of SQL in a long blur. To save the output to a file, you will need to use the <code>&gt;</code> symbol. This sends the output of a command to a file.

<pre><code class="language-php">mysqldump --user="username" --password="password" --add-drop-table database &gt; /tmp/db.sql</code></pre>

To restore a database backup, you can use the <code>mysql</code> command. This command lets you run SQL statements from the command line. For example, the following command gets you into the database:

<pre><code class="language-php">mysql --user="username" --password="password" dbname</code></pre>

At the <code>mysql&gt;</code> prompt, you can type an SQL statement such as:

<pre><code class="language-php">mysql&gt; SHOW TABLES;
mysql&gt; SELECT * FROM customers;</code></pre>

For restoring, you’ll need to use the pipe (<code>|</code>), which will send the output from one command into another. In this case, <code>cat</code> will output the database backup file and send it into the <code>mysql</code> command:

<pre><code class="language-php">cat /tmp/db.sql | mysql --user="username" --password="password" dbname</code></pre>

If people are looking over your shoulder while you’re doing this, you might not want to type the password directly into the command. In this case, just leave it out, and <code>mysql</code> or <code>mysqldump</code> will ask for it instead.

<pre><code class="language-php">cat /tmp/db.sql | mysql --user="username" --password dbname</code></pre>

Once you’ve created the database backup file, you can include it in the backups we did above:

<pre><code class="language-php">tar czf /tmp/backup.tgz . /tmp/db.sql</code></pre>

### More Advanced Tip: Hidden Files and Wildcards

Many websites use a file called <code>.htaccess</code> to implement URL rewriting and password protection. In UNIX, all files starting with a single dot are hidden. They won’t show up when you do <code>ls</code>, and they won’t get backed up if you do this:

<pre><code class="language-php">tar czf /tmp/backup.tgz *</code></pre>

The <code>*</code> is a wildcard. Before the command executes, the <code>*</code> is replaced with all non-hidden files in the current directory. To include hidden files as well, it’s better to back up the whole directory as above using a single dot:

<pre><code class="language-php">tar czf /tmp/backup.tgz .</code></pre>

To show hidden files when doing a directory listing, add <code>-a</code> to the command:

<pre><code class="language-php">ls -a
ls -la</code></pre>

## File Permissions

If you use FTP regularly to upload files to websites, then you might be familiar with permissions. All files and directories on Linux (and Mac, Windows and other UNIX systems) have an owner, a group and a set of flags specifying who can read, write and execute them.

The list of user names (and, thus, potential file owners) on a UNIX system is stored in the file <code>/etc/passwd</code>. You can try:

<pre><code class="language-php">more /etc/passwd</code></pre>

The Apache Web server is started by a command when the Web server boots up. But the user who starts Apache is often a restricted and unprivileged user, such as <code>nobody</code> or <code>apache</code> or <code>www-data</code>. This is for security reasons, to prevent someone from hacking into the website and then gaining control of the whole server. You can find out who that user is by running the command below and looking in the first column. The <code>ps aux</code> command shows all of the processes running on the server, and <code>grep</code> shows only processes that contain the word “apache.”

<pre><code class="language-php">ps aux | grep apache</code></pre>

This can cause conflicts, though. If you upload a file to a website via FTP and log in as <code>admin</code>, then the file will be owned by <code>admin</code>. If Apache was started by the user named <code>nobody</code>, then Apache might not be able to read that file and won’t be able to send it to any users who request it when viewing the website. Instead, users will see a broken image or a message such as “403 Forbidden. You don’t have permission to access that file.”

A subtler and more common problem is when an image can be viewed but not overwritten or removed via the website’s content management system (CMS). In this case, the user <code>nobody</code> can read the file but can’t write to it.

You can view permissions using the <code>ls</code> command with an extra <code>-l</code>, like so:

<pre><code class="language-php">ls -l</code></pre>

<img loading="lazy" decoding="async" class="116644" title="ls command with long list format" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b604b52-0941-4295-9cdf-ddf3ef2d9f85/ssh-ls-l3.png" alt="ls command with long list format" width="500" /><br>
<em>The command <code>ls -l</code> shows information about permissions, owners, size and date.</em>

This directory contains three files, with three subdirectories shown in green. The first letter on each line indicates the type: <code>d</code> for directory and <code>-</code> for normal file. The next nine letters are the permissions; they indicate the read, write and execute permissions for the owner, group and everyone else. After the number (which represents the size) is the owner and group for the file. These files are all owned by <code>admin</code>. This is followed by the file size (less useful for directories) and the date and time of the last modification.

Below is another example of three files in an <code>images</code> subdirectory. Two of the files were uploaded by <code>admin</code> via FTP, and Apache was started by the user <code>www-data</code>. One of the files will be unviewable through a Web browser. Which do you think it is?

<img loading="lazy" decoding="async" class="116648" title="Bad permissions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3875dc27-da38-4e21-a1af-76712b6464b3/ssh-ls-l4.png" alt="Bad permissions" width="500" />

The answer is <code>bg.jpg</code>. Both <code>bg.jpg</code> and <code>logo2.gif</code> have the same permissions: only the owner can read and write them. The <code>logo2.gif</code> file is OK because the owner is <code>www-data</code>, so that file can be accessed, read and returned by Apache. The <code>logo.gif</code> file is also OK because it has <code>r</code> in all three permissions (i.e. owner, group and everyone else). But <code>bg.jpg</code> will fail because only the user <code>admin</code> can read it, not the user who started Apache. If you were to access that file in a Web browser, you would see something like this:

<img class="116646" title="Forbidden message when accessing a file" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c28205b-4433-4938-a1cc-a8b7b5ae9c03/forbidden.png" alt="" width="500" /><br>
<em>What happens when you try to access a file without the correct permissions in a browser.</em>

These sorts of errors can be resolved with the <code>chmod</code> command, which changes file permissions. The three sets of permissions are represented in commands with <code>u</code> (“user” or owner), <code>g</code> (“group”), <code>o</code> (“other” or everyone else) or <code>a</code> (“all”). So, to enable all users to read <code>bg.jpg</code>, either of these would work:

<pre><code class="language-php">chmod go+r images/bg.jpg
chmod a+r images/bg.jpg</code></pre>

If this file were also part of a CMS, then you’d have to also add write permissions before the CMS could overwrite it:

<pre><code class="language-php">chmod a+rw images/bg.jpg</code></pre>

You can also make these changes to all files in all of the subdirectories by adding <code>-R</code>. This recursive operation is not supported by some FTP programs and so is a useful command-line tool:

<pre><code class="language-php">chmod -R a+rw images/</code></pre>

Directories also need the <code>x</code> (“execute” permission), but files generally don’t (unless they are in a <code>cgi-bin</code>). So, you can give everything <code>rwx</code> (read, write and execute) permissions and then take away the <code>x</code> from the files:

<pre><code class="language-php">chmod -R a+rwx images/
chmod -R a-x `find images/ -type f`</code></pre>

However, this does leave everything rather open, making it easier for hackers to gain a foothold. Ideally, your set of permissions should be as restrictive as possible. Files should be writable by the Apache user only when needed by the CMS.</p>

### More Advanced Tip: Chown and the Superuser

Another useful permissions command is <code>chown</code>. It changes the owner of a file. However, you have to be logged in as a user with sufficient privileges (such as <code>root</code>) in order to run it. To make <code>www-data</code> the owner of <code>bg.jpg</code>, run this:

<pre><code class="language-php">chown www-data images/bg.jpg</code></pre>

This will probably return “Permission denied.” You have to run the command as the superuser. For this, you will need to find the root password for your server, and then run the following:

<pre><code class="language-php">sudo chown www-data images/bg.jpg</code></pre>

You will definitely need to be the superuser if you want to edit configuration files, such as Apache’s:

<pre><code class="language-php">sudo vi /etc/httpd/conf/httpd.conf</code></pre>

If you want to become the superuser for every command, run this:

<pre><code class="language-php">su</code></pre>

This is dangerous, though, because you could easily accidentally remove things — especially if you are using the <code>rm</code> command, and particularly if you’re using it in recursive mode (<code>rm -r</code>), and most especially if you also force the changes and ignore any warnings (<code>rm -r -f</code>).</p>

## Conclusion

This article has introduced some very useful Linux commands, a potential asset for any aspiring Web worker and a surefire way to impress a dinner date.

For a few more commands related specifically to website crashes, check out the Smashing Magazine article “<a href="https://www.smashingmagazine.com/2010/12/13/what-to-do-when-your-website-goes-down/">What to Do When Your Website Goes Down</a>.” For a broader view, try this <a href="https://ss64.com/bash/">list of Linux commands</a>. And the “Mastering the VI Editor” tutorial mentioned above explains vi well.

Hopefully, you now have the tools and confidence to pitch in the next time one of your websites has a problem.

{{< signature "al" >}}

