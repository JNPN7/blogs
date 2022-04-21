# INTRODUCTION
When you are new to Linux and may have stumble upon files .bashrc, .bash_profile like me. So, whats the difference between these two file, what can we append in these files which will make our life easier, well you have came in right place.

# .bashrc vs bash_profile
First we have to know what happens when you first open the terminal does .bashrc runs or .bash_profile runs. When you open the terminal .bashrc runs not .bash_profile. File .bash_profile only runs when you log in to the system.

So, what happen is when you log into your system the .bash_profile script runs. After loging in again, you needed to open up the terminal the .bashrc gets executed not .bash_profile.
Let me show you some the screenshots to demonstrate

![Screenshot from 2022-02-11 23-24-49.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644601354989/xhOvek6n1.png)
This is when we add commands in .bash_profile. su - [username] logins to the username. It is used when you need to switch user. So for this example it works.


![Screenshot from 2022-02-11 23-26-48.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644601403641/q2047hBwt.png)
This is when we add commands in .bashrc. In this example I just opened new terminal.

These file comes handy when you need alias and set environment variables. When you need alias, add alias in .bashrc file. And when you need to set environment variables you can export path in .bash_profile.


For adding alias
```
alias ll="ls -l"
alias la="ls -a"
``` 
You can add these alias in .bashrc file. Now when you just give command ll or la, their alias gets executed. You add any alias as per your choice. You can also be creative and just echo some text so when ever you open up your terminal the text gets printed.

For adding path
```
export PATH="$PATH:<your-new-variable-path>"
export PATH="<your-new-variable-path:$PATH>"
``` 
You can add these paths in .bash_profile file. Then you will be able to use these variable. KIM that .bash_profile only runs at logging in so you need to logout and again login to be able to use these variables

## Problem with exporting path in .bashrc file
Exporting path in .bashrc also works, but really don't do it. It's wrong and bad in every aspects. Many newbie does this mistake, I have also done this when i was new. Let me explain why it is bad. If we exported path in .bashrc file then every-time we open new terminal the path gets added. And the $PATH variable gets updated locally. There is no problem in updating the variable locally i.e. for that single terminal only. Tho, why to update locally i.e. for single terminal, why not to update globally i.e. update one time that's it, then it will work for every terminal. This is exactly what we do by exporting path in .bash_profile

## Problem with aliasing in .bash_profile file
And in alias case you need to keep it in .bashrc not .bash_profile. If you kept alias in .bash_profile then it will not work. Unlike path the alias exists only in current session where as path exists as variable and holds it's value until logging out.

# .bash_logout
Now there is file .bash_logout. So whats the use of it then. Normally, it is not used. It can be used but it's a little sketchy. The .bash_logout only runs in shell in which you logged in the user.


![Screenshot from 2022-02-12 00-16-46.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644604332747/Tef1C4MuP.png)

# Conclusion
.bashrc, .bash_profile are very handy file if you use it right. It makes our live a lot easier.