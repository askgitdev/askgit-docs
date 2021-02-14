## `commits`

Similar to `git log`, the `commits` table includes all commits in the history of the currently checked out commit.

| Column          | Type     |
|-----------------|----------|
| id              | TEXT     |
| message         | TEXT     |
| summary         | TEXT     |
| author_name     | TEXT     |
| author_email    | TEXT     |
| author_when     | DATETIME |
| committer_name  | TEXT     |
| committer_email | TEXT     |
| committer_when  | DATETIME |
| parent_id       | TEXT     |
| parent_count    | INT      |

## `blame`

Similar to `git blame`, the `blame` table includes blame information for all files in the current HEAD.

| Column       | Type     |
|--------------|----------|
| line_no      | INT      |
| file_path    | TEXT     |
| commit_id    | TEXT     |
| line_content | TEXT     |


## `stats`

| Column    | Type |
|-----------|------|
| commit_id | TEXT |
| file_path | TEXT |
| additions | INT  |
| deletions | INT  |

## `files`

The `files` table iterates over _ALL_ the files in a commit history, by default from what's checked out in the repository.
The full table is every file in every tree of a commit history.
Use the `commit_id` column to filter for files that belong to the work tree of a specific commit.

| Column     | Type |
|------------|------|
| commit_id  | TEXT |
| path       | TEXT |
| contents   | TEXT |
| executable | BOOL |


## `branches`

| Column | Type |
|--------|------|
| name   | TEXT |
| remote | BOOL |
| target | TEXT |
| head   | BOOL |

## `tags`

| Column       | Type |
|--------------|------|
| full_name    | TEXT |
| name         | TEXT |
| lightweight  | BOOL |
| target       | TEXT |
| tagger_name  | TEXT |
| tagger_email | TEXT |
| message      | TEXT |
| target_type  | TEXT |

## `github_org_repos` and `github_user_repos`

These tables can be queried as table-valued functions expecting a single parameter, like so:

```sql
-- return all repos from a github *org*
SELECT * FROM github_org_repos('augmentable-dev')

-- return all repos from a github *user*
SELECT * FROM github_user_repos('augmentable-dev')
```

| Column            | Type     |
|-------------------|----------|
| id                | INT      |
| node_id           | TEXT     |
| name              | TEXT     |
| full_name         | TEXT     |
| owner             | TEXT     |
| private           | BOOL     |
| description       | TEXT     |
| fork              | BOOL     |
| homepage          | TEXT     |
| language          | TEXT     |
| forks_count       | INT      |
| stargazers_count  | INT      |
| watchers_count    | INT      |
| size              | INT      |
| default_branch    | TEXT     |
| open_issues_count | INT      |
| topics            | TEXT     |
| has_issues        | BOOL     |
| has_projects      | BOOL     |
| has_wiki          | BOOL     |
| has_pages         | BOOL     |
| has_downloads     | BOOL     |
| archived          | BOOL     |
| pushed_at         | DATETIME |
| created_at        | DATETIME |
| updated_at        | DATETIME |
| permissions       | TEXT     |

## `github_pull_requests`

This table expects 2 parameters, `github_pull_requests('augmentable-dev', 'askgit')`:

```sql
SELECT count(*) FROM github_pull_requests('augmentable-dev', 'askgit') WHERE state = 'open'
```

| Column                    | Type     |
|---------------------------|----------|
| id                        | INT      |
| node_id                   | TEXT     |
| number                    | INT      |
| state                     | TEXT     |
| locked                    | BOOL     |
| title                     | TEXT     |
| user_login                | TEXT     |
| body                      | TEXT     |
| labels                    | TEXT     |
| active_lock_reason        | TEXT     |
| created_at                | DATETIME |
| updated_at                | DATETIME |
| closed_at                 | DATETIME |
| merged_at                 | DATETIME |
| merge_commit_sha          | TEXT     |
| assignee_login            | TEXT     |
| assignees                 | TEXT     |
| requested_reviewer_logins | TEXT     |
| head_label                | TEXT     |
| head_ref                  | TEXT     |
| head_sha                  | TEXT     |
| head_repo_owner           | TEXT     |
| head_repo_name            | TEXT     |
| base_label                | TEXT     |
| base_ref                  | TEXT     |
| base_sha                  | TEXT     |
| base_repo_owner           | TEXT     |
| base_repo_name            | TEXT     |
| author_association        | TEXT     |
| merged                    | BOOL     |
| mergeable                 | BOOL     |
| mergeable_state           | BOOL     |
| merged_by_login           | TEXT     |
| comments                  | INT      |
| maintainer_can_modify     | BOOL     |
| commits                   | INT      |
| additions                 | INT      |
| deletions                 | INT      |
| changed_files             | INT      |

## `github_issues`

This table expects 2 parameters, `github_issues('augmentable-dev', 'askgit')`:

```sql
SELECT count(*) FROM github_issues('augmentable-dev', 'askgit') WHERE state = 'open'
```


| Column                    | Type     |
|---------------------------|----------|
| id                        | INT      |
| node_id                   | TEXT     |
| number                    | INT      |
| state                     | TEXT     |
| locked                    | BOOL     |
| title                     | TEXT     |
| user_login                | TEXT     |
| body                      | TEXT     |
| labels                    | TEXT     |
| active_lock_reason        | TEXT     |
| created_at                | DATETIME |
| updated_at                | DATETIME |
| closed_at                 | DATETIME |
| merged_at                 | DATETIME |
| merge_commit_sha          | TEXT     |
| assignee_login            | TEXT     |
| assignees                 | TEXT     |
| url                       | TEXT     |
| html_url                  | TEXT     |
| comments_url              | TEXT     |
| events_url                | TEXT     |
| repository_url            | TEXT     |
| comments                  | INT      |
| milestone                 | TEXT     |
| reactions                 | INT      |
