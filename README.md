## What’s the difference?

I updated the name and icon, and installed two separate GitHub clients to manage multiple accounts.

```shell
nvm install v20.18.1
nvm use v20.18.1
npm install -g yarn
yarn -v
conda create -n github-desktop python=3.9
conda activate github-desktop
yarn
yarn build:dev
yarn start
yarn build:prod
yarn package
```


## Known Issues

>These preferences will edit your global Git config file.

As a result, switching between different accounts can overwrite your user information.
My solution is to manually edit the config file and toggle comment lines using the command line.

It’s a simple workaround—but it works.

```
[user]
	name = git
	email = @mail
# [user]
	# name = hub
	# email = @mail
```
