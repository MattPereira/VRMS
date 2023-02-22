# How to contribute to VRMS

If you would like to contribute to our project, please reach out to the leads on Slack or at one of our weekly meetings. You can find the current project team and VRMS team meeting times on the [VRMS Project Details Page](https://www.hackforla.org/projects/vrms).


## **Table of Contents**
1. [**Part 1: Setting up the development environment**](#development-environment-setup)
2. [**Part 2: How to pick up issues**](#how-to-pick-up-issues)
3. [**Part 3: How to create pull requests**](#how-to-create-pull-requests)


## **Setting up the development environment**

### Forking and cloning the repository

#### Step 1: Become a member of the repository Team

Send your GitHub name to the project manager, or post it in the [VRMS Slack channel](https://hackforla.slack.com/archives/CRGH5HM0Q), and we'll add you as a member to the GitHub repository Team. Note: you should be added to both the VRMS and VRMS-write teams.

Once you have accepted the GitHub invite (via email or in your GitHub notifications), please do the following:

1. Mark your own membership public https://help.github.com/en/articles/publicizing-or-hiding-organization-membership#changing-the-visibility-of-your-organization-membership

1. Setup two factor authentication on your account https://github.com/hackforla/governance/issues/20

These steps are manditory in order to contribute to all HackforLA projects.

#### Step 2: Fork the repository

In https://github.com/hackforla/VRMS, look for the fork icon in the top right. Click it and create a fork of the repository.

For git beginners, a fork is a copy of the repository that will be placed on your GitHub account url.

It should create a copy here: https://github.com/your_GitHub_user_name/vrms, where `your_GitHub_user_name` is replaced with exactly that.

Note that this copy is on a remote server on the GitHub website and not on your computer yet.

If you click the icon again, it will not create a new fork but instead give you the URL associated with your fork.

#### Step 3: Clone your online repository to your local computer

The following process will make a copy of the fork that you just created on your local computer.

First create a new folder on your local computer that will contain `hackforla` projects.

In your shell, navigate there then run the following commands:

```bash
git clone https://github.com/your_GitHub_user_name/vrms.git
```

You should now have a new folder in your `hackforla` folder called `vrms`.

Verify which URL your `origin` remote is pointing to:

```bash
git remote show origin
```

If you accidentally cloned the `hackforla/vrms.git` then you can change your local copy to upload to your fork with the following:

```bash
git remote set-url origin https://github.com/your_user_name/vrms.git
```

Add another remote called `vrms` that points to the `hackforla` version of the repository. This will allow you to incorporate changes later:

```bash
git remote add vrms https://github.com/hackforla/vrms.git
```

Note: Understanding how git remotes work will make collaborating much easier. You can learn more about remotes [here](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork) and [here](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

#### Step 4: Change to a new branch

Create a new branch for each issue you work on. Doing all your work on topic branches leaves your repository's main branch unmodified and greatly simplifies keeping your fork in sync with the main project.

This command will let you know available branches and which branch you're on.

```bash
git branch
```

Star (`*`) indicates which branch you're on

By default you should start on the `development` branch.

This command will (create and) change to a new branch:

```bash
git checkout -b fix-logo-width-311
```

The text after the `-b`, in the example `fix-logo-width-311`, will be the name of your new branch. Choose a branch name that relates to the issue you're working on. (No spaces!) The format should look like the scheme above where the words are a brief description of the issue that will make sense at a glance to someone unfamiliar with the issue.

### Incorporating changes from upstream

Your fork of this repository on GitHub, and your local clone of that fork, will
get out of sync with the upstream repository from time to time.

Assuming you have a local clone with remotes `vrms` (the VRMS development repo that you forked) and `origin`
(your fork of this repo)at GitHub, you can do the following:

```bash
# WARNING: this will erase local pending changes!
# commit them to a different branch or use git stash
git checkout development
git fetch vrms
git reset --hard vrms/development
```

This will reset the current HEAD to match the VRMS development repository.

## Get up and running

1. Have [Node](https://nodejs.org/en/download/) and NPM installed locally:

   - Verify with `node -v` and `npm -v` respectively.

1. Install [Yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable): an improved package manager

   - Verify with `yarn --version`

1. Verify that you have the git remote repositories configured:

   - Verify that the output of `git remote -v` shows your local repo as origin and the upstream vrms repo.

1. Install the node packages needed in each directory:

   - `cd vrms/` and run `yarn install`
   - `cd client` and run `yarn install`
   - `cd client-mvp-04` and run `yarn install`
   - `cd ../backend` and run `yarn install`

1. Add your required environment variables for the frontend and backend directories:

   - `touch vrms/backend/.env`
   - `touch vrms/client/.env`
   - `touch vrms/client-mvp-04/.env`

   Note 1: In the above example you are trying to create an empty file called `.env` in each of the listed directories: backend, client and client-mvp-04. You can use either `touch <path-to-directory> .env` or navigate to the directory and use `touch .env`

   Note 2: `touch` is a Unix/Linux or Mac command; It is not available in Windows. In Windows, use a text editor (e.g. Notepad) to create an empty file and save it in each of the locations as `.env` . (If you use Windows Explorer to create the file it will create a file called `.env.txt`, which will not work.)

   - Then paste the content from the [document](https://docs.google.com/document/d/1yDF6UmyO-MPNrl3y_Mw0mkm_WaixlSkXzWbudCzHXDY/edit?usp=sharing). It is accessible for the project team members only.
   - _Please note that the `ports` for the frontend and backend are set in this location_

1. Take a second to review the `app.js` and `server.js` files in the `vrms/backend` folder. These two files are a blueprint for the back end, so please familiarize yourself with it. You'll see folders for the database collection models, routes for the API, and a config file which loads the necessary environment variables.

1. Start the local development servers (frontend & backend).

   To run `client`:

   - Navigate to the root of the application `vrms/` and run `npm run dev`

   To run `client-mvp-04`:

   - Navigate to the root of the application `vrms/` and run `npm run mvp`

You should now have a live app. Happy hacking.


## Using Git

This section discusses some tips and best practices for working with Git.

### Making changes, committing and pushing

1. Changes start on your local fork of this repository, in your own branch.

1. Commit your changes with a comment related to the issue it addresses to your local repository.

1. Push that commit(s) to GitHub.

1. From the `VRMS` repository, create a Pull Request which asks `VRMS` to pull changes from your fork into the main repository.

1. After the owner of the `VRMS` repository approves and merges your Pull Request, your changes will be live on the website.


## Running Tests

The VRMS application has a variety of tests written for the application. Review the `package.json` file in any directory
and look for any variation of `test` scripts.

To run all of the tests run `npm run test:all` from the root folder.

## Using the development database

The application uses MongoDB. We have created a shared development database using MongoDB Cloud and MongoDB Atlas. The conection string for the development database is included in the environmental variables that you pasted into your backend/.env file in step 5 of the "Get Up and Running" setion. If you completed that step successfully you should not need to do anything else.

To view and edit the development database manually, you can download [MongoDB Compass](https://www.mongodb.com/try/download/compass). To connect to the development database you will use the "DATABASE_URL" from the [document](https://docs.google.com/document/d/1yDF6UmyO-MPNrl3y_Mw0mkm_WaixlSkXzWbudCzHXDY/edit?usp=sharing) that contained the environmental variables. The string will start with "mongodb+srv://".

If you want to install a local copy to experiment with and learn more about MongoDB, you can use [this tutorial](https://zellwk.com/blog/local-mongodb/)



## **Part 2: Picking up Issues**
### **2.1 VRMS contributor expectations**
1. Attend at least 1 team meeting per week
2. Devote a minimum of 6 hours per week to working on VRMS assignments
3. Communicate with the team leadership if you plan to step away from the project

### **2.2 How VRMS organizes issues**
Developers may choose from issues with the following `role` labels:
- `role: Front End`
- `role: Back End`
- `role: Database`

### **2.3 Where to find issues**
The best way to view the issues available is our [GitHub Project Board](https://github.com/hackforla/VRMS/projects/12)

Developers may assign themselves issues only from the [Prioritized Backlog column](https://github.com/hackforla/VRMS/projects/12#column-19074778) and only one at a time.


### **2.4 Claiming an Issue**
The Prioritized Backlog column is filtered so the first (top) issue has the highest priority and should be worked on next if possible.


1. Assign yourself to the issue 
2. Move the issue to the `In Progress` column


### **2.5 Working on an Issue**
You must first create a new branch before you begin work on an issue.

1. Make sure you are on the `development` branch by using the command 
```
git branch
```
2. Pull down the latest changes from the `development` branch by using the command
```
git pull vrms development
```
3. Create a new branch where you will work on your issue by using the command 
```
git checkout -b <your-branch-name>
```
4. Add and commit changes to your new branch using the commands
```
git add .
git commit -m "your commit message"
``` 


## **Part 3: Pull Requests**
### **3.1 Pushing changes to your forked repository**
Once you are satisfied with your changes, push them to the feature branch you made within your remote repository.
```
git push --set-upstream origin <your-branch-name>
```
### **3.2 Createing a pull request on the VRMS repository**
1. Go to your forked repository on GitHub and click on the `Compare & pull request` button.
2. Title your pull request by summarizing the changes you made
3. Add your issue number to the pull request
4. Fill out the what changes did you make and why section of the PR creation comment
5. Include images with your pull request if there are any visual changes to the user interface



