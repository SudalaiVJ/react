#first build 
FROM node:14 as build-stage

#set working directory
RUN mkdir /usr/app
# copy the Local react file to container.
COPY . /usr/app
# set the working directory
WORKDIR /usr/app
# install all dependencies for the project.
RUN yarn
# Set the path
ENV PATH /usr/src/app/node_modules/.bin:$PATH

RUN npm run build
# second build - create the react app in nginx

FROM nginx:alpine
# set working directory
WORKDIR /usr/share/nginx/html
# remove default files of nginx
RUN rm -rf ./*
#copy the first build to nginx
COPY --from=build-stage /usr/app/build .

ENTRYPOINT ["nginx", "-g", "daemon off;"]
