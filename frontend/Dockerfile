FROM node:18
WORKDIR /app
COPY public ./public
RUN npm install -g serve
CMD ["serve", "-s", "public", "-l", "3000"]
