# 🎉 FEASTIVAL

An Event Tracker platform offers simplicity and user-friendliness. Our platform is designed to help you effortlessly discover and reminder events that match your interests.

Check out:

- Web:
- Repo:
- Progress:

1. Figma : https://www.figma.com/file/wkys7TpKtRP2AcoYXtDvZo/FEASTIVAL?type=design&node-id=0-1&mode=design&t=RzWDwlGkI0PgVU4h-0

## Concept

🎉 FEASTIVAL allow to:

## Data Model

![](/assets/data-model.png)

```
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id       String  @id @default(uuid())
  email    String  @unique
  username String  @unique
  role     Role    @default(USER)
  image    String?
  password String

  events   Event[]
  comments Comment[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now())
}

model Performance {
  id          String  @id @default(uuid())
  name        String  @unique
  description String
  image       String?

  events Event[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now())
}

model Event {
  id          String   @id @default(uuid())
  name        String
  image       String?
  description String
  location    String
  venue       String?
  organizer   String?
  showAt      DateTime
  status      Status

  categoryId String
  category   Category @relation(fields: [categoryId], references: [id])

  performanceId String
  performance   Performance @relation(fields: [performanceId], references: [id])

  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  userId String
  user   User   @relation(fields: [userId], references: [id])
}

model Thread {
  id      String @id @default(uuid())
  title   String
  content String

  comments Comment[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now())
}

model Comment {
  id String @id @default(uuid())

  userId String
  user   User   @relation(fields: [userId], references: [id])

  threadId String
  thread   Thread @relation(fields: [threadId], references: [id])

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now())
}

model Category {
  id        String   @id @default(uuid())
  name      String   @unique
  event     Event[]
  createdAt DateTime @default(now())
  updatedAt DateTime @default(now())
}

enum Role {
  USER
  ADMIN
}

enum Status {
  upcoming
  ongoing
  complete
}



```

## Getting Started

## Tech Stack

- TypeScript : Typed language Related to JavaScript, HTML, CSS

### Backend

- NestJs : Framework
- PostgreSQL : Database management system
- Prisma ORM : Database ORM
- DigitalOcean : Api deployment
- Swagger :

### Frontend

- Next.js : Framework
- React Hook Form : Register component
- React Icons :
- Tailwind : Styling
- DaisyUI : Styled interactive components
- Shadcn/ui : Styled interactive components
- React : UI library
- Vercel : App deployment

## Setup

## References

- [www.bandsintown.com](https://www.bandsintown.com/)
- [www.eventbrite.com](https://www.eventbrite.com/)
