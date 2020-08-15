# Display a colourful quote on login

:::{#tags}
Linux Bash Fortune Cowsay Lolcat
:::

I saw a screenshot with `lolcat` somewhere which reminded me of my favourite UNIX program, `cowsay`. I set out to make the cow say something colourful on my login into my WSL Ubuntu.

![Figure 1: A screenshot of `bash` prompt displaying a colourful message.](images/linux-fortune-cowsay-lolcat-1.png)


## Installation

Run the usual `apt install` for:

* `fortune-mod`
* `cowsay`
* `lolcat`


## Configuration

Put the following at the end of `.bashrc`, because it's only run for *interactive* shells:

```Shell
# print a friendly fortune on login
if [ -x /usr/games/fortune -a -x /usr/games/cowsay -a /usr/games/lolcat ]; then
    fortune | cowsay | lolcat
fi
```

Obviously, additional command line parameters can be set. I am happy with the default actions.

## Further work

* **TODO** custom fortune database

&mdash;Oliver Frolovs, 2020