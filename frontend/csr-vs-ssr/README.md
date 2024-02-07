# CSR vs SSR

There are several reasons why a frontend developer might choose to use CSR instead of opting for SSR, depending on the project requirements, the team's expertise, and specific deployment needs.

## General considerations

Some considerations:

- __Custom Server configuration__: If you need to use a custom server configuration, you might want to use CSR. This is because you can use a custom server configuration to serve your static files, and then use a client-side framework to render the content on the client side. Most SSR frameworks provide a layer of abstraction over the server configuration.

- __Resources__: You can decide to make either the client or the server responsible of rendering the content of the application.

- __Network__: If you want to reduce the amount of data transferred over the network, you might want to use CSR.

- __Offline experience__: By caching the application and data locally, a CSR app can still be navigable even without an internet connection. This would not be possible with server-side routing.

## Client-side routing

With client-side routing, navigation between different parts of an application is handled within the browser without requiring a page reload from the server. This provides some advantages over traditioanl server-side routing:

- __Faster page transitions__: The entire page doesn't need to be reloaded from the server.
- __Reduced server load__: The server doesn't need to process every navigation request.
- __Smooth user experience__: It can provide a more seamless and app-like user experience by navigating through different parts of the app without a full page refresh.
- __Enhanced offline experiences__: By caching the application and data locally, the app might still be navigable even without an internet connection.
- __Fine-grained control over transitions__: Developers can implement custom animations, loading states, or partial updates to the page, providing a more dynamic and engaging user interface.
- __Stateful UIs__: It's easier to maintain state across different views, allowing for features like scroll position restoration, complex animations based on user interactions, or maintaing the state of a partially completed form.
