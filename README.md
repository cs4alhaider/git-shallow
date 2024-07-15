# Git Shallow Clone and Fetching Full History

## Introduction

This document explains the concept of shallow cloning in Git and how to fetch the full commit history after performing a shallow clone. 

## What is a Shallow Clone?

A shallow clone in Git is a repository clone with a limited commit history. By specifying a depth, you can clone the repository with only the latest commits. This is useful for saving bandwidth, speeding up the cloning process, and reducing disk space usage.

### Shallow Clone Command

To perform a shallow clone, use the `--depth` option with the `git clone` command. For example:

```bash
git clone --depth 1 https://github.com/supabase/supabase
```

This command clones the repository but limits the history to the most recent commit.

### Benefits of Shallow Cloning

1. **Saving Bandwidth:** Downloads significantly less data.
2. **Speed:** Faster cloning process.
3. **Disk Space:** Uses less disk space as only the latest state of the files is downloaded.

## Behavior of `git pull` on a Shallow Clone

After cloning a repository with `--depth 1`, running `git pull` will fetch new changes but will not automatically convert the shallow clone into a full clone. The history remains limited to the specified depth.

### Default Behavior of `git pull`

When you run `git pull`:

1. **Fetch New Changes:** Fetches new commits from the remote repository that are descendants of the latest commit.
2. **Maintain Shallow History:** Does not fetch older commits beyond the specified depth.

## Fetching the Full History

If you need the full commit history after performing a shallow clone, you can either deepen the clone gradually or unshallow it to fetch all commits.

### Deepen the Clone

You can gradually increase the depth of the history by specifying a new depth:

```bash
git fetch --depth <new-depth>
```

For example, to deepen the history to the latest 5 commits:

```bash
git fetch --depth 5
```

### Unshallow the Clone

To fetch the entire commit history, use the `--unshallow` option:

```bash
git fetch --unshallow
```

This command converts the shallow clone into a full clone by fetching all commits from the remote repository.

## Example Workflow

Here's an example workflow that starts with a shallow clone and then fetches the full history:

1. **Shallow Clone:**
   ```bash
   git clone --depth 1 https://github.com/supabase/supabase
   cd supabase
   ```

2. **Fetch New Changes (shallow):**
   ```bash
   git pull
   ```
   This command fetches new commits that are direct descendants of the latest commit you have but does not fetch older commits.

3. **Unshallow the Clone (fetch full history):**
   ```bash
   git fetch --unshallow
   ```
   This command fetches all the commits from the remote repository, converting your shallow clone into a full clone.

## Conclusion

Using `--depth 1` is beneficial for quickly setting up a working copy of a repository when full history is not required. If you later decide you need the full history, you can use `git fetch --unshallow` to fetch all the commits and convert your shallow clone into a full clone.
