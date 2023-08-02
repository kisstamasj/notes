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


## Integration testing