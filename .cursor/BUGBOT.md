# Bugbot rules

## JavaScript framework selector

The Node.js, Bun, and Deno quick starts wrap their content in `<FrameworkSelector runtime="...">`. When a reader selects Express, Fastify, Koa, or Hapi, every `<PlatformContent includePath="..." switchable />` inside it is swapped client-side for that framework's version. Those versions are only visible after selecting a framework, so they're easy to break without noticing. The setup is described in `docs/contributing/pages/components.mdx#frameworkselector` and configured in `src/components/frameworkSelector/frameworks.ts`.

If the PR changes any of these:

- `platform-includes/*/javascript.{express,fastify,koa,hapi}.mdx`
- `platform-includes/*/javascript.{node,bun,deno}.{express,fastify,koa,hapi}.mdx`
- `platform-includes/getting-started-node/javascript.mdx`
- `docs/platforms/javascript/guides/{node,bun,deno}/index.mdx`
- `src/components/frameworkSelector/frameworks.ts`

then check:

- A `javascript.<framework>.mdx` file is used on the Node.js, Bun, and Deno quick starts. Flag Node.js-only content in it, such as `node --import`, `@sentry/node`, or `@sentry/profiling-node`, and suggest moving it to `javascript.node.<framework>.mdx`.
- Framework-specific content that isn't inside a `switchable` include shows up for every framework. Flag it when it only applies to one framework.
- The runtime page's Markdown export doesn't include the framework versions. When the PR changes framework-specific guidance (for example `shouldHandleError` in `getting-started-capture-errors/javascript.express.mdx`), check that the framework's own guide page (`docs/platforms/javascript/guides/<framework>/index.mdx`) still says the same thing.
- Remind the author to check the preview with `?framework=<framework>` on each affected runtime page, for example `/platforms/javascript/guides/node/?framework=express`.
