Sentry
------

Environment:
```
Language: Javascript
Engine: NodeJS 11.14.0
npm: 6.9.0
sentry: 5.0.8
winston: 3.2.1
```

Create account or login to [sentry](https://sentry.io/auth/login/)
Create an organisation then a project.
Go to project settings, then `Client Keys`, copy it to your project configatuion file (do not share it !).    

Create a nodeJS project:
```
npm init
```

Install sentry library package:
```
npm i --save sentry winston
```

Initialize sentry at the begining of you project:
```Javascript
Sentry.init({
	dsn: '${SENTRY_DSN}',
	release: '${RELEASE_NUMBER}',
	environment: '${ENVIRONMENT_NAME}'
});
```

Example:
```Javascript
Sentry.init({
	dsn: 'https://24b1e90822934ab78b09822147ea8fa0@sentry.io/123123',
	release: '1.0',
	environment: 'production'
});

Define sentry error handler at the end of you router file:
```Javascript
app.use(Sentry.Handlers.errorHandler());
```

Configure [winston](https://github.com/winstonjs/winston) and include configuration file in your project:

`winston_config` file:
```Javascript
...
const logger = createLogger({
...

module.exports = logger;
```

`index.js` file:
Use of winston logger function:
```Javascript
import { logger } from './winston_config'
...
logger.info(["Super log"]);
```
