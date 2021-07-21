```sql
-- unique commit author names
SELECT DISTINCT(author_name) FROM commits
```

```sql
-- commit counts by author name
SELECT
    author_name, count(*) 
FROM commits
WHERE parent_count < 2 -- ignore merge commits
GROUP BY author_name
ORDER BY count(*) DESC
```

```sql
-- commit counts by author email domain
SELECT
    count(*),
    substr(author_email, instr(author_email, '@')+1) AS email_domain -- https://sqlite.org/lang_corefunc.html
FROM commits
WHERE parents < 2 -- ignore merge commits
GROUP BY email_domain
ORDER BY count(*) DESC
```

```sql
-- top 50 files changed most frequently in the past year
SELECT file_path, COUNT(*)
FROM commits, stats('', commits.hash)
WHERE
commits.author_when > DATE('now', '-12 month')
AND commits.parents < 2 -- ignore merge commits
GROUP  BY file_path
ORDER  BY COUNT(*) DESC
LIMIT  50
```
