# MSCR Developer Guide

This is the developer guide for running the MSCR instance locally and contributing to the codebase. MSCR codebase is available in github repositories and forked from DVV codebase. MSCR codebase is open and for contributing, please create pull request and follow the instructions in the documentation below.

## Getting Access
MSCR code base resides in github and its open source under European Union Public Licence V. 1.1. If you want to contribute, please raise a Pull Request and we will contact you.

## MSCR CodeBase
Majority of the MSCR development happens in two repositories:

- https://github.com/CSCfi/mscr-datamodel-api
- https://github.com/CSCfi/mscr-ui-monorepo

This document describes the manual and automated processes related to software development in these two repositories. 

## MSCR Web App
#### Technology Stack
- React
- Next.js for routing and cache management
- Suomi.fi Components for UI elements

#### Features

#### Running the Frontend Application

- Clone the MSCR front end repository from git@github.com:CSCfi/mscr-ui-monorepo.git.
- Add a .env.local file in mscr-ui root with the following local configs
    - DATAMODEL_API_URL=http://localhost:9004/datamodel-api
    - TERMINOLOGY_API_URL=http://localhost:9103/terminology-api
    - AUTH_PROXY_URL=http://yti-auth-proxy
- for local development, change this to "local" in .env.local:
            REWRITE_PROFILE=docker
            ENV_TYPE=dev
            MATOMO_URL=https://suomi.matomo.cloud

- SECRET_COOKIE_PASSWORD="somethingOf Your choice"
    - The SECRET_COOKIE_PASSWORD should never be inside your repository directly, it's here only to ease the example deployment
    - For local development, you should store it inside a `.env.local` gitignored file. See https://nextjs.org/docs/basic-features/environment-variables#loading-environment-variables next iron cookies are encrypted so the cookie password is for the app to unencrypt the content
- Run npm install in the root directory.
- Go mscr-ui folder and run "npm run dev". MSCR web app will be running in the localhost.

## MSCR Backend

### Setup on Linux:

- Clone mscr-compose repository from github repo https://github.com/CSCfi/mscr-datamodel-api
- Use the linux-dev branch
- Pull relevant images with docker pull,find the names in docker-compose.yml. For pulling the images, contact the development team for access issues.
    - yti-datamodel-api
            docker-registry.rahti.csc.fi/mscr-test/mscr-datamodel-api:latest
    - yti-datamodel-opensearch
            docker-registry.rahti.csc.fi/mscr-test/opensearch:latest
    - yti-fuseki
            docker-registry.rahti.csc.fi/mscr-test/mscr-fuseki
    - yti-groupmanagement
            docker-registry.rahti.csc.fi/mscr-test/yti-groupmanagement:latest
    - yti-postgres
            docker-registry.rahti.csc.fi/mscr-test/yti-postgres:latest
    
- You may need to change the ports in docker-compose.yml if you have conflicts. Set up a directory for the container logs, containing the paths listed out in the following step
- Give the directories required permissions:
    - sudo chown 999 mscr-data/data/logs/yti-postgres/
    - sudo chmod 770 mscr-data/data/logs/
    - sudo chmod g+s mscr-data/data/logs/
    - sudo chmod 775 mscr-data/data/logs/yti-datamodel-opensearch

- Make a .env file in the mscr-compose root and add a line starting with DATADIR= and followed by the path to your mscr_data folder, like: DATADIR=/home/username/mscr/mscr_data/

- Use whatever docker app or plugin you have for getting your hands on the containers This step may need to be updated, the first here is the original but the second or third might be more accurate:
    - run: docker-compose up yti-terminology-api
    - OR run: docker-compose up yti-datamodel-api
    - OR start the yti-datamodel-api container from the docker-compose.yml if your app/plugin allows
- Start a terminal for yti-postgres and do the following:
    - open psql with: psql -U postgres 
    - in psql give command: create user mscr with password 'msrc';
    - then: create database mscr_datamodel with owner mscr;
    - and: create database groupmanagement;
    - \q to exit psql
- in your local terminal, navigate to mscr-compose/scripts and do bash init-admin.sh
check that the containers are running and restart if necessary (you may need to restart all containers several times, sometimes OpenSearch fails to create all indexes at first)

- you need to have this value in your .env.local (different from mock-api): DATAMODEL_API_URL=http://localhost:9004/datamodel-api 

- To get an API-key, go to http://localhost:9302/ , "Impersonate User" Admin User and go to User details in the Menu. Put that key into requests you make.


# Guidelines
# Creating a PR
