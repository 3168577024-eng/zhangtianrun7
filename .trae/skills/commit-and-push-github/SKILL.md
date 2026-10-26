---
name: commit-and-push-github
description: Commit and push the current project to the GitHub repository named github. Use when the user says 提交到GitHub, push to github, commit to github, or similar requests. Do not use for Gitee pushes.
---

# Commit and Push to GitHub

## Remote Repository

- URL (SSH, preferred since public key is configured): `git@github.com:3168577024-eng/zhangtianrun7.git`
- URL (HTTPS, alternative): `https://github.com/3168577024-eng/zhangtianrun7`
- Remote name: `github` (Gitee keeps using `origin`)

## Workflow

### 1. Check Repository Status

```powershell
git status
git log --oneline -5
```

### 2. Ensure Remote is Configured

```powershell
git remote -v
```

If the remote `github` is missing or incorrect, set it:

```powershell
git remote add github git@github.com:3168577024-eng/zhangtianrun7.git
```

Or update an existing one:

```powershell
git remote set-url github git@github.com:3168577024-eng/zhangtianrun7.git
```

If SSH auth fails (public key unavailable), switch to HTTPS:

```powershell
git remote set-url github https://github.com/3168577024-eng/zhangtianrun7
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
git push -u github master
```

If the default branch is `main`:

```powershell
git push -u github main
```

### 6. Verify

```powershell
git status
git log --oneline -1
```

Confirm the push succeeded and the working tree is clean.

## Notes

- If the user specifies a custom commit message, use it instead of the auto-generated one.
- If push fails due to non-fast-forward (e.g. the GitHub repo has commits such as an initial README), do NOT force push — report the error and suggest resolving remote changes first.
- Pushing to Gitee (`origin`) is handled by the separate commit-and-push skill.
- Always report the final status (success or failure) to the user.
