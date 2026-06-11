FROM node AS app
WORKDIR /frontend
COPY . .
RUN npm install && npm run build
# RUN npm run build

FROM nginx
COPY --from=app /frontend/build /usr/share/nginx/html
CMD [ "nginx","-g","daemon off;" ]
