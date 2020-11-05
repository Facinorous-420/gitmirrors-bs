TODO:
1. Make & test creategroups script < TO BE AIRED >
2. Test setcron script
3. Test mirror script
4. Test update script
5. Test adding more groups after, then running set up script again
6. Test setcron script again after adding new groups
7. Verify folder structure matches the one listed in this README
8. Rewrite this README to actually look good and be easy to follow

# Prerequisites

### Required software

* [Tested with GitLab 8.x/9.x/10/x][gitlab]
* [python-gitlab @ v1.1.0][python-gitlab]
* [GNU coreutils][coreutils]
* [git 1.8.0][git] or later

#### python-gitlab

   `yum install python-pip` | `sudo apt install python-pip`
   `pip install python-gitlab`


# Set Up

1. Create a user in your gitlab, name it `gitmirror`
2. Create a user on your linux machine, call it `gitmirror` by running: `sudo adduser gitmirror`
3. Switch to the new user by typing `su - gitmirror` and by default you are, but make sure you are in it's home directory by typing `cd ~`
4. Clone this repo by typing `git clone https://github.com/Facinorous-420/gitmirrors-bs.git`
5. Enter the new directory by typing `cd gitmirrors-bs`
6. Edit setup.conf by typing `nano setup.conf`
7. Give the setup script execute permissions by typing `chmod u+x ./setup`
<br>

Be sure to read the config and change all things to your desired specifications. Refer to the comments in that file for info on what everything is.
Do not edit anything under the system variables section, only the user variables. You'll need to generate a Personal Access Token in the user `gitmirror` on gitlab for the config.
<br>

**NOTE:** Currently you must create the groups in gitlab using the `gitmirror` user manually. This will be changed in a future update. Once this text is gone, it'll be automatic.
<br>

8. Run `./setup` to begin the automatic set up process. 
9. Once the set up is done, you will be given a SSH key. Login to your `gitmirror` account on your gitlab instance, and add that SSH key to it.
10. Run `./setcron` to add the mirror cron jobs to the users cron table

# Mirroring

Run <code>./mirror</code> to set up a mirror
<br>

The full syntax for the command is `./mirror -g GROUPNAME -n REPONAME -r SOURCEREPOLOCATION`
Where `-g` means **destination group name**, `-n` means **destination repo name**, and `-r` means **source repo location**
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