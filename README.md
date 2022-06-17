# heroku-cli-flask

Deployed to Heroku using docker container -> https://secure-ocean-02769.herokuapp.com/

# Requirements
- Installed and logged in to Heroku CLI
- Installed Docker engine for Linux OS, Docker Desktop for Windows OS


## Getting Started
Log in to Container Registry:
```bash
heroku container:login
```
Get sample code by cloning an Alpine-based python example:
```bash
git clone https://github.com/heroku/alpinehelloworld.git
```
Navigate to the app’s directory and create a Heroku app:
```bash
heroku create
```
Build the image and push to Container Registry:
```bash
heroku container:push web
```
Then release the image to your app:
```bash
heroku container:release web
```
Now open the app in your browser:
```bash
heroku open
```
it will show or redirect to your deployed endpoint url link

## Logging in to the registry
Heroku runs a container registry on registry.heroku.com.

If you are using the Heroku CLI, you can log in with:
```bash
heroku container:login
```
or directly via the Docker CLI:
```bash
docker login --username=_ --password=$(heroku auth:token) registry.heroku.com
```
## Building and pushing image(s)
Build an image and push : To build an image and push it to Container Registry, make sure that your directory contains a Dockerfile and run:
```bash
heroku container:push <process-type>
```
Pushing an existing image : To push an image to Heroku, such as one pulled from Docker Hub, tag it and push it according to this naming template:
```bash
docker tag <image> registry.heroku.com/<app>/<process-type>
docker push registry.heroku.com/<app>/<process-type>
```
By specifying the process type in the tag, you can release the image using the CLI. If you would prefer to not specify the process type in the tag, you’ll have to release via the API which uses the image_id.


Pushing multiple images: To push multiple images, rename your Dockerfiles using Dockerfile.<process-type>:
```bash
ls -R
```
example output:
```bash
./webapp:
Dockerfile.web

./worker:
Dockerfile.worker

./image-processor:
Dockerfile.image
```

Then, from the root directory of the project, run:
```bash
heroku container:push --recursive
```
This will build and push all 3 images. If you only want to push specific images, you can specify the process types:
```bash
heroku container:push web worker --recursive
```
example output:
```bash
=== Building web
=== Building worker
=== Pushing web
=== Pushing worker
```

Learning resource:
- Heroku dev Center - https://devcenter.heroku.com/articles/container-registry-and-runtime#:~:text=Heroku%20Container%20Registry%20allows%20you,yml.
