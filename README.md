# aad64_Individual_Project_4
Auto Scaling Flask App Using Any Platform As a Service

# Summary:
This project was created to learn the ins and outs of creating a Flask app and using Dockerhub and Azure App Services to deploy said app. For the same, we built a publicly accessible auto-scaling container using Azure App Services and Flask. This was an easy way to build and deploy a scaleable web-hosted app.

YourAppFolder/
├── app.py
├── templates/
│   └── index.html  # Your HTML file
├── static/
│   ├── css/
│   ├── js/
│   └── images/      # Your image files
└── your_python_files/
    ├── __init__.py
    ├── data_processing.py
    └── other_python_file.py


## FAQs:

### 1. How do I create a Dockerhub repository?
Ans: 
1. First, you need to create a Dockerhub account. You can do so [here](https://hub.docker.com/signup).
2. Then, you need to create a repository. You can do so by clicking on `Create Repository`.
3. Then, you need to choose a name for your repository. For this project, I chose `individual_project_4`. (*Note*: Try to add a description as well so that you know what the repo is for.)
4. Then, you need to choose whether you want the repository to be public or private. For this project, I chose `public` as I wanted to make it accessible to everyone.
5. Go ahead and click `Create`. Your screen should would look something like this (**Tip**: Keep website handy because you're going to need the Docker command soon.):
<img width="1280" alt="Screenshot 2023-12-07 at 11 33 45 AM" src="https://github.com/nogibjj/aad64_Individual_Project_4/assets/143753050/450b23c9-9899-4eb5-8607-2a94a672cd5c">


### 2. How do I initially create a web app in Azure? 
Ans: 
1. You start by opening up Microsoft Azure Portal. Go to `Create a New Resource` and click `Web` then `Web App`. 
<img width="1580" alt="Screenshot 2023-12-05 at 10 40 32 PM" src="https://github.com/nogibjj/aad64_Individual_Project_4/assets/143753050/52ff84d3-962b-494d-8820-6d5fd2e2d113">
2. Make sure you've been given enough credits to create a new web app (and if now, ask one of the TAs). 
3. Then, you need to choose or create a Resource Group. For this project, I created a new one. 
4. Choose a name for your project and make sure it's unique. For this project, I called the web app `TellMeMyProfession`.
5. Choose how to publish your code. For this project, I chose `Docker Container` as I wanted to use Docker to deply my app as a Docker image.
6. Choose the operating system. I chose `Linux` as I am working with a Mac.
7. For region, pricing tier, and size, I chose the default options. 
<img width="739" alt="Screenshot 2023-12-07 at 11 38 49 AM" src="https://github.com/nogibjj/aad64_Individual_Project_4/assets/143753050/ecfc3521-c08d-48ca-a596-d1028432a67c">
8. Click Docker, and choose the following options (make sure to change it according to your needs):
<img width="733" alt="Screenshot 2023-12-07 at 11 39 00 AM" src="https://github.com/nogibjj/aad64_Individual_Project_4/assets/143753050/7ef8a9ee-207c-4644-add1-e320ab592b4e">
9. Click `Review + Create` and then `Create`.
For a much better, and much more detailed **how-to**, check [this](https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/1-introduction) link out.
<img width="1204" alt="Screenshot 2023-12-06 at 2 44 08 PM" src="https://github.com/nogibjj/aad64_Individual_Project_4/assets/143753050/d8317e28-c1d3-46cb-b0a2-ff2b4c3a07a0">


### 3. Are there any steps I need to complete before I build my docker image? 
Ans: Yes! First off, make sure that you are working in codespaces. Then, through codespaces, you need to 
1. Install Docker Hub. 
2. Log into Dockerhub
    For this, make sure you know your Dockerhub username, and you could create a password but I personally used a personal access token which I got by clicking my username in the top-right corner and from the drop-down menu select Account Settings. Select the Security tab and then New Access Token.
3. Log into Azure. 

### 4. Why are we using codespaces? 
Ans: Codespaces is a virtual environment that allows you to develop entirely in the cloud and thus, is a great tool for remote development. For the current project, you may face certain issues with library dependencies and/or hardware incompatibilities (especially for Mac M2 users) when you try to build a docker image and deploy your app. To avoid these issues, you can use codespaces to develop your app in the cloud.

### 5. How do I build a flask app? 
Ans: Though there are many approaches to doing this, I found this process to be very useful. 
1. Lay out what exactly you want your web app to do. 
2. After doing so, create your HTML and CSS files to have a basic skeleton of what your user will see (CSS is what you use to style your web page). You can open these HTML files as static files in your web browser. 
3. Create the flask app to then connect your HTML and CSS files to your Python code. You can find the code for the same in `flask_app.py` in this project.
4. Run the app locally to make sure everything is working as expected. You can do so by running `python flask_app.py` in your terminal.

### 6. How do I use **huggingface** in my code?
Ans: First, you need to install the `transformers` package to use hugging face. There are a variety of LLM models you can choose from in hugging face. Follow [this link]([Title](https://huggingface.co/docs/transformers/quicktour)) to learn more. For this project, I used the `text-generation` NLP model. 


### 7. What are the libraries I need to install?
Ans: Most of the libraries are the usual ones we need for CI/CD (e.g., pytest, ruff, etc.). You can find the list of libraries in the `requirements.txt` file. You can install them by running `pip install -r requirements.txt` in your terminal. Some of the unique ones required specifically for this project were:
* `Flask` - to create the web app
* `transformers`- For your LLM model. 
* `tensorflow` - This will be required as a dependency for transformers. If you do not have tensorflow (or pytorch), your docker image will not build. 


### 8. How to run the app locally?
Ans. To run the app locally, write up your entire flask app. This entails making your HTML (and possibly CSS) files as well. Then, you need to run the python file through your command line and if you have successfully built your flask app, you should be able to open your flask app in a web browser. 


### 9. How do I build a docker image? 
Ans: or this, you're first going to want to layout your dockerfile (you can check mine out [here]()). You can find the dockerfile for this project in the main project directory. This will install use Python 3.10.8 as the base image, set the working directory to /app and copy the local directory contents into the container, install required Python packages from a requirements.txt file, expose port 5000 to allow external access, set an environment variable NAME to myenv, and execute a Flask application (flask_app.py) with specified host and port configurations when the container starts.

You may face some issues here, e.g., getting issues regarding torch if you're using huggingface. For the same, I pivoted to using TensorFlow instead of torch and it worked well for my app. However, make sure this is applicable to yours as well before removing any dependencies. 

Then, you can build your dockerimage using the command: `docker build -t <YOUR_DOCKER_USERNAME>/<YOUR_IMAGE_NAME> .`
You want to add your username before the image name because this will help later when you push the image. If you forget to do so, you can use the command: 
`docker tag <YOUR_OLD_IMAGE_NAME>:latest <NEW_IMAGE_NAME>:latest`

If this builds successfully, you can check that this image has been made using: `docker images`

### 10. Why do I have two Dockerfiles?
Ans: I have two Dockerfiles because these two Dockerfiles serve different purposes - one for deploying the Flask application in a production-like environment, and the other for setting up a development environment. The Dockerfile is located in the *main project directory* and is used for deploying your Flask application. It includes instructions to set up a Python environment, copy your project files, install dependencies, and run your Flask app. The Dockerfile located in the *.devcontainer folder* is typically used in development environments, especially when working with Visual Studio Code or VS Code's Remote - Containers extension.


### 11. How do I push my docker image? 
Ans: After you've confirmed that the image has been successfully built, you can push your docker image by using the following command:
`docker push <YOUR_USERNAME>/<YOUR_IMAGE_NAME>`

You may encounter the following error: **unauthorized: access token has insufficient scopes**

If you do, you may need to run the following command in your commmand line to re-login into Dockerhub. 

`docker login -u <YOUR_DOCKER_USERNAME> -p <YOUR_PERSONAL_ACCESS_TOKEN>`

To run the docker file, you use the following command: `docker run -p 5000:5000 <YOUR_IMAGE_NAME>`
* **Note:** Make sure to run this command every time you build a new image to make sure your web app is working the way you want it to. 


### 12. What do I do if while building my docker image, it says **No space left on device**?
Ans: For this, you may need to remove all the cached docker images that you have built thus far. For the same, you could use the command:
`docker system prune --all --force --volumes`

### 13. How do I configure my Azure web app with Dockerhub?
Ans: 
1. Go to your Azure web app Overview page and look for `Deployment Center` in the menu bar on the left. Fill in the necessary details as shown in the image below and click **Save**. 
2. Then, go to `Configuration` and add a New application setting. Make sure to type in the same port number as you've used for your entire flask app. 

**Note:** Make sure to do this any time you build a new image and want to deploy your website. 

