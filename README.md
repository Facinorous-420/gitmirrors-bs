I had wanted to set up a way to easily get gitlab-mirrors set up and running, while managing multiple mirror groups easily. This lead me to create this repo, which more or less automated the installation of those scripts and group creation. If anything doesnt work, feel free to open an issue and Ill take a look at it. I am no way a professional at bash, so my code probably isn't the best and I am open for any PRs that may make it a better and a more streamlined set up. Have fun.

Every step below is needed to get this to work. Please read carefully and do everything it says. Refer to the original repo referenced at the bottom of this README in exactly how the mirroring works, and how you can configure it further than what my scripts will automatically configure for you. 

**NOTE:** if you edit files within `mirrormanagement` folder, then the `update` script will overwrite your changes. Make sure to back them up, or open an issue and Ill add the option youre trying to add into the automation.


# Prerequisites

### Required software

* [Tested with GitLab 8.x/9.x/10/x][gitlab]
* [python-gitlab @ v1.1.0][python-gitlab]
* [GNU coreutils][coreutils]
* [git 1.8.0][git] or later

#### user setup

  1. Create a user in your gitlab, name it `gitmirror`
  2. Create a user on your linux machine, call it `gitmirror` by running: `sudo adduser gitmirror`

#### python-gitlab

   `sudo apt install python-pip`
   then run `pip install python-gitlab` as your `gitmirror` user


# Script Set Up

1. By default you are, but make sure you are in `gitmirror`'s home directory by typing `cd ~`
2. Clone this repo by typing `git clone https://github.com/Facinorous-420/gitmirrors-bs.git`
3. Enter the new directory by typing `cd gitmirrors-bs`
4. Edit setup.conf by typing `nano setup.conf`
5. Give the setup script execute permissions by typing `chmod u+x ./setup`
<br>

Be sure to read the config and change all things to your desired specifications. Refer to the comments in that file for info on what everything is.
Do not edit anything under the system variables section, only the user variables. You'll need to generate a Personal Access Token in the user `gitmirror` on gitlab for the config.
<br>

6. Run `./setup` to begin the automatic set up process. 
7. Once the set up is done, you will be given a SSH key. Login to your `gitmirror` account on your gitlab instance, and add that SSH key to it.
8. Run `./setcron` to add the mirror cron jobs to the users cron table
9. Run `./creategroups` to create all the groups inside of your gitlab automatically

# Mirroring

Run <code>./mirror</code> to set up a mirror
<br>

The full syntax for the command is `./mirror -g GROUPNAME -n REPONAME -r SOURCEREPOLOCATION`
<br>

Where `-g` means **destination group name**, `-n` means **destination repo name**, and `-r` means **source repo location**
<br>

These scripts are meant for mirroring using HTTP not SSH. I'll add an option to pick between the two in the future.
<br>

The first time you run this command, it will ask you to enter the `gitmirror` details for your Gitlab instance. I'm going to try to make this as hands free as possible in the future.
<br>

If you at any time want to add more groups you can mirror to, simply add them to the setup.conf file and redo steps **6**, **8**, and **9** in the Scripts Set Up Section above.

# Updating

You might find out that gitlab-mirror doesn't actually update that often as it's a pretty solid code base. Although, if it ever does, you can simply run `./update` to update your project's gitlab-mirror.

# File Structure

When done, the file structure in your system should look as such:

```
/home/gitmirror/gitmirrors-bs
├── mirrormanagement
│   ├── Group1
│   │ 
│   └── Group2
│ 
└── repositories
    ├── Group1
    │   ├── git
    │   ├── gitlabhq
    │   ├── gitlab-shell
    │   ├── nsca-ng
    │   ├── python-gitlab
    │   ├── ruby
    │   └── systems-svn
    └── Group2
        └── GitLab Enterprise Edition
```

# Great Thanks

Great thanks to the original creator of [gitlab-mirrors](https://github.com/samrocketman/gitlab-mirrors), [samrocketman](https://github.com/samrocketman) obviously as that is the main foundation to these bash scripts.
