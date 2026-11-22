# Graphify for Codex

Official Graphify plugin source for Codex and ChatGPT. It connects your coding agent to the repositories you index in [Graphify](https://graphify.com), so the agent can use the code graph, Memory and PR review status through Graphify's hosted MCP server.

The server is `https://api.graphify.com/mcp`. Sign-in uses OAuth in the browser. There is no API key to paste and no secret in this repository.

The hosted MCP serves the code graph, Memory and `review_status`. Wiki lives in the Graphify app at [app.graphify.com](https://app.graphify.com); it is not served over MCP.

The open-source Graphify CLI is a separate local tool: [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) (PyPI: `graphifyy`, Apache 2.0).

[Graphify](https://graphify.com) · [Docs](https://docs.graphify.com/integrations/codex) · [Install in ChatGPT / Codex](https://chatgpt.com/plugins/plugin_asdk_app_6abe89f7f5d88191b9422522bb8562a4) · [Cursor](https://github.com/Graphify-Labs/graphify-cursor-plugin) · [Claude](https://github.com/Graphify-Labs/graphify-claude-plugin)

## Install

The quickest path is the official OpenAI plugin directory, which Codex and ChatGPT share:

1. Open the [Graphify listing](https://chatgpt.com/plugins/plugin_asdk_app_6abe89f7f5d88191b9422522bb8562a4) and select **Install plugin**, or in Codex CLI open `/plugins` and search **Graphify**.
2. Connect your Graphify account and finish the browser sign-in.
3. Start a new Codex or ChatGPT session so the Graphify tools load.

Or add this repository as a Codex marketplace, then install the plugin:

```bash
codex plugin marketplace add Graphify-Labs/graphify-codex-plugin
codex plugin add graphify@graphify
```

The second command follows OpenAI's `codex plugin add PLUGIN_NAME@MARKETPLACE_NAME` form. The marketplace name in this repo is `graphify`.

Manual setup, including the Codex IDE extension (which does not support plugins yet):

```bash
codex mcp add graphify --url https://api.graphify.com/mcp
codex mcp login graphify
```

Use one path. Two connections show every Graphify tool twice.

You need a Graphify account and at least one repository with the status **Indexed**. The [quickstart](https://docs.graphify.com/platform/quickstart) connects GitHub and starts indexing.

## Try it

After the tools load, ask:

- Map my selected repository: its main areas, how requests flow through it, and the files I should read first. Cite files.
- What could break if I change the session token validator's signature? List its callers, affected files and linked tests.
- Use review_status to list Graphify's recent PR reviews, with status, gate result and top findings.

## What it can and cannot do

- It answers from repositories already indexed in your Graphify workspace, not from arbitrary local files.
- Repository graph tools are read-only: they do not edit files, open pull requests or start reviews.
- Some Memory tools can write workspace notes. Read each tool request before you approve it.
- Switching workspace changes which repositories the session can read.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| Graphify rejects the connection | You added the server but did not sign in. Run `codex mcp login graphify`. |
| `graphify` is missing from `/mcp` | Start a new Codex session after adding it. |
| The tools return no repositories | The repository is not indexed yet, or it is in a different workspace. Check [Repositories and builds](https://docs.graphify.com/platform/repositories). |
| Every Graphify tool appears twice | You have both the plugin and a manual server entry. Remove one. |
| Only a `graphify_setup` tool appears, or tools say Graphify isn't set up yet | Finish setup at [app.graphify.com/onboarding](https://app.graphify.com/onboarding), enable a repository, wait until it is **Indexed**, start a new session, and sign in again if needed. |

The [Codex guide](https://docs.graphify.com/integrations/codex) has the full walkthrough.

## License

This plugin package is licensed under [Apache-2.0](./LICENSE). Use of the hosted Graphify service is governed by its [terms](https://graphify.com/terms) and [privacy policy](https://graphify.com/privacy).

Report security issues as described in [SECURITY.md](./SECURITY.md).
