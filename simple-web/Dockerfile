# Specify a base image
FROM node:14-alpine

WORKDIR /usr/app

# Install some depenendencies
# By only copying the package.json we avoid reinstalling depenendencies if simple web is modified
COPY ./package.json ./
RUN npm install

# Copy simple web.
COPY ./ ./

# Default command
CMD ["npm", "start"]