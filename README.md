# Google Cloud Function Boilerplate

## Setup
- [Signup for Google Cloud](https://console.cloud.google.com)
- Create a new project project.
- Install the `gcloud` cli tool.
	```sh
	brew cask install google-cloud-sdk
	```
- Login
	```sh
	gcloud auth login
	```
- Find the project id you just created and set it as the current project.
	```sh
	gcloud projects list
	gcloud config set project translator-246304
	```

## Development
- (optional) If you want to use gcloud services, you'll need to create some credentials.
	```sh
	gcloud iam service-accounts create chet-dev
	```
- Add an owner policy
	```sh
	gcloud projects add-iam-policy-binding translator-246304 --member "serviceAccount:chet-dev@translator-246304.iam.gserviceaccount.com" --role "roles/owner"
	```
- Create the credentials file.
	```sh
	gcloud iam service-accounts keys create credentials.json --iam-account chet-dev@translator-246304.iam.gserviceaccount.com
	```
- Start the development server (you may have to build the first bundle `npm run build` before you do this.)
	```sh
	npm start
	```
- Test that its working
	```sh
	curl curl http://localhost:8080/
	```

## Deploying
- [Read about it here](https://cloud.google.com/functions/docs/deploying/filesystem)
- Build the TypeScript files:
	```sh
	npm run build
	```
- Edit the package.json deploy script to reference the name of the function you want to deploy. Currently, it's called `translate`.
- Deploy
	```sh
	npm run deploy
	```
- The deployment should log an endpoint url that you can test.
	```sh
	curl https://us-central1-translator-246304.cloudfunctions.net/translate
	```

## Resources
- https://www.toptal.com/nodejs/serverless-nodejs-using-google-cloud
- https://cloud.google.com/functions/docs/writing/
- https://cloud.google.com/functions/docs/functions-framework