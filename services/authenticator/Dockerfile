FROM node:16-alpine

RUN apk --no-cache add build-base python3

WORKDIR /usr/app

COPY services/common services/common
COPY services/authenticator/src services/authenticator/src
COPY services/authenticator/LICENSE services/authenticator/.
COPY services/authenticator/package.json services/authenticator/.
COPY package.json .
COPY yarn.lock .

ENV NODE_ENV production

RUN yarn global add pm2 && \
    yarn workspace @microrealestate/authenticator install --frozen-lockfile --production && \
    yarn cache clean

RUN chown -R node:node /usr/app

USER node

CMD ["pm2-runtime", "services/authenticator/src/index.js"]
