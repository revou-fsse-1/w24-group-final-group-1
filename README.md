# 🎉 FEASTIVAL

An Event Tracker platform offers simplicity and user-friendliness. Our platform is designed to help you effortlessly discover and reminder events that match your interests.

!!! NOTE !!!
we are using our custom organization repo.. you can check our progress below.

![](/assets/branding-aspects.png)

Check out:

- Web:

- Our Organization Repo:

1. Frontend : https://github.com/feastival/feastival-frontend
2. Backend : https://github.com/feastival/feastival-backend

- Progress:

1. Figma : https://www.figma.com/file/wkys7TpKtRP2AcoYXtDvZo/FEASTIVAL?type=design&node-id=0-1&mode=design&t=RzWDwlGkI0PgVU4h-0

## Our Members

| Name                                                | Role                      |
| :-------------------------------------------------- | :------------------------ |
| [Dandi Rizky](https://github.com/DandiRizkyy)       | Lead & Frontend Developer |
| [Indra Setiadhi](https://github.com/indrasetiadhi4) | Backend Developer         |
| [Mesel Ghea](https://github.com/meselghea)          | Frontend Developer        |
| [Niken Hapsari](https://github.com/nikenhpsr)       | Backend Developer         |
| [Okky Anggoro](https://github.com/anggr)            | Frontend Developer        |

## Concept

🎉 FEASTIVAL allows:

- Visitors to create an account.
- Visitors to add their profile photos. - (optional)
- Visitors to search music concerts by concert names or cities.
- Visitors to view upcoming and ongoing music concerts in this month.
- Visitors to read artist profiles.
- Visitor to read detail music concerts.
- Logged-in visitors to add concert reminders for the music concerts they want to attend.
- Logged-in visitors to view the music concerts they have attended and will attend in "My Profile".
- Logged-in visitors to delete reminder history if they decide not to attend a concert or have already attended it.
- Logged-in visitors to create threads and comment on threads in the community.

## Tech Stack

- TypeScript : Typed language Related to JavaScript, HTML, CSS

### Backend

- NestJs : Framework
- PostgreSQL : Database management system
- Prisma ORM : Database ORM
- DigitalOcean : Database deployment
- Render : Api deployment
- REST API
- Swagger

### Frontend

- Next.js : Framework
- React Hook Form : Register component
- React Icons :
- Tailwind : Styling
- Shadcn/ui : Styled interactive components
- React : UI library
- Axios : fetching api
- Vercel : App deployment

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
  imageUrl String?
  password String

  roleId   String?
  role     Role? @relation(fields: [roleId], references: [id])

  events   Event[]
  comments Comment[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Artist {
  id          String  @id @default(uuid())
  name        String  @unique
  description String?
  imageUrl    String?

  events Event[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Event {
  id          String   @id @default(uuid())
  name        String
  imageUrl    String?
  description String
  location    String
  venue       String?
  organizer   String?
  startedAt   DateTime
  finishedAt  DateTime

  statusId String?
  status   Status? @relation(fields: [statusId], references: [id])

  categoryId String?
  category   Category? @relation(fields: [categoryId], references: [id])

  artists Artist[]
  users   User[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Thread {
  id      String @id @default(uuid())
  title   String
  content String

  comments Comment[]

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Comment {
  id String @id @default(uuid())

  userId String
  user   User   @relation(fields: [userId], references: [id])

  threadId String
  thread   Thread @relation(fields: [threadId], references: [id])

  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Category {
  id        String   @id @default(uuid())
  name      String   @unique
  event     Event[]
  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Role {
  id        String   @id @default(uuid())
  name      String   @unique
  user      User[]
  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

model Status {
  id        String   @id @default(uuid())
  name      String   @unique
  event     Event[]
  createdAt DateTime @default(now())
  updatedAt DateTime @default(now()) @updatedAt
}

```

## References

- [www.bandsintown.com](https://www.bandsintown.com/)
- [www.eventbrite.com](https://www.eventbrite.com/)
