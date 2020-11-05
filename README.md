TODO:
1. Make & test creategroups script < TO BE AIRED >
2. Test update script
3. Test adding more groups after, then running set up script again
4. Test setcron script again after adding new groups
5. Verify folder structure matches the one listed in this README

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

1. By default you are, but make sure you are in `gitmirror`'s` home directory by typing `cd ~`
2. Clone this repo by typing `git clone https://github.com/Facinorous-420/gitmirrors-bs.git`
3. Enter the new directory by typing `cd gitmirrors-bs`
4. Edit setup.conf by typing `nano setup.conf`
5. Give the setup script execute permissions by typing `chmod u+x ./setup`
<br>

Be sure to read the config and change all things to your desired specifications. Refer to the comments in that file for info on what everything is.
Do not edit anything under the system variables section, only the user variables. You'll need to generate a Personal Access Token in the user `gitmirror` on gitlab for the config.
<br>

**NOTE:** Currently you must create the groups in gitlab using the `gitmirror` user manually. This will be changed in a future update. Once this text is gone, it'll be automatic.
<br>

6. Run `./setup` to begin the automatic set up process. 
7. Once the set up is done, you will be given a SSH key. Login to your `gitmirror` account on your gitlab instance, and add that SSH key to it.
8. Run `./setcron` to add the mirror cron jobs to the users cron table

# Mirroring

Run <code>./mirror</code> to set up a mirror
<br>

The full syntax for the command is `./mirror -g GROUPNAME -n REPONAME -r SOURCEREPOLOCATION`
Where `-g` means **destination group name**, `-n` means **destination repo name**, and `-r` means **source repo location**
<br>

The first time you run this command, it will ask you to enter the `gitmirror` details for your Gitlab instance. I'm going to try to make this as hands free as possible in the future.
<br>

If you at any time want to add more groups you can mirror to, simply add them to the setup.conf file and redo the set up process.

# Updating

You might find out that gitlab-mirror doesn't actually update that often. Although, if it ever does, you can simply run `./update` to update your project's gitlab-mirror.

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