---
name: update-github-info
on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *'
engine: copilot
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog  # includes both GitHub Blog and Changelog
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
---

# Update GitHub Info

This workflow automatically updates the GitHub Info content by:

1. Reading Mona's notes for guidance
2. Fetching the latest updates from GitHub Blog
3. Fetching recent changes from GitHub Changelog
4. Updating the website content
5. Opening a pull request for review

## Important Notes

- **Do not auto-compile this workflow.** The lock file is managed by the repository maintainers.
- Only modify `site/content/github-info.md` - do not change other files.
- All changes must go through a pull request for Mona to review.

## Task

You are an assistant helping to keep the GitHub Info website up to date. Follow these steps:

1. **Read the guidelines**: Read `notes/mona-notes.md` to understand the style and requirements for updates.

2. **Fetch latest GitHub updates**:
   - Web fetch: https://github.blog/latest/
   - Web fetch: https://github.blog/changelog/
   - Extract the 3-5 most recent and relevant updates for developers

3. **Update the content**: Modify `site/content/github-info.md` to include recent GitHub updates following Mona's guidelines:
   - Keep summaries short and practical
   - Prefer updates that help developers learn GitHub faster
   - Mention the source (GitHub Blog or GitHub Changelog)
   - Format as a bullet list with dates if available

4. **Open a pull request for Mona**: Use the `create-pull-request` tool to:
   - Create a branch named `update-github-info-<date>`
   - Add a clear PR title: "chore: update GitHub info with latest changes"
   - Include a description of what was added
   - **Request Mona (@mona) for review** so she can approve before merging

Remember: Only update `site/content/github-info.md`. Do not modify other files.
