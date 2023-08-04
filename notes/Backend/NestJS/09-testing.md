# Testing in NestJS

- speed up testing: 
```json
//package.json
{
    ...

    "scripts": {
        ...

        "test:watch": "jest --watch --maxWorkers=1",

        ...
    }
}
```

## Unit testing

- testing small units of the project (controller, service etc..) 
- we have to provide all the neccessery service (in the example we provide UsersService fake version)
- we have to fake services wich one connected to a repo and db

### Unit testing services

```ts
import { Test } from '@nestjs/testing';
import { AuthService } from './auth.service';
import { UsersService } from './users.service';
import { User } from './user.entity';
import { v4 as uuid } from 'uuid';
import { BadRequestException, UnauthorizedException } from '@nestjs/common';

describe('AuthService', () => {
  let service: AuthService;
  let fakeUsersService: Partial<UsersService>;

  beforeEach(async () => {
    // store users in memory
    const users: User[] = [];
    fakeUsersService = {
      find: (email: string) => {
        const filterdUsers = users.filter((user) => user.email === email);
        return Promise.resolve(filterdUsers);
      },
      create: (email: string, password: string) => {
        const user = { id: uuid(), email, password } as User;
        users.push(user);
        return Promise.resolve(user);
      },
    };
    const module = await Test.createTestingModule({
      providers: [
        AuthService,
        { provide: UsersService, useValue: fakeUsersService },
      ],
    }).compile();

    service = module.get(AuthService);
  });

  it('Can create an instance of auth service', async () => {
    expect(service).toBeDefined();
  });
});
```

- expect for error throwing:
```ts
it('throws an error if user signs up with email that is in use', async () => {
    await service.signup('asdf@asdf.com', 'asdf');
    await expect(service.signup('asdf@asdf.com', 'asdf')).rejects.toThrow(
      BadRequestException,
    );
});
```

> in this scenario we don't test the users service, this test only testing the auth service

### Unit testing controllers
- we dont testing decorators, interceptors (e2e test )
- we have to implement fakeServices (only the functions wich is needed for the tests)
- example:
```ts
import { Test, TestingModule } from '@nestjs/testing';
import { UsersController } from './users.controller';
import { UsersService } from './users.service';
import { AuthService } from './auth.service';
import { User } from './user.entity';
import { NotFoundException } from '@nestjs/common';

describe('UsersController', () => {
  let controller: UsersController;
  let fakeUsersService: Partial<UsersService>;
  let fakeAuthService: Partial<AuthService>;

  beforeEach(async () => {
    fakeUsersService = {
      findOne: (id: string) => {
        return Promise.resolve({
          id,
          email: 'asd@asd.hu',
          password: 'asd123',
        } as User);
      },
      find: (email: string) => {
        return Promise.resolve([
          { id: 'asd', email, password: 'asd123' },
        ] as User[]);
      },
      // remove: () => {},
      // update: () => {},
    };
    fakeAuthService = {
      // signup: () => {},
      signin: (email: string, password: string) => {
        return Promise.resolve({ id: 'asd123', email, password } as User);
      },
    };

    const module: TestingModule = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [
        { provide: UsersService, useValue: fakeUsersService },
        { provide: AuthService, useValue: fakeAuthService },
      ],
    }).compile();

    controller = module.get<UsersController>(UsersController);
  });

  it('should be defined', () => {
    expect(controller).toBeDefined();
  });

  it('findeAllUsers returns a list of users with the given email', async () => {
    const users = await controller.findAllUsers('asd@asd.hu');
    expect(users.length).toEqual(1);
    expect(users[0].email).toEqual('asd@asd.hu');
  });

  it('findUser returns a single user with a given id', async () => {
    const user = await controller.findUser('asd');
    expect(user).toBeDefined();
  });

  it('findUser throws an error if the given id is not found', async () => {
    fakeUsersService.findOne = (id: string) => null;

    await expect(controller.findUser('asd')).rejects.toThrow(NotFoundException);
  });

  it('sign in updates session object and retuns user', async () => {
    let session = { userId: '' };
    const user = await controller.signin(
      { email: 'asd@asd.hu', password: 'asd123' },
      session,
    );

    expect(user.id).toEqual('asd123');
    expect(session.userId).toEqual('asd123');
  });
});
```

## E2E testing (end to end testing)
- Testing different part of the application to working perfectly together.
- create an entyre copy of the application
- create requests to the application
- create copy of the applictation to every single test
- for running one test at the time set this to the package.json: ```"test:e2e": "jest --config ./test/jest-e2e.json --maxWorkers=1"```
- cli command: ```npm run test:e2e```
- when e2e test running it will skip the complete ```main.ts``` file, so the pipes, middlewares and configurations will not be applied
  - **solution 1**: Create a ```setupApp(app)``` function, wich can receive the app as parameter, and apply in there the pipes, middlewares and configurations. So we can call this function in the ```main.ts``` and also in the e2e tests. **This is not the official way, but works fine.**
  - **solution 2 (official)**: Apply the pipes, middlewares and configurations inside the AppModule.
  
    - **applying pipes (ex.: validation pipe)**:
    ```ts
    // app.module.ts
    import { ValidationPipe } from '@nestjs/common';
    import { APP_PIPE } from '@nestjs/core';

    ...

    providers: [
      {
        provide: APP_PIPE,
        useValue: new ValidationPipe({
          whitelist: true,
        }),
      },
    ]

    ...

    ```
    - **applying middleware (ex.: cookie-session)**:
    ```ts
    // app.module.ts
    import { MiddlewareConsumer } from '@nestjs/common';
    const cookieSession = require('cookie-session');

    ...

    export class AppModule {
      configure(consumer: MiddlewareConsumer) {
        consumer
          .apply(
            cookieSession({
              keys: ['asdf1234'],
            }),
          )
          .forRoutes('*');
      }
    }
    ```
- setting up test db: [more info in config-service.md](10-config-service.md)
- clear up the test db:

src/test/setup.ts
```ts
import { rm } from 'fs/promises';
import { join } from 'path';

global.beforeEach(async () => {
  try {
    await rm(join(__dirname, '..', 'test-db.sqlite'));
  } catch (error) {
    console.log('Failed to delete test-db.sqlite');
  }
});
```
jest-e2e.json
```json
{
  "moduleFileExtensions": ["js", "json", "ts"],
  "rootDir": ".",
  "testEnvironment": "node",
  "testRegex": ".e2e-spec.ts$",
  "transform": {
    "^.+\\.(t|j)s$": "ts-jest"
  },
  "setupFilesAfterEnv": ["<rootDir>/setup.ts"] // <--- here
}
```

- get and send cookie session:
```ts
it('signup as a new user then get the currently logged in user', async () => {
    const testEmail = 'asd@asd.hu';
    const res = await request(app.getHttpServer())
      .post('/auth/signup')
      .send({ email: testEmail, password: 'asd123' })
      .expect(201);

    const cookie = res.get('Set-Cookie'); // <--- get the cookie from the response

    const { body } = await request(app.getHttpServer())
      .get('/auth/whoami')
      .set('Cookie', cookie) // <--- set the cookie to the next request
      .expect(200);

    expect(body.id).toBeDefined();
    expect(body.email).toEqual(testEmail);
  });
```

## Integration testing