# Nextjs (Routing Fundamentals)

## Routing types

- ```app``` routing
- ```pages``` routing

I'll focus on ```app``` routing.

## File Conventions

|file|description|
|---|---|
|```layout```|Shared UI for a segment and its children|
|```page```|Unique UI of a route and make routes publicly accessible|
|```loading```|Loading UI for a segment and its children|
|```not-found```|Not found UI for a segment and its children|
|```error```|Error UI for a segment and its children|
|```global-error```|Global Error UI|
|```route```|Server-side API endpoint|
|```template```|Specialized re-rendered Layout UI|
|```default```|Fallback UI for Parallel Routes|

## Component Hierarchy

The React components defined in special files of a route segment are rendered in a specific hierarchy:
- ```layout```
- ```template```
- ``` error```
- ```loading```
- ```not-found```
- ```page``` or nested ```layout```

![Component Hierarcy](../../images/file-conventions-component-hierarchy.jpg)

## Advanced Routing Patterns

- Parallel Routes
- Intercepting Routes

## Creating Routes

Next.js uses a file-system based router where folders are used to define routes.

Each folder represents a route segment that maps to a URL segment. To create a nested route, you can nest folders inside each other.

A special ```page.ts``` file is used to make route segments publicly accessible.

![Creating Routes](../../images/route-segments-to-path-segments.jpg)

![Creating Routes](../../images/defining-routes.jpg)

## Creating UI

Special file conventions are used to create UI for each route segment. The most common are pages to show UI unique to a route, and layouts to show UI that is shared across multiple routes.

For example, to create your first page, add a page.js file inside the app directory and export a React component:

```tsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```

## Pages

A page is UI that is unique to a route. You can define a page by default exporting a component from a page.js file.

For example, to create your index page, add the page.js file inside the app directory:

![Pages](../../images/page-special-file.jpg)

## Layouts

- UI that is shared between multiple routes.
- On navigation, layouts preserve state, remain interactive, and do nt re-render.
- Layouts can be nested.
- A layout can be defined by default exporting a react component from a ```layout.ts` file.
- The component should accept a ```children``` prop that will be populated with a child layout (if it exists) or a page during rendering.

For example, the layout will be shared with the /dashboard and /dashboard/settings pages:

![Layouts](../../images/layout-special-file.jpg)

```tsx
// app/dashboard/layout.tsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}: {
  children: React.ReactNode
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>
 
      {children}
    </section>
  )
}
```

## Root Layut (Required)

The root layout is defined at the top level of the app directory and applies to all routes. This layout is required and must contain ```html``` and ```body``` tags, allowing you to modify the initial HTML returned from the server.

```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        {/* Layout UI */}
        <main>{children}</main>
      </body>
    </html>
  )
}
```

## Nesting Layouts

By default, layouts in the folder hierarchy are nested, which means they wrap child layouts via their children prop. You can nest layouts by adding layout.js inside specific route segments (folders).

