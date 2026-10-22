---
name: commit-and-push
description: Commit and push the current project to the Gitee repository origin. Use when the user says 提交项目, commit and push, push to gitee, or similar requests. Do not use for other git tasks.
---

# Commit and Push to Gitee

## Remote Repository

- URL: `https://gitee.com/Zhang-tianrun77024/gaojiwangye`
- Name: `origin`

## Workflow

### 1. Check Repository Status

```powershell
git status
git log --oneline -5
```

Verify the current directory is a git repo and check for uncommitted changes.

### 2. Ensure Remote is Configured

```powershell
git remote -v
```

If the remote `origin` is missing or incorrect, set it:

```powershell
git remote add origin https://gitee.com/Zhang-tianrun77024/gaojiwangye
```

Or update an existing one:

```powershell
git remote set-url origin https://gitee.com/Zhang-tianrun77024/gaojiwangye
```

### 3. Stage All Changes

```powershell
git add -A
```

### 4. Commit

```powershell
git commit -m "提交项目更新 $(Get-Date -Format 'yyyy-MM-dd HH:mm')"
```

If there are no changes to commit, skip this step (working tree is clean).

### 5. Push

```powershell
git push -u origin master
```

If the `master` branch doesn't exist or the default branch is `main`:

```powershell
git push -u origin main
```

### 6. Verify

```powershell
git status
git log --oneline -1
```

Confirm the push succeeded and the working tree is clean.

## Notes

- If the user specifies a custom commit message, use it instead of the auto-generated one.
- If push fails due to non-fast-forward, do NOT force push — report the error and suggest resolving remote changes first.
- Always report the final status (success or failure) to the user.
