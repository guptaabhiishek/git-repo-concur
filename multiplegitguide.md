Git commands
Step 1 - Create a New SSH Key

ssh-keygen -t rsa -C "your-email-address”
Save key to ~/.ssh/id_rsa_yours

Step 2 - Attach the New Key

login to your second GitHub account, browse to "Account Overview," and attach the new key ~/.ssh/id_rsa_COMPANY.pub
, within the "SSH Public Keys" section. 
ext, because we saved our key with a unique name, we need to tell SSH about it. Within the Terminal, type: ssh-add ~/.ssh/id_rsa_COMPANY

Step 3 - Create a Config File

We've done the bulk of the workload; but now we need a way to specify when we wish to push to our personal account, and when we should instead push to our company account. To do so, let's create a config file.
touch ~/.ssh/config
vim config
#Default GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
 Let's add another one for the company account. Directly below the code above, add:

Host github-COMPANY
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_COMPANY
Step 4 - Try it Out

Create a test directory, initialize git, and create your first commit.

git init
git commit -am "first commit'
	Login to your company account, create a new repository, give it a name of "git-repo-concur," and then return to the Terminal and push your git repo to GitHub.

15MBP-03115:testgit abhishekg$ git remote add origin git@github.com:guptaabhiishek/git-repo-concur.git

15MBP-03115:testgit abhishekg$ git push -u origin master


Note that, this time, rather than pushing to git@github.com, we're using the custom host that we create in the
config file: git@github-COMPANY.

Return to GitHub, and you should now see your repository. Remember:

When pushing to your personal account, proceed as you always have.
For your company account, make sure that you use git!github-COMPANY as the host.