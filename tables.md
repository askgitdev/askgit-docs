## `commits`

Similar to `git log`, the `commits` table includes all commits in the history of the currently checked out commit.

| Column          | Type     |
|-----------------|----------|
| hash            | TEXT     |
| message         | TEXT     |
| author_name     | TEXT     |
| author_email    | TEXT     |
| author_when     | DATETIME |
| committer_name  | TEXT     |
| committer_email | TEXT     |
| committer_when  | DATETIME |
| parents         | INT      |

Params:
  1. `repository` - path to a remote (http(s)) repository
  2. `rev` - return commits starting at this revision (i.e. branch name or SHA), defaults to `HEAD`

```sql
-- return all commits starting at HEAD
SELECT * FROM commits

-- specify an alternative repo on disk
SELECT * FROM commits('/some/path/to/repo')

-- clone a remote repo and use it
SELECT * FROM commits('https://github.com/askgitdev/askgit')

-- use the default repo, but provide an alternate branch
SELECT * FROM commits('', 'some-ref')
```

## `refs`

| Column    | Type |
|-----------|------|
| name      | TEXT |
| type      | TEXT |
| remote    | TEXT |
| full_name | TEXT |
| hash      | TEXT |
| target    | TEXT |

Params:
  1. `repository` - path to a remote (http(s)) repository


## `stats`

| Column    | Type |
|-----------|------|
| file_path | TEXT |
| additions | INT  |
| deletions | INT  |

Params:
  1. `repository` - path to a remote (http(s)) repository
  2. `rev` - commit hash (or branch/tag name) to use for retrieving stats, defaults to `HEAD`
  3. `to_rev` - commit hash to calculate stats relative to

```sql
-- return stats of HEAD
SELECT * FROM stats

-- return stats of a specific commit
SELECT * FROM stats('', 'COMMIT_HASH')

-- return stats for every commit in the current history
SELECT commits.hash, stats.* FROM commits, stats('', commits.hash)
```

## `files`

| Column     | Type |
|------------|------|
| path       | TEXT |
| executable | BOOL |
| contents   | TEXT |

Params:
  1. `repository` - path to a remote (http(s)) repository
  2. `rev` - commit hash (or branch/tag name) to use for retrieving files in, defaults to `HEAD`

## `blame`

Similar to `git blame`, the `blame` table includes blame information for all files in the current HEAD.

| Column      | Type     |
|-------------|----------|
| line_no     | INT      |
| commit_hash | TEXT     |

Params:
  1. `repository` - path to a remote (http(s)) repository
  2. `rev` - commit hash (or branch/tag name) to use for retrieving blame information from, defaults to `HEAD`
  3. `file_path` - path of file to blame

## `toml_json`

Scalar function that converts `toml` to `json`.

```SQL
SELECT toml_to_json('[some-toml]')

-- +-----------------------------+
-- | TOML_TO_JSON('[SOME-TOML]') |
-- +-----------------------------+
-- | {"some-toml":{}}            |
-- +-----------------------------+
```

## `xml_to_json`

Scalar function that converts `xml` to `json`.

```SQL
SELECT xml_to_json('<some-xml>hello</some-xml>')

-- +-------------------------------------------+
-- | XML_TO_JSON('<SOME-XML>HELLO</SOME-XML>') |
-- +-------------------------------------------+
-- | {"some-xml":"hello"}                      |
-- +-------------------------------------------+
```

## `yaml_to_json` and `yml_to_json`

Scalar function that converts `yaml` to `json`.

```SQL
SELECT yaml_to_json('hello: world')

-- +------------------------------+
-- | YAML_TO_JSON('HELLO: WORLD') |
-- +------------------------------+
-- | {"hello":"world"}            |
-- +------------------------------+
```

## `str_split`

Helper for splitting strings on some separator.

```sql
SELECT str_split('hello,world', ',', 0)

-- +----------------------------------+
-- | STR_SPLIT('HELLO,WORLD', ',', 0) |
-- +----------------------------------+
-- | hello                            |
-- +----------------------------------+
```

```sql
SELECT str_split('hello,world', ',', 1)

-- +----------------------------------+
-- | STR_SPLIT('HELLO,WORLD', ',', 1) |
-- +----------------------------------+
-- | world                            |
-- +----------------------------------+
```
