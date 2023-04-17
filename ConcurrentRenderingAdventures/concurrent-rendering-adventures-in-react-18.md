# REACT SUSPENSE

React Suspense allows us to create better user experiences by rendering components asynchronously. We can internally
think
about it like specifically rendering something while in every state of a promise
It enables components to be suspended while they wait for data to be loaded, and then to display data as soon as it
is available. This can help to reduce loading times and make the application more responsive to user interactions by
giving the final user feedback easily

We can use Parallel and Nested Suspense as we need, so in case of needing it we can

```jsx
<Suspense>
    <Suspense>
    </Suspense>
</Suspense>
<Suspense>
</Suspense>
```

## < Suspense >

In order to use Suspense you only need to wrap your components in a <Suspense> component
and providing a fallback element to display while the data is being loaded

```jsx
<Suspense fallback={<div>Loading...</div>}>
    <DataComponent/>
</Suspense>

```

## Error Boundaries

But this way we are only covering the "while" fetching data case.
No problem!, in the case of an error, React Suspense provides Error Boundaries in order to handle errors.

In order to use Error Boundaries you only need to wrap your components in a <ErrorBoundary> component as we did with
Suspense

```jsx
<ErrorBoundary FallbackComponent={ErrorFallbackComponent}>
    <Suspense fallback={<div>Loading...</div>}>
        <DataComponent/>
    </Suspense>
</ErrorBoundary>
```

## Suspense List

The Suspense List component takes two props: revealOrder and tail. The revealOrder prop specifies the order in which the
items in the list should be loaded. It can take one of three values: "forwards", "backwards", or "together".
The tail prop specifies what should be displayed while the items are loading.
It can take any valid React element.

This way we can easily modify the Suspense Behavior depending on our needs

```jsx
<SuspenseList revealOrder="backwards" tail={<div>Loading...</div>}>
    <Suspense fallback={<div>Loading item 1...</div>}>
        <FirstSuspense/>
    </Suspense>
    <Suspense fallback={<div>Loading item 2...</div>}>
        <SecondSuspense/>
    </Suspense>
    <Suspense fallback={<div>Loading item 3...</div>}>
        <ThirdSuspense/>
    </Suspense>
</SuspenseList>
```

### Reveal Order

The revealOrder prop specifies the order in which the items in the list should be loaded.
There are three possible values:

- "forwards": items are loaded in the order they appear in the list, from top to bottom.
- "backwards": items are loaded in the reverse order they appear in the list, from bottom to top.
- "together": all items are loaded together.

### Tail

The tail prop specifies what should be displayed while the items are loading. It can take any valid React element.

# REACT CONCURRENT RENDERING

React concurrent rendering is only available at 18 and higher versions
allows for smoother and more responsive user interfaces.
It enables React to perform multiple tasks at the same time,
rather than blocking the UI while waiting for one task to complete. And at the same time this improves performance
We have to be careful when using states because concurrent rendering can cause UI to differ from state

In traditional React rendering, changes to the state or props of a component trigger a synchronous re-render of the
component and its children. This can be a time-consuming process, especially if the component has a large number of
children or expensive computations.

With Concurrent Rendering, React can split the work of rendering a component and its children into smaller units of work
called "fibers".
Fibers are lightweight and can be interrupted and resumed at any time, allowing React to work on other tasks while
waiting for the current
task to complete.

This means that the UI remains responsive even when React is performing complex tasks in the background.
For example, if a user is scrolling through a long list of items and reaches the end of the current batch of data,
Concurrent Rendering allows React to fetch and render the next batch of data without blocking the UI.

in React 18 it looks like we are trying to make react more and more Async-friendly

## HOW TO?

Even when Concurrent Rendering is enabled by default in React 18 there are a few best practices that can help you get
the most out of Concurrent Rendering:

- Split large components into smaller ones: Components with a large number of children can be split into smaller
  components
  to improve performance and enable Concurrent Rendering.

- Use the useTransition hook: The useTransition hook allows you to defer updates to a component until a certain
  condition is met.
  This can be useful for improving the perceived performance of an application by showing a loading spinner or
  placeholder content while data is being fetched.

- You can also use startTransition for Class based components

- Use the useDeferredValue hook: The useDeferredValue hook allows you to defer updates to a component until the value
  being updated has remained stable for a certain period of time. This can be useful for improving the perceived
  performance of an application by reducing the number of unnecessary updates.

# COMBINING SUSPENSE AND TRANSITIONS

We have seen how powerful those new features can be separately, we can get much more out of them by using them together.
Suspense and Transitions can be used together to create an even smoother and even more responsive user experience.
We can use Suspense to handle the loading of data, and Transitions to control the timing of updates to the UI.

```jsx
const MixedComponent = () => {
    const [data, setData] = useState(null);
    const [isPending, startTransition] = useTransition({timeoutMs: 1000});

    useEffect(() => {
        async function fetchData() {
            startTransition(() => {
                const response = await fetch('google.com/data');
                const json = await response.json();
                setData(json);
            });
        }

        fetchData();
    }, [startTransition]);

    return (
        <Suspense fallback={<p>Loading...</p>}>
            {data && (
                <DataComponent data={data}/>
            )}
        </Suspense>

```
