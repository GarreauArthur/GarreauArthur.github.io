---
layout: post
title: "How to access your DigitalOcean managed database with Github Action ? (example with prisma)"
date: 2021-08-22
math: true
comments: true
tags:
  - DevOps
  - Github
  - DigitalOcean
---

# Goal

The goal of this article is to show you how to add and remove the public IP
address of the GitHub Hosted runner, on which your (CI/CD) workflow is running,
to the list of trusted sources of your DigitalOcean managed database.

# The Problem

So here's the scenario:

* You are creating a workflow using Github actions,
* and you are using a Digital Ocean Managed Database.
* You are also a responsible human being, and decided to limit the access of your
databases to trusted sources only.
* But, you realize that your **CI/CD GitHub workflow** needs to interact with
your database,
* And because you are cheap or lazy (or both like me)
* You don't want to set up a droplet (with a fixed IP) to host your runner
* You just want to use Github hosted runners to run your workflow.
* But you don't know the IP address of your GitHub hosted runners 
* So you decided to read this article to know how to modify your workflow to
add the runner's IP to the list of trusted sources of your database.

# The solution

Because I am such a nice guy, I created [this GitHub Action](https://github.com/marketplace/actions/managed-trusted-sources-of-managed-database-digital-ocean)
to be able to easily add and/or remove the public IP address of your runner to
the list of trusted sources of your database.

This github action requires 2 inputs to work:

* a DigitalOcean access token
* the ID of you database

## Step 1: Create a Digital Access Token

[Check the doc](https://docs.digitalocean.com/reference/api/create-personal-access-token/)

1. <input type="checkbox"> Log in to the [DigitalOcean Control Panel](https://cloud.digitalocean.com/)
2. <input type="checkbox"> On the left, click on API
3. <input type="checkbox"> On the tab "Tokens/keys" > Personal Access token, click "Generate new token"
4. <input type="checkbox"> Choose a name, example: `github_access_token`
5. <input type="checkbox"> Give it READ & WRITE permissions
6. <input type="checkbox"> Click "Generate Token"
7. <input type="checkbox"> Save it somewhere, we will need it later

## Step 2: Get the ID of your database

Getting the ID of a managed database is suprisingly more difficult than I expected,
because it seems like this information is not visible on the web interface of 
DigitalOcean (unless if I am blind).

So to get the Id, we need to use the DigitalOcean CLI `doctl`.

### Step 2.1: Install doctl

This step depends of your OS, so:

1. <input type="checkbox"> Install doctl by following the [doc](https://docs.digitalocean.com/reference/doctl/how-to/install/)
2. Use the API token to grant doctl access to the DigitalOcean account
  1. <input type="checkbox"> `doctl auth init`
  2. <input type="checkbox"> Paste the token
3. <input type="checkbox"> Validate that it's working: `doctl account get`

### Step 2.2: Get the database's ID

1. <input type="checkbox"> Get the ID of the database with: `doctl database list`

## Step 3: Create GitHub secrets

The Digital Ocean access token & the database's ID are sensitive information and
you should store them inside secrets.

1. <input type="checkbox"> Go on your repository's GitHub page 
2. <input type="checkbox"> Click on "Settings"
3. <input type="checkbox"> Click "Secrets" > "New repository secret"
4. <input type="checkbox"> Name: `DIGITALOCEAN_TOKEN`
5. <input type="checkbox"> Paste your token HERE
5. <input type="checkbox"> Click "Add Secret" 
6. <input type="checkbox"> Repeat to add the database id, in a secret named: `DATABASE_ID`

Now we are ready to modify the GitHub workflow

## Step 4: Modify the workflow

It is now time to modify your workflow (YAML file in `.github/workflows/`).

### Step 4.1: Add the runner's IP to the trusted sources 

* <input type="checkbox"> Add a first step, that will add the runner's IP address
to the list of trusted source of your database:

```yml
    # Step 1, add the IP address
    - name: Add IP address to trusted source (managed database)
      uses: GarreauArthur/manage-digital-ocean-managed-database-trusted-sources-gh-action@main
      with:
        action: "add"
        database_id: ${{ secrets.DATABASE_ID  }}
        digitalocean_token: ${{ secrets.DIGITALOCEAN_TOKEN  }}
```

### Step 4.2: Do something with your database (example: Prisma, EXTREMELY VALUABLE INFORMATION)

* <input type="checkbox"> Do something with your database

For example, if you are using [Prisma](https://www.prisma.io), you can migrate
your database with something like:

```yml
    # Step 2, do whatever you need to do with you database
    - name: Deploy to database 
      run: npx prisma migrate deploy
      env:
        DATABASE_URL: ${{ secrets.DATABASE_URL  }}
```

**IMPORTANT**: you need to create a GH secret containing the `connection string`
of your database, **!!! BUT !!!** you need to modify it to make it work: you
need to append `&connect_timeout=60&pool_timeout=60&socket_timeout=60` at the
end of the string, otherwise, the runner will not be able to connect, the
connection will timeout.

### Step 4.3: Remove the runner's IP of the trusted sources

* <input type="checkbox"> Add one step in your workflow, to remove the runner's
IP address of the trusted sources

```yml
    # Step 3, remove the IP address
    - name: Remove IP address of trusted sources (managed database)
      uses: GarreauArthur/manage-digital-ocean-managed-database-trusted-sources-gh-action@main
      with:
        action: "remove"
        database_id: ${{ secrets.DATABASE_ID  }}
        digitalocean_token: ${{ secrets.DIGITALOCEAN_TOKEN  }}
```

## Step 5

Commit & Push, and it should work.

Bye.

