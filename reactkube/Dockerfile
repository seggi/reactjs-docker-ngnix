FROM  node:12.19.0-alpine3.9  AS production

WORKDIR /app

COPY package.json ./

COPY yarn.lock ./

RUN yarn install --frozen-lockfile

COPY . .

RUN yarn build

FROM nginx:1.19-alpine AS server

COPY  ./nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --from=production ./app/build /usr/share/nginx/html



