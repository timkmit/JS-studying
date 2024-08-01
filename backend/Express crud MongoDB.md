`npm init -y`
`npm i express @types/express`
`npm i nodemon`

in package.json we need to write "start":"nodemon" for starting our server

`npm i mongoose`
`npm @types/mongoose`

`npm i ts-node`

write tsconfig.json in the root dir:
`{`
    `"compilerOptions": {`
        `"target": "ES6",`
        `"module": "NodeNext",`
        `"moduleResolution": "NodeNext",`
        `"lib": ["ES6"],`
        `"sourceMap": true,`
        `"strict": true,`
        `"noImplicitAny": true,`
        `"esModuleInterop": true,`
        `"resolveJsonModule": true,`
        `"allowJs": true,`
        `"rootDir": "src",`
        `"outDir": "dist"`
    `},`
    `"include": ["src/**/*"]`
`}`

write nodemon.json file in the root dir:
`{`
    `"watch": [`
        `"src"`
    `],`
    `"ext": ".ts, .js",`
    `"exec": "ts-node ./src/index.ts"`
`}`

after that we need to make folders "controllers", "db", "routes" in src and index.ts file

next step write console.log("Hello") in index.ts file and in console run our App: npm run start
ON THAT STEP CKECKING HEALTH OF OUR SERVER
if warning about "cannot find module" - check nodemon.json

now need to try connect DB - create free cluster in Mongo and writing
`import express from "express"`
`import mongoose from "mongoose"`

`const app = express()`
`app.use(express.json())`
`const MONGO_URL = 'mongodb+srv://timkmitdb:65876587@atlascluster.bxtjbj0.mongodb.net/'`
`mongoose.connect(MONGO_URL, {`
    `dbName: 'kanbanApp'`
`})`
    `.then(() => {`
        `console.log("DB connected")`
    `})`
    `.catch((error) => console.log(error))`
`app.listen(3000, () => {`
    `console.log("Server sucsesfully started on 3000 port")`
`})`



npm install swagger-ui-express swagger-jsdoc
npm install --save-dev @types/swagger-ui-express @types/swagger-jsdoc

