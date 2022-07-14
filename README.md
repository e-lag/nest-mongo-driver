# nest-mongo-driver
driver mongo for NestJs

## Usage

```typescript
/**
 * ### in module
 */
export const DB_MONGO_1 = 'DB_MONGO_1';

const MONGO_DBS: MongoDbConfig[] = [
    {
        injectToken: DB_MONGO_1,
        dbUrlEnvironment: 'DB_MONGO_URL_1',
    },
];

@Module({
    imports: [ MongoDriverModule.forRoot(MONGO_DBS) ],
    providers: [
        ...REPOSITORY_MODULES,
    ],
    exports: [
        MongoDriverModule,
        ...REPOSITORY_MODULES,
    ],
})
export class RepositoriesModule {
}

/** 
 * ### in Service 
 * */

@Injectable()
export class ClientAdapterService  {

    constructor(@Inject(DB_MONGO_1) private db1: Db) {
    }

    async findOne(filter: Filter<UserModel>): Promise<UserModel> {
        return this.db1.collection(USERS_COLLECTION).findOne<UserModel>(filter);
    }
}
```
