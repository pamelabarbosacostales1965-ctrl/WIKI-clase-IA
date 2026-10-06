# Upload the repository and invite @danielriofrio

[Home](README.md)

## Browser workflow

1. Extract `cmp4004e-ai-study-wiki.zip` on your computer.
2. Sign in to GitHub and create a repository named, for example, `cmp4004e-ai-study-wiki`. Choose the visibility requested by your instructor. Do not initialize it with a second README if you plan to upload this folder's contents.
3. Open the repository's file-upload interface and upload the **contents** of `cmp4004e-ai-study-wiki`, including its `wiki` folder. Keep README at the repository root. Commit the upload with a message such as “Add AI class study wiki.”
4. Open README and verify chapter links and formulas. If your browser does not preserve folders during upload, use the Git workflow below.
5. Open repository **Settings**, then **Collaborators** under access settings. Authenticate if prompted.
6. Choose **Add people**, search for `danielriofrio` (without the @), select the correct GitHub account, and send the invitation.
7. Check the invitation is listed as pending or accepted. Share the repository URL through your course's requested channel. A pending invitation is not yet an accepted invitation.

GitHub documents collaborator invitations in [its official instructions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository). Interface labels may vary by account or repository type; organization repositories have their own access-management flow.

## Optional Git workflow

Open a terminal inside the extracted repository folder, after creating an empty GitHub repository. Replace `YOUR_USERNAME` with your username and use the repository name you actually created.

```sh
git init
git add .
git commit -m "Add AI class study wiki"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/cmp4004e-ai-study-wiki.git
git push -u origin main
```

Authenticate using your normal GitHub-supported Git method. Then send the collaborator invitation through Settings as above.

## Submission checklist

- README appears at repository root.
- All chapters and reference files are present.
- You reviewed the wiki and its AI assistance disclosure.
- The correct `danielriofrio` account was invited.
- You shared the actual repository URL.

**Publication note (October 6, 2026):** the GitHub Wiki edition has been published at https://github.com/pamelabarbosacostales1965-ctrl/WIKI-clase-IA/wiki. This repository edition accompanies it. No collaborator invitation has been sent by this task.
