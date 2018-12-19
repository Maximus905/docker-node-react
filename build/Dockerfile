FROM node:8-alpine
RUN apk add --no-cache bash gawk sed grep bc coreutils git

WORKDIR /opt/app
RUN chown -R node:node /opt/app 
COPY --chown=node:node docker-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-entrypoint"]

# set our node environment, either development or production
# defaults to production, compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV $NODE_ENV

# default to port 3000 for node, and 9229 and 9230 (tests) for debug
ARG PORT=3000
ENV PORT $PORT

EXPOSE $PORT 9229 9230

ARG GIT_USER=unknown_user
ENV GIT_USER ${GIT_USER}
ARG GIT_EMAIL=unknown_user@empty.com
ENV GIT_EMAIL ${GIT_EMAIL}

ARG PROJECT_GIT_URL
ENV PROJECT_GIT_URL ${PROJECT_GIT_URL}

RUN echo "git user will be set as ${GIT_USER}" \
	&& git config --global user.name $GIT_USER \
	&& echo "email of git user will be set as ${GIT_EMAIL}" \
	&& git config --global user.email $GIT_EMAIL
USER node
WORKDIR /opt/app
