# Weatherapp

There was a beautiful idea of building an app that would show the upcoming weather. The developers wrote a nice backend and a frontend following the latest principles and - to be honest - bells and whistles. However, the developers did not remember to add any information about the infrastructure or even setup instructions in the source code.

Luckily we now have [docker compose](https://docs.docker.com/compose/) saving us from installing the tools on our computer, and making sure the app looks (and is) the same in development and in production. All we need is someone to add the few missing files!

---
### Deployed app [link](https://frontend-image-v2aqbqbh2a-od.a.run.app)

---

## Prerequisites

* An [openweathermap](http://openweathermap.org/) API key.
* NodeJS LTS <18.17.1 (16.20.2 Reccomended) - for running without Docker


## Commands (Docker)
### Production
`docker-compose -f .\docker-compose.prod.yml build && docker-compose -f docker-compose.prod.yml up` - Build and start both backend and frontend.

### Dev environment
`docker compose -f .\docker-compose.dev.yml build && docker-compose -f docker-compose.dev.yml up` - Build and start both backend and frontend (with hot reload enabled)

## Commands
### Backend
- `cd backend` - Navigate to backend directory
- `npm install` - Install all requirements for backend
- `npm start` - Start the server in production mode
- `npm run dev` - Start the server in dev mode (MacOS/Linux)
- `npm run dev-win` - Start the server in dev mode (Windows)
- `npm run lint` - Run linter for all files
- `npm run test` - Run unit tests
### Frontend
- `cd frontend` - Navigate to backend directory
- `npm install` - Install all requirements for backend
- `npm start` - Start the server in dev mode
- `npm run build` - Build production static web-app (created in dist)
- `npm run dev` - Start the server in dev mode (MacOS/Linux)
- `npm run dev-win` - Start the server in dev mode (Windows)
- `npm run lint` - Run linter for all files
- `npm run test` - Run unit tests

## Deploy to Google Cloud - Cloud Run
### Prerequisities
* Set up local shell - [Guide](https://cloud.google.com/artifact-registry/docs/docker/store-docker-container-images#local-shell)
* Set up docker respository in Google Artifact Registry - [Guide](https://cloud.google.com/artifact-registry/docs/docker/store-docker-container-images#create)
### Deployment instruction
1. Build containers in production mode:

    `docker-compose -f .\docker-compose.prod.yml build`
2. Set tags for backend:

    `docker tag backend {region}-docker.pkg.dev/{project}/{repository}/backend-image`
3. Push backend image to Google Cloud Artifact Registry:

    `docker push {region}-docker.pkg.dev/{project}/{repository}/backend-image`
4. Deploy backend image in Cloud Run:
    - Go to Cloud Run dashboard
    - Click Create service
    - Choose uploaded image from Artifact Registry
    - Set port to 9000
    - Confirm
5. Copy deployed backend URL to ENDPOINT variable in `frontend/.env.prod` 
6. Build containers in production mode:

    `docker-compose -f .\docker-compose.prod.yml build`
7. Set tags for frontend:

    `docker tag frontend {region}-docker.pkg.dev/{project}/{repository}/frontend-image`
8. Push frontend image to Google Cloud Artifact Registry:

    `docker push {region}-docker.pkg.dev/{project}/{repository}/frontend-image`
9. Deploy frontend image in Cloud Run:
    - Go to Cloud Run dashboard
    - Click Create service
    - Choose uploaded image from Artifact Registry
    - Set port to 90
    - Confirm


---
---
# ORIGINAL EXERCISE INSTRUCTIONS

## Returning your solution

### Via github

* Make a copy of this repository in your own github account (do not fork unless you really want to be public).
* Create a personal repository in github.
* Make changes, commit them, and push them in your own repository.
* Send us the url where to find the code.

### Via tar-package

* Clone this repository.
* Make changes and **commit them**.
* Create a **.tgz** -package including the **.git**-directory, but excluding the **node_modules**-directories.
* Send us the archive.

## Exercises

Here are some things in different categories that you can do to make the app better. Before starting you need to get yourself an API key to make queries in the [openweathermap](http://openweathermap.org/). You can run the app locally using `npm i && npm start`.

### Docker

*Docker containers are central to any modern development initiative. By knowing how to set up your application into containers and make them interact with each other, you have learned a highly useful skill.*

* Add **Dockerfile**'s in the *frontend* and the *backend* directories to run them virtually on any environment having [docker](https://www.docker.com/) installed. It should work by saying e.g. `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`. If it doesn't, remember to check your api key first.

* Add a **docker-compose.yml** -file connecting the frontend and the backend, enabling running the app in a connected set of containers.

* The developers are still keen to run the app and its pipeline on their own computers. Share the development files for the container by using volumes, and make sure the containers are started with a command enabling hot reload.

### Node and React development

*Node and React applications are highly popular technologies. Understanding them will give you an advantage in front- and back-end development projects.*

* The application now only reports the current weather. It should probably report the forecast e.g. a few hours from now. (tip: [openweathermap api](https://openweathermap.org/forecast5))

* There are [eslint](http://eslint.org/) errors. Sloppy coding it seems. Please help.

* The app currently reports the weather only for location defined in the *backend*. Shouldn't it check the browser location and use that as the reference for making a forecast? (tip: [geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation))

### Testing

*Test automation is key in developing good quality applications. Finding bugs in early stages of development is valuable in any software development project. With Robot Framework you can create integration tests that also serve as feature descriptions, making them exceptionally useful.*

* Create automated tests for the application. (tip: [mocha](https://mochajs.org/))

* Create [Robot Framework](http://robotframework.org/) integration tests. Hint: Start by creating a third container that gives expected weather data and direct the backend queries there by redefining the **MAP_ENDPOINT**.

### Cloud

*The biggest trend of recent times is developing, deploying and hosting your applications in cloud. Knowing cloud -related technologies is essential for modern IT specialists.*

* Set up the weather service in a free cloud hosting service, e.g. [AWS](https://aws.amazon.com/free/) or [Google Cloud](https://cloud.google.com/free/).

### Ansible

*Automating deployment processes saves a lot of valuable time and reduces chances of costly errors. Infrastructure as Code removes manual steps and allows people to concentrate on core activities.*

* Write [ansible](http://docs.ansible.com/ansible/intro.html) playbooks for installing [docker](https://www.docker.com/) and the app itself.

### Documentation

*Good documentation benefits everyone.*

* Remember to update the README

* Use descriptive names and add comments in the code when necessary

### ProTips

* When you are coding the application imagine that you are a freelancer developer developing an application for an important customer.

* The app must be ready to deploy and work flawlessly.

* The app must be easy to deploy to your local machine with and without Docker. 

* Detailed instructions to run the app should be included in your forked version because a customer would expect detailed instructions also.

* Structure the code and project folder structure in a modular and logical fashion for extra points.

* Try to avoid any bugs or weirdness in the operating logic.
