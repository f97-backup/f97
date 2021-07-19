1. Delete all local git branches

```bash
git branch --merged | grep -v \* | xargs git branch -D 
```
