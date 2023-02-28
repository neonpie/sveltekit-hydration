# SvelteKit Hydration test

This is a simple test to check when event handlers are attached using SvelteKit. There are better ways of doing this, for example monkey patching using a proxy, but for now this will do.

This test was run on both dev and production versions.

SvelteKit sends the component state along with the HTML content to the client, **but** it still needs to initialize on the client via `start.js` and `app.js` and so on **before hydration can happen**. This is the order:

1. Set up client (start.js, app.js...)

   ```javascript
   // start.js in dev mode
   ...
   const client = create_client(app, target);

    init({ client });

    if (hydrate) {
    	await client._hydrate(hydrate);
    } else {
    	client.goto(location.href, { replaceState: true });
    }

    client._start_router();
   ```

````
2. Hydrate

To try this for yourself, run the app and open in Chrome or Firefox

Chrome Network:

1. Open Devtools
2. Network -> Disable Cache
3. Refresh
4. For dev -> find Counter and Greeter components in network; For prod -> find \_page... js in network and examine

Firefox Network:

1. Open Devtols
2. Network -> Disable Cache
3. Refresh
4. For dev -> Find Counter and Greeter components in network; For prod -> find \_page... js in network and examine

Chrome Profiler:

1. Open Devtools
2. Network -> Disable Cache
3. Performance -> Start Profiling and reload page -> Stop
4. For dev -> find Counter and Greeter components in network; for prod -> find \_page... js in network and see when it is loaded

Firefox Profiler:

1. Open Devtools
2. Network -> Disable Cache
3. Performance -> Start Recording -> Stop
4. For dev -> find Counter and Greeter components in network; for prod -> find \_page... js in network and see when it is loaded

---

# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
````

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
