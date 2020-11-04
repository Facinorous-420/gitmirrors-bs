1. Create a user in your gitlab named <code>gitmirror</code>
2. Create a new user on your linux system.
3. Clone this repo into your new users home directory <code>~</code>
4. Edit setup.conf to your desires
5. Run <code>./setup</code> to behin the set up process
6. Copy ssh key shown in terminal at the end of setup script into your gitlab users account
7. Run <code>./creategroups</code> to make all the groups in gitlab
8. Run <code>./mirror</code> to set up a mirror

Write script to create cron jobs for auto mirrors

Use ./update to update your gitlab-mirror dependancy
