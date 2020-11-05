Yes, I know this README sucks. 
This isn't the final version. This is just to give you a basic understanding of how easy it will be to run this shit.

== SET UP ==
1. Create a user in your gitlab named <code>gitmirror</code>
2. Create a new user on your linux system, probably best to name it <code>gitmirror</code> too
3. Clone this repo into your new users home directory <code>~</code>
4. Edit setup.conf to your desires
5. Run <code>./setup</code> to begin the set up process
6. Copy ssh key shown in terminal at the end of setup script into your gitlab users account
7. Run <code>./creategroups</code> to make all the groups in gitlab <-- this is a WIP script, for now you must make your own in gitlab under the user you made before
8. Run <code>./setcron</code> to add the mirror cron jobs to the users cron table

== ADDING MIRRORS ==

Run <code>./mirror</code> to set up a mirror
If you at any time want to add more groups you can mirror to, simply add them to the setup.conf file and rdo the set up process again.

== UPDATING DEPENDANCIES ==

Use <code>./update</code> to update your gitlab-mirror dependancy

== FILE STRUCTURE ==

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