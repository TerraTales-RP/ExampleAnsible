### Initial Requirements
- A computer or server running some form of Linux
- An internet connection
- patience

# Installation
This is a step by step process of cloning and configuring this for a new Pterodactyl Server. 

1. Clone the Repository
Download Git if you don't already have it, go through the steps to clone this repository. Here's [documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

2. Install Ansible
There are various ways to install Ansible. The most basic Linux distributions such as Ubuntu can install Ansible with `sudo apt install ansible`. However, I recommend you check out Ansible's
[documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for installing before you make any more decisions.

3. Setup Ansible Hosts File
This all depends on whether you're running this on your own local system or intend to have it run remotely. I'm only going to detail how to set it up locally as that was the intended use case on TerraTales.
For additional information on setting up your hosts file, you can find it located [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).
The simplest way to do this is  the following. We first create and modify the host file via running ```sudo vi /etc/ansible/hosts```. If you're unfamiliar with vi, it's pretty simple for what we're doing.
First hit your `insert` key to enter insert mode and type the following into the file.
```
[local]
127.0.0.1
```
Write the file by hitting `ESC` to exit insert mode, and type `:w` to write the file. Once that's completed you can simply type `:q` to exit the program.

4. Fill out vars.yml
You're going to want to rename the `vars.yml.example` file to `vars.yml`, this can be done simply in the folder with ```cp vars.yml.example vars.yml```. From there, use your preferred text editor to
modify the variables. If you need help with GitHub Personal Access Tokens, documentation is [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

5. Setup ansible-playbook.yml
There's only two major lines in this file that need to be edited.
The below line will need to be modified in accordance with the file path of the vars.yml file. (Line 7)
```yml
vars_files:
  #The Full Path for the Variable File. This needs to be changed for each install. 
    - /home/example/ExampleAnsible/vars.yml
```
The below line will need to be modified to reflect the upstream Git repository that you will be using for making changes. (Line 48)
```yml
- name: Pull Live Git Repository. (Should Avoid Auth Status Hang)
      git:
        # The below line will need to be changed according to your Github User/Org and Repository.
        repo: 'https://{{git_user}}:{{git_pac}}@github.com/YOURUSER-OR-ORG/REPOSITORY.git'
```

6. Setting up Plugins & Configurations
There are some example plugins in the folders already. You'll have to create the configuration folders and files when you add a plugin to it. From there it's quite self-explanatory. I'd recommend having
your staff members make pull requests to the repository as they make changes.
