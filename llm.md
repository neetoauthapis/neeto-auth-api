# LLM Guidelines for NeetoAuth API Docs

## Important Rules

1. **Never make direct changes to the `bundled` folder.** The `bundled` folder is auto-generated and should not be edited manually.

2. **Always make changes in the `docs` folder.** All source content lives in the `docs` folder. This is where edits should be made.

3. **After making any changes, run `yarn build:dev`.** This regenerates the API documentation in the `bundled` folder from the `docs` folder.

4. **Both `docs` and `bundled` changes must be committed and pushed.** After running `yarn build:dev`, the updated files in both the `docs` folder and the `bundled` folder need to be checked in and pushed together.

## CLI reference

5. **Never hand-edit `snippets/cli/**` or `cli-reference/overview.mdx`.** They are generated from `cli/catalog.json` by `scripts/generate-cli-reference.mjs` and are overwritten on every build.

6. **Refresh them with `yarn cli:catalog && yarn cli:build`.** `cli:catalog` re-snapshots the catalog from an installed `neetoauth` binary, so build it from the CLI repo's latest `main` first - a stale binary silently drops newer commands. `cli:build` alone runs in CI, which has no binary.

7. **The hand-written CLI pages are `cli/*.mdx` and `cli-reference/{users,products,utility}.mdx`.** Adding a resource to the CLI means adding a page here and an entry in `groupToPage` in `scripts/generate-cli-reference.mjs`; an unmapped group falls back to the utility page and warns on stderr.

8. **Publish `neetoauth.com/cli/install.{sh,ps1,cmd}` for installation, never the `neeto-downloads` S3 URLs.** The bucket appears in the CLI's own `update` command and release scripts, but it is infrastructure rather than a public interface.

## MCP Documentation Rules

1. **`mcp/introduction.mdx`, `mcp/authentication.mdx`, `mcp/connect.mdx` and `mcp/troubleshooting.mdx` follow the shared neeto MCP template.** Every neeto product runs the same MCP server stack, so every neeto docs site carries the same sections, tables, client list and troubleshooting entries on these four pages, with only the product name, its resources, its help center and its support address swapped. The NeetoCal pages in neeto-cal-api are the reference copy. Change the shared wording in every product's docs or in none.

2. **The server endpoint is always the product's own connect host, `https://connect.neetoauth.com/mcp/messages`.** Never document a workspace subdomain host such as `https://YOUR_SUBDOMAIN.neetoauth.com/mcp/messages`. The credential selects the workspace, not the host.

3. **The documented clients are Claude, ChatGPT, Claude Code, Codex, Cursor, Gemini CLI, VS Code, Windsurf and Antigravity.** Antigravity is documented with an API key only. Do not add or drop a client on one product's docs alone.

4. **`mcp/examples.mdx` and `mcp/tools.mdx` are product specific.** Tool names and descriptions come from the product's `app/tools/*.rb`, never from another product's docs.
