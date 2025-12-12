# Prisma Schema Template

Database schema with User model and example resource model.

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// User model - always include for authentication
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  password  String
  name      String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  // Relations to user-owned resources
  tasks     Task[]
  // Add more relations as needed

  @@map("users")
}

// Example resource model - adapt based on requirements
model Task {
  id          String    @id @default(cuid())
  title       String
  description String?
  completed   Boolean   @default(false)
  dueDate     DateTime?
  priority    Priority  @default(MEDIUM)
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // Owner relation
  userId      String
  user        User      @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@map("tasks")
}

enum Priority {
  LOW
  MEDIUM
  HIGH
  URGENT
}
```

## Schema Patterns

### Common Field Types
- `String` - text fields
- `Int` / `Float` - numbers
- `Boolean` - true/false
- `DateTime` - timestamps
- `Json` - flexible JSON data
- `Enum` - predefined values

### Common Modifiers
- `@id` - primary key
- `@unique` - unique constraint
- `@default()` - default value
- `@relation` - foreign key relationship
- `@map()` - custom table/column name
- `@@index()` - database index for performance

### Relation Patterns
```prisma
// One-to-Many (User has many Posts)
model User {
  posts Post[]
}

model Post {
  userId String
  user   User   @relation(fields: [userId], references: [id])
}

// Many-to-Many (Posts have many Tags)
model Post {
  tags Tag[]
}

model Tag {
  posts Post[]
}
```
