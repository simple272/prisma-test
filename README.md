# Prisma Test + Postgresql


## 환경 설정 
### 프로젝트 생성
```
$ npm init -y
$ git init
$ touch .gitignore 
$ touch README.md
```

### 프로젝트 설정 [(Prisma 설정)](https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-typescript-postgres)
```
$ npm i -D prisma typescript ts-node @types/node

$ npx prisma init
$ npm i @prisma/client
```

### Prisma Migration
1. 모델 작성 in schema.prisma file (Install Prisma extension on vscode)
```
    model Post {
        id        Int      @id @default(autoincrement())
        createdAt DateTime @default(now())
        updatedAt DateTime @updatedAt
        title     String   @db.VarChar(255)
        content   String?
        published Boolean  @default(false)
        author    User     @relation(fields: [authorId], references: [id])
        authorId  Int
    }

    model Profile {
        id     Int     @id @default(autoincrement())
        bio    String?
        user   User    @relation(fields: [userId], references: [id])
        userId Int     @unique
    }

    model User {
        id      Int      @id @default(autoincrement())
        email   String   @unique
        name    String?
        posts   Post[]
        profile Profile?
    }
```
2. migration 실행
```
$ npx prisma migrate dev --name init
```

3. client 테스트
```
$ npx ts-node index.ts
```

### Prisma studio 
```
$ npx prisma studio
```