# AskGit Tables

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
