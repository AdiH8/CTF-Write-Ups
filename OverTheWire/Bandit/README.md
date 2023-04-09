# Bandit Level 0

## Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

# Bandit Level 0 → Level 1

## Level Goal

The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

```bash
cat readme
```

>password for Bandit1:
> NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

# Bandit Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called **-** located in the home directory

```bash
cat ./-
```

>password for Bandit2: 
>rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi