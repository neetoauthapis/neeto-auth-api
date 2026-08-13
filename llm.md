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
