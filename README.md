# suse-theme

Modified version of the core-beta theme that is included with CTFd by default

## Subtree Installation

### Add repo to themes folder

```
git subtree add --prefix CTFd/themes/suse-ctfd-theme git@github.com:SUSE/suse-ctfd-theme.git main --squash
```

### Pull latest changes to subtree
```
git subtree pull --prefix CTFd/themes/suse-ctfd-theme git@github.com:SUSE/suse-ctfd-theme.git main --squash
```

### Subtree Gotcha

Make sure to use Merge Commits when dealing with the subtree here. For some reason Github's squash and commit uses the wrong line ending which causes issues with the subtree script: https://stackoverflow.com/a/47190256. 

### Builds

- For the latest on CTFd builds see: https://docs.ctfd.io/docs/themes/build-system

Basic build steps:
1. Start from the root of the theme folder (i.e. the same location as this README)
2. run `yarn install`
3. run `yarn build`

If you are running CTFd via docker and have added the theme as a subtree per above, changes from the yarn build should get picked up automatically (you will need to click reload in your browser). For instructions about how to run via Docker, see https://docs.ctfd.io/docs/deployment/installation#docker


### Quick setup

1. git clone https://github.com/CTFd/CTFd.git 
2. cd CTFd
3. git subtree add --prefix CTFd/themes/suse-ctfd-theme git@github.com:SUSE/suse-ctfd-theme.git main --squash
4. cd CTFd/themes/suse-ctfd-theme
5. yarn install
6. yarn build
7. in a separate tab open the top level folder of the CTFd repo
8. if you have not already set a `ctfd_secret_keyi`, run `head -c 64 /dev/urandom > .ctfd_secret_key`
9. in the CTFd folder run `docker-compose up`
10. open a browser to http://0.0.0.0:8000
11. on the `style` step of the setup wizard, in the `theme` dropdown select "suse-ctfd-theme"


### hacky update path

1. push theme changes to a branch of the suse-ctfd-theme repo (the original or a fork)
2. in a terminal window other than where the docker instance of ctfd is running, cd to the CTFd repo folder
3. if any local merges of the theme folder have occurred, git reset to the previous commit without those changes (NOTE! if you're also making changes to CTFd, don't do this!)
4. from the CTFd directory delete the CTFd/themes/suse-ctfd-theme folder
5. repeat the `git subtree add` command from quick setup, replace `main` with your branch name
6. cd into the themes/suse-ctfd/theme folder
7. run `yarn install`
8. run `yarn build`
9. reload the browser session where CTFd is being used
10. curse whoever didn't document a cleaner update path

Note you do *not* need to rebuild the container. 


