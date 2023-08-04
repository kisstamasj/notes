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

**For better testing (with validation pipe, cookie session config and config service):**
```ts
import { MiddlewareConsumer, Module, ValidationPipe } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ReportsModule } from './reports/reports.module';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './users/user.entity';
import { Report } from './reports/report.entity';
import { APP_PIPE } from '@nestjs/core';
import { ConfigModule, ConfigService } from '@nestjs/config';
const cookieSession = require('cookie-session');

@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true,
      envFilePath: `.env.${process.env.NODE_ENV}`,
    }),
    UsersModule,
    ReportsModule,
    TypeOrmModule.forRootAsync({
      inject: [ConfigService],
      useFactory: (config: ConfigService) => {
        return {
          type: 'sqlite',
          database: config.get<string>('DB_NAME'),
          synchronize: true,
          entities: [User, Report],
        };
      },
    }),
  ],
  controllers: [AppController],
  providers: [
    AppService,
    {
      provide: APP_PIPE,
      useValue: new ValidationPipe({
        whitelist: true,
      }),
    },
  ],
})

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

    @Column({default: false}) // <--- setting default value for a field
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
> It is also be true for update and delete function

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

### Associations (relations)
#### Steps:
1. Figure out what kind of association we are modeling
2. Add the appropriate decorators to our related entities
3. Assoctiate the records when one is created
4. Apply a serializer to limit info shared

#### Relations types

- **one-to-one relationship**:
One record associated with one other record. (Ex.: Country <-> Capital)
- **one-to-many or many-to-one relationship**:
One record can related many other records. (Ex.: Car <-> parts, Customer <-> Orders, Country <-> Cities)
- **many-many relationship**:
Many records can related many other records. (Ex.: Trains <-> Riders, Classes <-> Students)

#### One-to-Many relationship

**src/users/user.entity.ts**
```ts
import { Report } from '../reports/report.entity';
import {
  Entity,
  Column,
  PrimaryGeneratedColumn,
  OneToMany,
} from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  email: string;

  @Column()
  password: string;

  // here the relation
  @OneToMany(() => Report, (report) => report.user)
  reports: Report[];
}
```
- ```@OneToMany()``` decorator does not change the Users table
- association is not automatically fetched when we fetch a user

**src/reports/report.entity.ts**
```ts
import { User } from '../users/user.entity';
import { Entity, Column, PrimaryGeneratedColumn, ManyToOne } from 'typeorm';

@Entity()
export class Report {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  price: number;

  @Column()
  make: string;

  @Column()
  model: string;

  @Column()
  year: number;

  @Column()
  lng: number;

  @Column()
  lat: number;

  @Column()
  mileage: number;

  @ManyToOne(() => User, (user) => user.reports)
  user: User;
}
```
- ```@ManyToOne()``` decorator changes the Reports table (create userId field)
- association is not automatically fetched when we fetch a report

#### Making query with association (one-to-many)

```ts
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { CreateReportDto } from './dtos/create-report.dto';
import { Report } from './report.entity';
import { User } from '../users/user.entity';

@Injectable()
export class ReportsService {
  constructor(@InjectRepository(Report) private repo: Repository<Report>) {}

  create(reportDto: CreateReportDto, user: User) {
    const report = this.repo.create(reportDto as Report);
    // here is the association
    report.user = user;
    return this.repo.save(report);
  }
}
```

#### Find with relation
```ts
const report = await this.repo.findOne({
  where: { id },
  relations: { user: true },
});
```

#### Dto for serialization
```ts
import { Expose, Transform } from 'class-transformer';

export class ReportDto {
  @Expose()
  id: number;

  @Expose()
  price: number;

  @Expose()
  make: string;

  @Expose()
  model: string;

  @Expose()
  year: number;

  @Expose()
  lng: number;

  @Expose()
  lat: number;

  @Expose()
  mileage: number;

  // Showing only the userId and not the whole User object
  @Transform(({ obj }) => obj.user.id)
  @Expose()
  userId: string;
}
```