# knip-next-jest-monorepo-bug

This repository demonstrates how to reproduce a bug that occurs when running knip in a monorepo context with a Next.js + Jest app as an npm workspace.

## Assembly

This repo was assembled by performing the following actions:

1. Initialize a new npm project and set `workspaces` in package.json to an array with `apps/*` as the only element
2. Initialize knip with `npm init @knip/config`
3. Create an `apps/` directory and `cd` into it
4. Following the [Next.js + Jest setup guide](https://nextjs.org/docs/app/guides/testing/jest), run the command `npx create-next-app@latest --example with-jest next-app`
5. Return to the root directory and run the command `npm run knip`
6. Observe an error similar to the following:
```
❯ npm run knip

> knip
> knip

Analyzing workspace (apps/next-app)…
/Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/next/dist/lib/find-pages-dir.js:42
        throw Object.defineProperty(new Error("> Couldn't find any `pages` or `app` directory. Please create one under the project root"), "__NEXT_ERROR_CODE", {


Error: > Couldn't find any `pages` or `app` directory. Please create one under the project root
    at findPagesDir (/Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/next/dist/lib/find-pages-dir.js:42:37)
    at /Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/next/dist/build/jest/jest.js:128:75
    at async Object.resolveConfig (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/plugins/jest/index.js:80:23)
    at async runPlugin (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/WorkspaceWorker.js:273:40)
    at async WorkspaceWorker.runPlugins (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/WorkspaceWorker.js:314:13)
    at async build (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/graph/build.js:95:35)
    at async main (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/index.js:43:88)
    at async run (file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/cli.js:26:111)
    at async file:///Users/elijah.olmos/dev/knip-next-jest-monorepo-bug/node_modules/knip/dist/cli.js:111:1

Node.js v20.18.1
```
