A Jailfile for deploying the example web app for the [jimhttp](https://github.com/dbohdan/jimhttp) microframework. The Jailfile consists of reusable functions that you can import in a POSIX shell script with `IMPORT_ONLY=yes . Jailfile`. It shows how to run an application as a daemon that is automatically restarted.

# Requirements

The Adhokku Ansible role installed on the developer machine. (Follow the instructions in the main [Adhokku repository](https://github.com/adhokku/adhokku) to install it.) A FreeBSD host with Adhokku set up.

# Deployment

1\. Create a new project.

```shell
mkdir adhokku-jimhttp-hello
cd adhokku-jimhttp-hello
git init
```

2\. Create the Ansible files needed to run Adhokku commands.

```shell
export ADHOKKU_PATH="/etc/ansible/roles/adhokku.adhokku/"
sh "$ADHOKKU_PATH/adhokku-tool" init
```

3\. Add the required submodules.

```shell
mkdir vendor
cd vendor
git submodule add https://github.com/adhokku/adhokku-jimhttp
git submodule add https://github.com/dbohdan/jimhttp
cd ..
echo '. /app/vendor/adhokku-jimhttp/Jailfile' > Jailfile
git add .
git commit -m 'Initial commit'
```

4\. Deploy the application.

```shell
ansible-playbook -i inventory playbooks/deploy.yml
```
