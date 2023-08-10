### How to manage different account

Suppose,I have multiple Account on github then How can we toggle from one Account to Another Account?Is it possible to push command from different account on a same vscode?

Yes,It is possible to deploy code on Cloud i.e github with mutiple account .
We have to tell to VSCode currently we are using which accont by command
```
git config --global user.email "useremail"
git config --global user.name "username"
```
For in case of any error run followin Command
```
git config --global credential.useHttpPath true
```

[https://stackoverflow.com/questions/47465644/github-remote-permission-denied](for more details refer this documentation)
