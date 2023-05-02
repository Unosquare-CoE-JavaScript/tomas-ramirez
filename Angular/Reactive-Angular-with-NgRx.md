# NgRx

NgRx Store is a state management library for Angular applications. It provides a predictable and centralized way to
manage application state, making it easier to build complex applications with multiple components and data sources.
Or even easier to have a single truth source for our Angular applications

NgRx Store is built on top of the Redux architecture, which is a popular pattern for managing state in JavaScript
applications and different frameworks and ecosystems such as react, At its core, NgRx Store is based on three key
concepts:

- Store: the central data store for the application, which holds the current state of the application.

- Actions: plain JavaScript objects that represent an intent to change the state of the application.

- Reducers: pure functions that take the current state and an action, and return a new state.

Simple right?Well, using these concepts, NgRx Store provides a way to manage application state in a consistent way.

## HOW TO

To use NgRx Store in your Angular application, you'll need to install the @ngrx/store package
Once you've installed the package, you can create a store by importing the StoreModule and passing it a reducer

```typescript
import {StoreModule} from '@ngrx/store';
import {reducer} from './reducers';

@NgModule({
    imports: [
        BrowserModule,
        StoreModule.forRoot(reducer)
    ],
    declarations: [
        AppComponent
    ],
    bootstrap: [AppComponent]
})
export class AppModule {
}
```

Once you've set up the store, you can use the Store service to access the current state of the application and dispatch
actions:

```typescript
import {Component} from '@angular/core';
import {Store} from '@ngrx/store';
import {increment} from './actions';

@Component({
    selector: 'app-root',
    template: `
<button (click)="increment()">Increment</button>
<p>Counter: {{ counter }}</p>
`
})
export class AppComponent {
    counter: number;

    constructor(private store: Store<{ counter: number }>) {
        store.select('counter').subscribe((counter) => {
            this.counter = counter;
        });
    }

    increment() {
        this.store.dispatch(increment());
    }
}
```

## Actions and entities in depth

## Actions

Actions in NgRx Store are used to represent anything that may cause any change to the state of the application. An
action is a plain JavaScript object that has a type property, which describes the type of action, and an optional
payload property, which contains any data required to perform the action.

Actions are used to trigger updates to the application state by dispatching them to the NgRx Store. When an action is
dispatched, it is processed by one or more reducers, which update the application state based on the action type and
payload.

Actions are typically organized into action classes, which provide a more structured and type-safe way to define
actions.

```typescript
export class LoadBooks implements Action {
    readonly type = '[Books] Load Books';
}
```

### Entities

Entities in NgRx Store are used to represent complex objects in the application state. An entity is a plain JavaScript
object that has an id property, which uniquely identifies the object, and any additional properties required to
represent the object.

Entities are usually organized into feature stores, they group related entities together in the application state.

```typescript
export interface Book {
    id: string;
    title: string;
    author: string;
    published: Date;
}

export interface BooksState {
    ids: string[];
    entities: { [id: string]: Book };
}
```

## Selectors & Side Effects & Facades in depth

### Selectors

Selectors in NgRx Store are used to derive data from the application state. A selector is a pure function that takes the
application state as input and returns a derived value. Selectors can be used to calculate derived properties, filter
data, and combine data from multiple sources.

Selectors are usually organized into feature selectors, they group related selectors together in the application.

```typescript
export const getBooks = (state: AppState) => state.books;

export const getSelectedBook = createSelector(
    getBooks,
    (books: Book[], props: { id: string }) => {
        return books.find(book => book.id === props.id);
    }
);
```

### Side Effects

Side effects in NgRx Store are used to perform asynchronous operations that may affect the application state. A side
effect is a function that takes an action as input and returns an observable that emits one or more actions over time.
Side effects can be used to fetch data from external APIs, update data in a database, and perform other asynchronous
operations.

Side effects are usually organized into feature effects, they group related effects together in the application.

```typescript
@Injectable()
export class BooksEffects {
    constructor(private actions$: Actions, private booksService: BooksService) {
    }

    loadBooks$ = createEffect(() =>
        this.actions$.pipe(
            ofType('[Books] Load Books'),
            mergeMap(() =>
                this.booksService.getBooks().pipe(
                    map(books => ({type: '[Books] Books Loaded', payload: books})),
                    catchError(() => EMPTY)
                )
            )
        )
    );
}
```

### Facades

A facade is a higher-level abstraction that provides a simplified interface to a complex system. In the context of NgRx
Store, a facade is an API layer that sits on top of the NgRx Store and exposes a simplified interface for accessing and
modifying the application state.

Facades can be used to simplify the management of application state and reduce the coupling between components and the
store. By providing a simplified interface to the store, facades can make it easier to write components that are more
focused on their specific responsibilities, rather than worrying about managing the store directly.

```typescript
@Injectable({
    providedIn: 'root',
})
export class BooksFacade {
    books$: Observable<Book[]> = this.store.select(getBooks);
    selectedBook$: Observable<Book> = this.store.select(getSelectedBook, {id: this.selectedId});

    constructor(private store: Store<AppState>) {
    }

    loadBooks(): void {
        this.store.dispatch(BooksActions.loadBooks());
    }

    selectBook(id: string): void {
        this.selectedId = id;
    }
}
```
