# Fullstack TypeScript

Fullstack TypeScript is a popular technology stack for building web applications using TypeScript on both the frontend
and backend.

## Resolvers

Resolvers are an important concept in Fullstack TypeScript that help to manage data flow between the
frontend and backend of an application.

Resolvers are functions that are responsible for retrieving data from a data source and returning it to the client. In
Fullstack TypeScript, resolvers are typically used to retrieve data from a backend database and return it to the
frontend client.

Resolvers are typically organized into GraphQL schemas, which define the data types and operations that can be performed
on the data. Here's an example of a GraphQL schema in Fullstack TypeScript:

```typescript
type Book = {
    id: ID,
    title: String,
    author: String,
}

type Query = {
    books: [Book],
    book(id: ID): Book
}

type Mutation = {
    createBook(title: String, author: String): Book
    updateBook(id: ID, title: String, author: String): Book
    deleteBook(id: ID): ID
}
```

### Resolvers implementation

To implement resolvers in Fullstack TypeScript, you can use a library such as graphql-tools or type-graphql. These
libraries provide utilities for defining resolvers and generating TypeScript types based on your schema.

```typescript
@Resolver(Book)
export class BookResolver {
    constructor(private bookService: BookService) {
    }

    @Query(() => [Book])
    async books(): Promise<Book[]> {
        return this.bookService.getAllBooks();
    }

    @Query(() => Book, {nullable: true})
    async book(@Arg('id') id: string): Promise<Book | null> {
        return this.bookService.getBookById(id);
    }

    @Mutation(() => Book)
    async createBook(@Arg('title') title: string, @Arg('author') author: string): Promise<Book> {
        return this.bookService.createBook(title, author);
    }

    @Mutation(() => Book, {nullable: true})
    async updateBook(@Arg('id') id: string, @Arg('title', {nullable: true}) title?: string, @Arg('author', {
        nullable:
            true
    }) author?: string): Promise<Book | null> {
        return this.bookService.updateBookById(id, title, author);
    }

    @Mutation(() => ID)
    async deleteBook(@Arg('id') id: string): Promise<string> {
        await this.bookService.deleteBookById(id);
        return id;
    }
}
```

We define resolver methods for each of the operations defined in the schema using the @Query and @Mutation decorators.
The @Arg decorator is used to specify the arguments that can be passed to the resolver methods.

## Consuming Data

Consuming data is an important aspect of Fullstack TypeScript that allows the frontend to retrieve data from the backend
and display it to the user.

### Consuming Data on the Frontend

On the frontend, there are several ways to consume data in a Fullstack TypeScript application. One common approach is to
use a client-side GraphQL library such as Apollo Client.

Apollo Client provides an easy-to-use API for making GraphQL queries and mutations.

```typescript
import {ApolloClient, InMemoryCache, gql} from '@apollo/client';

const client = new ApolloClient({
    uri: 'http://localhost:4000/graphql',
    cache: new InMemoryCache(),
});

const GET_BOOKS = gql`
query GetBooks {
books {
id
title
author
}
}
`;

client
    .query({
        query: GET_BOOKS,
    })
    .then((result) => console.log(result));
```

### Consuming Data on the Backend

On the backend, there are several ways to consume data in a Fullstack TypeScript application. One common approach is to
use an ORM (Object Relational Mapping) library such as TypeORM.

TypeORM provides an easy-to-use API for interacting with a database.

```typescript
import {createConnection} from 'typeorm';
import {Book} from './entities/book.entity';

createConnection()
    .then(async (connection) => {
        const bookRepository = connection.getRepository(Book);

        const books = await bookRepository.find();
        console.log(books);

    })
    .catch((error) => console.log(error));
```

## Mutations

Mutations are a way to modify data on the backend. Mutations allow clients to send data to the server to create, update,
or delete resources.

### Mutations on the Frontend

On the frontend, there are several ways to perform mutations in a Fullstack TypeScript application. One common approach
is to use a client-side GraphQL library such as Apollo Client.

Apollo Client provides an easy-to-use API for making GraphQL mutations.

```typescript
import {ApolloClient, InMemoryCache, gql} from '@apollo/client';

const client = new ApolloClient({
    uri: 'http://localhost:4000/graphql',
    cache: new InMemoryCache(),
});

const ADD_BOOK = gql`
mutation AddBook($title: String!, $author: String!) {
addBook(title: $title, author: $author) {
id
title
author
}
}
`;

client
    .mutate({
        mutation: ADD_BOOK,
        variables: {title: 'The Catcher in the Rye', author: 'J.D. Salinger'},
    })
    .then((result) => console.log(result));
```

### Mutations on the Backend

On the backend, there are several ways to perform mutations in a Fullstack TypeScript application.

```typescript
import {createConnection} from 'typeorm';
import {Book} from './entities/book.entity';

createConnection()
    .then(async (connection) => {
        const bookRepository = connection.getRepository(Book);

        const newBook = new Book();
        newBook.title = 'The Great Gatsby';
        newBook.author = 'F. Scott Fitzgerald';

        const savedBook = await bookRepository.save(newBook);
        console.log(savedBook);

    })
    .catch((error) => console.log(error));
```
