# Data Persistence in NestJS

## TypeORM

[https://orkhan.gitbook.io/typeorm/](https://orkhan.gitbook.io/typeorm/)

- works with the most database engine: MySQL, PostgresSQL, SqLite, MongoDB
- install: ```@nestjs/typeorm typeorm```
  
### Connection to the DB

```ts
// app.module.ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [TypeOrmModule.forRoot({
    type: 'sqlite',
    database: 'db.sqlite',
    entities: [],
    synchronize: true // <--- ONLY FOR DEVELOPMENT ENVIRONMENT, AUTOMATIC MIGRATION
  })],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### Entities
Entity is a class that maps to a database table (or collection when using MongoDB).


#### Creating an Entity

1. Create an entity file, and create a class in it that lists all the properties that your entity will have.
```ts
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm"

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number

    /*
    OR with UUID

    @PrimaryGeneratedColumn("uuid")
    id: string;

    */

    @Column()
    firstName: string

    @Column()
    lastName: string

    @Column()
    isActive: boolean
}
```
2. Connect the entity to its parent module. This creates a repository
```ts
import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersController } from './users.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './user.entity';

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  controllers: [UsersController],
  providers: [UsersService]
})
export class UsersModule {}
```
3. Connect the entity to the root connection (in app module)
```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './users/user.entity';

@Module({
  imports: [
    UsersModule, , 
    TypeOrmModule.forRoot({
      type: 'sqlite',
      database: 'db.sqlite',
      entities: [User], // <--- Here
      synchronize: true
    })
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### Usage in a service
```ts
import { Injectable } from '@nestjs/common';
import { Repository } from 'typeorm';
import { InjectRepository } from '@nestjs/typeorm';
import { User } from './user.entity';

@Injectable()
export class UsersService {
    constructor(@InjectRepository(User) private repo: Repository<User>){}

    create(email: string, password: string){
        const user = this.repo.create({email, password})
        return this.repo.save(user);
    }
}
```
> It is possible to call save without create a user entity, but in this case the hooks won't be called.
> It is also true for update and delete function

### Hooks

- ```AfterInsert```: called when a new record inserted into the database
```ts
import { Entity, Column, PrimaryGeneratedColumn, AfterInsert } from "typeorm";

@Entity()
export class User {
    @PrimaryGeneratedColumn('uuid')
    id: string

    @Column()
    email: string;

    @Column()
    password: string;

    @AfterInsert()
    logInsert(){
        console.log('inserted ')
    }
}
```

- [More info](https://orkhan.gitbook.io/typeorm/docs/listeners-and-subscribers)

### Best practice for update
```ts
async update(id: string, attrs: Partial<User>) {
    const user = await this.repo.findOneBy({ id });
    if (!user) {
        throw new NotFoundException('User is not found');
    }

    Object.assign(user, attrs);

    return this.repo.save(user);
}
```