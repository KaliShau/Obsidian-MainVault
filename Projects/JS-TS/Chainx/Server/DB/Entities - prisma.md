
___
##### Use prisma: 
```D
model Users {
	id String @id @default(uuid())
	createdAt DateTime @default(now()) @map("created_at")
	updatedAt DateTime @updatedAt @map("updated_at")
	
	username String @unique
	password_hash String
	
	firstName String @default("No first name") @map("first_name")
	lastName String @default("No last name") @map("last_name")
	
	imageUrl String @default("uploads/avatars/default.jpg") @map("image_url")
	
	posts Posts[]
	sentMessages Messages[] @relation("SentMessages")
	receivedMessages Messages[] @relation("ReceivedMessages")
	comments Comments[]
	likes Likes[]
	
	@@map("users")
}

model Posts {
	id String @id @default(uuid())
	createdAt DateTime @default(now()) @map("created_at")
	updatedAt DateTime @updatedAt @map("updated_at")
	
	title String
	content String
	
	imageUrl String @map("image_url")
	
	user Users @relation(fields: [userId], references: [id])
	userId String @map("user_id")
	
	comments Comments[]
	likes Likes[]
	
	@@map("posts")
}

model Messages {
	id String @id @default(uuid())
	createdAt DateTime @default(now()) @map("created_at")
	updatedAt DateTime @updatedAt @map("updated_at")
	
	content String
	
	sender Users @relation("SentMessages", fields: [senderId], references: [id])
	senderId String @map("sender_id")
	
	receiver Users @relation("ReceivedMessages", fields: [receiverId], references: [id])
	receiverId String @map("receiver_id")
	
	@@map("messages")
}
  
model Comments {
	id String @id @default(uuid())
	createdAt DateTime @default(now()) @map("created_at")
	updatedAt DateTime @updatedAt @map("updated_at")
	
	content String
	
	user Users @relation(fields: [userId], references: [id])
	userId String @map("user_id")
	
	post Posts @relation(fields: [postId], references: [id])
	postId String @map("post_id")
	
	@@map("comments")
}

model Likes {
	id String @id @default(uuid())
	createdAt DateTime @default(now()) @map("created_at")
	updatedAt DateTime @updatedAt @map("updated_at")
	
	users Users @relation(fields: [userId], references: [id])
	userId String @map("user_id")
	
	post Posts @relation(fields: [postId], references: [id])
	postId String @map("post_id")
	
	@@map("likes")
}
```