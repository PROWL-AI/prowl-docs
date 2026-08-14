# Before you open this

**Almost everything here is generated.** The tool pages, the tool index, the MCP tools
reference and `CHANGELOG.md` are rendered from the Prowl codebase and rewritten on every
release — a fix applied to a published file is overwritten by the next sync, usually
within a day.

So:

- **Found something wrong?** Open an **issue** instead. Quote the file and the line. The
  fix lands in the generator, and reaches this repository on the next sync.
- **A tool's schema, error table or example looks wrong?** That is a bug in Prowl, not in
  the documentation. An issue is the right place, and it is genuinely useful — those
  pages are rendered from the live registry, so a wrong page usually means a wrong
  registry entry.

A pull request is still welcome for things this repository actually owns: typos in the
issue templates, this file, or a broken link between pages that survives a regeneration.

## If you are opening one anyway

- [ ] The file I changed is not generated (it is not under `docs/tools/`, not
      `docs/mcp/tools-reference.md`, and not `CHANGELOG.md`)
- [ ] I checked the change survives a regeneration
- [ ] What is wrong, and where I saw it:
