title: 10 Steps to Continous Deployment For Your Django Project
date: 2015-11-04 11:39:32
category:
- Programming
tags:
- Python
- Porting
- Python3

---

Continous Delivery, Continous Integration, Continous Deployment, Continous... Those are dream words to some teams, for others those are second nature. Getting a deploy procedure completely automated where we can deploy with confidence is not a easy task. With the tools like Jenkins, Snap-CI, Travis, we can get pretty close to this dream deploy of a `git push` to see that in production.

## What are those terms anyway?

### Continous Integration

### Continous Delivery

### Continous Deployment

## Starting out

### Makefile, fabric, ansible, puppet...

Avoid having python dependencies to run your builds, it is always better to depend on system tools for deploying, `fabric` is actually a great deploy tool, but as of today fabric works only on `Python2`. I've seen some people using [invoke](https://invoke.readthedocs.org/en/latest/), invoke is really promissing but for now they are on they pre-release version

### External services

## Adding more steps

## Run by revision

## Automating more and more

### From Continous Integration to Continous Delivery

### From Continous Delivery to Continous Deployment

## Smaller steps are best

Smaller steps run faster, the faster you have feedback the better, getting your

## Check your migrations

## Faster deploys

## After deploys steps
