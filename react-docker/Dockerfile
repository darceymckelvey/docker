# set the base image to create the react app
# we are using the node:20-alpine image, which is a lightweight version of the Node.js image
FROM node:20-alpine

# create a user and group to run the app
# this is a good practice to avoid running the app as root
# the -S flag creates a system user, and the -G flag adds the user to the specified group
# the app will run as the 'app' user, which belongs to the 'app' group
# this helps to improve security by limiting the permissions of the app user
# the 'app' user will have a home directory at /home/app, and will be able to
# read and write files in that directory
# it is good practice to run applications with a non-root user to minimize
# the potential damage that can be caused by a security breach
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

# set the working directory to app
WORKDIR app

# copy the package.json and package-lock.json files to the working directory
# this is necessary to install the dependencies of the app
COPY package*.json ./

# change the ownership of the files to the app user
# this is necessary because the app user needs to have permission to read and write the files
USER root

# change the ownership of the files to the app user
# chrown -R <user>:<group> <directory>
# the -R flag means to change the ownership of the directory and all its contents recursively
# in this case, we are changing the ownership of the current directory (.) to the app user and group
RUN chown -R app:app .

# switch back to the app user
USER app

# install the dependencies of the app
# this will create a node_modules directory in the working directory, which will contain all the dependencies
RUN npm install

# copy the rest of the files to the working directory
# this will copy all the files in the current directory (except for the node_modules directory)
# to the working directory in the container
COPY . .

# expose the port that the app will run on
# this is necessary to allow access to the app from outside the container
EXPOSE 5173

# start the app
# this will run the command 'npm run dev' when the container is started
# the 'npm run dev' command will start the development server of the react app
CMD ["npm", "run", "dev"]
