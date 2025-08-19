Git Submodule Concept with Examples
🔹 What is a Git Submodule?
A Git submodule is a Git repository inside another Git repository. It allows you to track a project dependency (another repo) while keeping it version-controlled separately.

👉 Think of it like this:
- You have a main project repo.
- Inside it, you embed another repo (submodule), which is managed independently.

This is useful when:
- You want to include libraries or components developed in a separate repo.
- You need to track a specific commit/tag/branch of another repository.
- 
🔹 Key Points
1. A submodule is linked by reference (commit hash), not by copying files.
2. Each submodule has its own `.git` directory (not merged with parent repo).
3. The main repo just stores a pointer to the submodule’s commit.
   
🔹 Basic Commands with Examples
1. Add a Submodule
Command:
git submodule add https://github.com/example/library.git libs/library

- Remote repo: https://github.com/example/library.git
- Local folder: libs/library

This creates a `.gitmodules` file:
[submodule "libs/library"]
    path = libs/library
    url = https://github.com/example/library.git
    
2. Clone a Repo with Submodules
If you clone a project that contains submodules:
git clone https://github.com/example/project.git

The submodules won’t be fetched automatically. Initialize and update them:
git submodule init
git submodule update

Or in one command:
git clone --recurse-submodules https://github.com/example/project.git

3. Update Submodules
If the submodule has new commits:
cd libs/library
git pull origin main

Then go back to the parent repo and commit the new reference:
cd ../..
git add libs/library
git commit -m "Update submodule to latest commit"

4. Remove a Submodule
Steps to remove:
git submodule deinit -f -- libs/library
git rm -f libs/library
rm -rf .git/modules/libs/library

5. Example Project Structure
project/
│── .git/
│── .gitmodules
│── app/
│── libs/
    └── library/   (submodule repo)
   
🔹 Real-Time Use Case
Suppose you’re building a web app:
- Main repo → your web application code
- Submodule repo → shared authentication module used across multiple projects

Instead of copying the code, you add it as a submodule:
git submodule add https://github.com/company/auth-module.git libs/auth

Now your app always points to a fixed commit of auth-module.
When updates happen, you just pull the latest changes in the submodule and commit the new reference.

✅ Summary
- Git submodules let you include one repo inside another.
- They track commits, not just branches.
- Useful for dependencies/libraries shared across projects.

