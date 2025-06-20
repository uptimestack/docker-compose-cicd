## Manual installation
    - Install nodejs locally
    - Clone the repo
    - Install dependencies
        - npm init -y
        - npm install
        - npm install typescript
        - npx tsc --init
        - Change this in tsconfig.json: "rootDir": "./src", "outDir": "./dist"
        - Change this in package.json:
            -   "scripts": {
                    "build": "tsc -b",
                     "start": "npx prisma migrate dev && node dist/index.js"
                    }
        - If using from Github:
            - in index.ts: import { PrismaClient } from "@prisma/client"
            - in schema.prisma remove output in prisma_generator

    - Start the DB locally
        - docker run -e POSTGRES_PASSWORD=yourpassword -d -p 5432:5432 postgres
        - Go to neon.tech and get yourself a new DB
    - Change the .env file and update your DB credentials
    - npx prisma migrate    
    - npm prisma generate
    - npm run build
    - npm run start

## Docker installation
    - Install docker
    - Create docker network
        - docker network create user-network
    - Start postgres
        - docker run --network user-network --name postgres -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
    - Build the image 
        - docker build --network=host -t user-project . (Use localhost in DATABASE_URL)
        OR
        - docker build --network user-network -t user-project . (Use db container name 'postgres' in DATABASE_URL)
    - Run docker container
        - docker run -e DATABASE_URL=postgresql://postgres:mysecretpassword@localhost:5432/postgres --network user-network -d -p 3000:3000 user-project 

## Docker Compose installation
    - Install docker, docker-compose
    - Run 'docker-compose up'