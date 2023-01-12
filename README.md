
# DEVELOPMENT
`docker-compose -f docker-compose.dev.yaml up -d --build`

`docker-compose -f docker-compose.dev.yaml down -v`

# PRODUCTION
`docker-compose -f docker-compose.yaml -f docker-compose.prod.yaml up -d --build`

`docker-compose -f docker-compose.yaml -f docker-compose.prod.yaml down -v`

# CLI

`docker build -t react-image .`

`docker run -e CHOKIDAR_USEPOLLING=true -v %cd%\src:/app/src -p 3000:3000 --name react-app react-image`

