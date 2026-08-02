ROOM 404
## Objective
Understand directory brute-forcing and locate hidden administrative portals.

## Tools Used
* `nmap`
* `gobuster` / `dirb`
bash
nmap -sC -sV -oN nmap/initial 10.10.x.x

**Directory Enumeration:** Used `dirb` to enumerate directories on the given port:
bash
dirb http://10.10.x.x/
**Exploitation:** Located `/admin` panel and analyzed the login form logic.
Commands:
bash
git clone "git dumper URL"
cd git-dumper
ls

Install git-dumper

bash
git-dumper ".git file" dir_name/
cd dir_name
ls -la
cd .git
ls -la
gitleaks detect -v
git log 
git show "commit code"


## Key Takeaways
* Always sanitize input fields.
* Limit detailed error messages on production web pages.
