# Deploy / Publish to Production 
## Deploy to Digital Ocean Droplet with Ubuntu 22.04 running nginx, gunicorn, and postgreSQL  

- Complete full Testing on local machine (fix any issues discovered in testing before next step)
```bash
make test
```
- Complete full Linting on local machine (fix any linting issues before moving on)
```bash
make pre-commit
```
- Update :octicons-git-branch-24: main branch with latest changes.
    Either:
    - merge new branch into :octicons-git-branch-24: main branch
    - push changes to :octicons-git-branch-24: main branch
- When ready, initiate a pull request to merge changes from the main branch into the production branch.  
    - In Github **open production branch** on click on:   
    n commints behind of <mark style="background-color: lightblue">main</mark>.  
    - You should see something like this:  
    :octicons-git-compare-24: <mark>base: production</mark> :octicons-arrow-left-24: <mark style="background-color: lightblue">compare: main</mark> <span style="color:green"> :octicons-check-24: Able to merge.</span>  ...  
    click the Create Pull Request button and review the changes.
    - Approve and Complete Pull Request according to procedures.  
    Pull Request title should be the version number.
    ```
    version: 0.1.18-alpha
    ```
    The description should show bulleted points that outline the major changes in this version.  It should be similar to the change log, but provide a little more detail.  It may also contain additional items that may not have been appropriate to include in the change log
    ```
    - Correct behavior of 'Cancel' button on the 'My Profile' page
    - Add django-check-seo tools to dev environment.
    - Enhanced 'Home' page to provide a better user experience by making it more engaging and informative. Added 'features' and 'How To' sections
    ```
- Open up a terminal on the Digital Ocean Droplet
```bash title="alias"
remote
```
- cd into the correct directory.  You should be in: 
~/beats -or- /home/rocket/beats
```bash
pwd
```
```bash title="output"
/home/rocket/beats
```
- Check status
```bash
git status
```
```bast title="output"
On branch production
Your branch is up to date with 'origin/production'.

nothing to commit, working tree clean
```
- Updated code on remote server with latest from production branch
```bash
git pull origin production
```
- If it's a <mark>simple update</mark> you can just reload gunicorn & nginx
```bash title="alias"
restart
```
  -- or --
```bash title="full commands"
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```
- If it is a more <mark>complex update</mark> (including changes to the database or dependencies)
```bash title="activate virtual environment"
source _env/bin/activate
```   
```bash title="install dependencies"
pip install -r requirements.txt
```
```bash title="apply django migrations"
python manage.py migrate
```
```bash title="collect static files"
python manage.py collectstatic
```
```bash title="restart gunicorn & nginx using alias"
restart
```
-- or --
```bash title="restart gunicorn & nginx full commands"
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```

- You may need to access the admin site to update settings for django-waffle flags, switches or samples.  Access the admin site at:  /delta/
```url
http://cyclingbeats.com/delta/
```