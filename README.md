```sh
#!/bin/sh
FILES=$(git diff --cached --name-only --diff-filter=ACMR | sed 's| |\\ |g')
[ -z "$FILES" ] && exit 0

echo "$FILES" | grep ^inventory/ | xargs -I{} /bin/sh -c '[[ $(sed -n '"'"'/^$ANSIBLE_VAULT;/p;q'"'"' {}) ]]||exit 1'||(echo "Please encrypt inventory file(s)!";exit 1)
```
