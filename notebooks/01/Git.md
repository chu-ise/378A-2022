# Git and GitHub Configurations

## git config

use the email that is registered at the github account

```sh
git config --global user.name "Your Name"
git config --global user.email you@example.com
```

## clone the epository

```sh
git clone https://github.com/chu-ise/378A-2022
```

## checkout the branch that will be used to submit a pull request

```sh
git checkout -b your-branch # use your id
```

## make your submit folder and copy the homework

```sh
cd homework/submit
mkdir your-folder
cp ../../homework_01.ipynb .
```

## add your homework to the git repo

```sh
git add homework_01.ipynb
git status
```

## commit the changes to the repo

```sh
git commit -m "your message"
git status
```

## push to the github repo

```sh
git push --set-upstream origin your-branch
git status
```

## check out the main branch

```sh
cd ../../../
git checkout main
git status
```

## pull the changes from the github repo

```sh
git pull
git status
```

## checkout your branch again

```sh
git checkout your-branch # no -b option
git status
```
