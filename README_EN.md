# auto-green

[![Build Status](https://github.com/LiangLliu/auto-green/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/LiangLliu/auto-green/actions)

🌍 **Language**: [中文](README.md) | **English**

Automatically keep your GitHub commit status green.

> a commit a day keeps your girlfriend away.

## How It Works

This project uses GitHub Actions' scheduled task feature to automatically execute `git commit` at regular intervals,
with the commit message "a commit a day keeps your girlfriend away". The inspiration comes from an anonymous user's
answer to the Zhihu
question "[What's it like to maintain 365 days of green on GitHub?](https://www.zhihu.com/question/34043434/answer/57826281)":

> I once maintained over 200 days of green, but neglected my girlfriend, and it's been green ever since.

## Usage

- Click the **Use this template** button in the upper right corner to copy this GitHub repository. **:warning: Never
  Fork this repo, because fork projects' activities won't make you green :warning:**
- Modify [lines 19 and 20 of the ci.yml file](https://github.com/LiangLliu/auto-green/blob/master/.github/workflows/ci.yml#L19)
to your own GitHub email and username
- (Optional) You can adjust the frequency by
  modifying [line 8 of the ci.yml file](https://github.com/LiangLliu/auto-green/blob/master/.github/workflows/ci.yml#L8)

**Important Reminders**:

- Make sure your repository is **Public**, as private repository commits won't show as green on your GitHub profile
- This project uses `GITHUB_TOKEN` for authentication, which is automatically provided by GitHub Actions and requires no
  additional configuration

## Cron Schedule Syntax

The cron schedule syntax has 5 fields separated by spaces, each representing a time unit.

```plain
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of the month (1 - 31)
│ │ │ ┌───────────── month (1 - 12 or JAN-DEC)
│ │ │ │ ┌───────────── day of the week (0 - 6 or SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

Each time field meaning:

| Symbol | Description     | Example                                               |
|--------|-----------------|-------------------------------------------------------|
| `*`    | Any value       | `* * * * *` every minute of every hour of every day   |
| `,`    | Value separator | `1,3,4,7 * * * *` at 1, 3, 4, 7 minutes of every hour |
| `-`    | Range           | `1-6 * * * *` from 1 to 6 minutes of every hour       |
| `/`    | Step values     | `*/15 * * * *` every 15 minutes                       |

**Notes**:

- Due to GitHub Actions limitations, if set to `* * * * *`, the actual execution frequency is once every 5 minutes
- Default setting is daily execution at UTC 0:00 (`0 0 * * *`)
- GitHub Actions scheduled tasks may have delays, actual execution time may vary by a few minutes

## Important Considerations

- **Environmental Reminder**: While this project is fun, please use it in moderation. Excessive meaningless commits may
  be considered spam
- **Learning Oriented**: It's recommended to use this project as a starting point for learning GitHub Actions, rather
  than the sole way to maintain long-term green status
- **Real Contributions**: The best green squares come from real code contributions and meaningful projects

## How It Works

This project achieves automatic commits through the following steps:

1. **Scheduled Trigger**: GitHub Actions executes based on cron expressions
2. **Environment Setup**: Checks out code in Ubuntu environment
3. **Git Configuration**: Sets up committer information
4. **Authentication**: Uses GitHub-provided `GITHUB_TOKEN` for authentication
5. **Code Sync**: Pulls latest code to avoid conflicts
6. **Empty Commit**: Executes `git commit --allow-empty` to create empty commits
7. **Push Changes**: Pushes commits to remote repository

## FAQ

**Q: Why use "Use this template" instead of Fork?**
A: GitHub only shows contributions from repositories you own or are a collaborator on. Forked repositories don't count
towards your contribution graph unless you're making commits to the original project.

**Q: Will this affect my GitHub statistics?**
A: Yes, it will show green squares on your contribution graph. However, it won't affect your actual code contribution
statistics in repository insights.

**Q: Is this against GitHub's Terms of Service?**
A: This project doesn't violate GitHub's ToS, but please use it responsibly and don't abuse it.

## License

[auto-green](https://github.com/LiangLliu/auto-green) is released under the MIT License. See the
bundled [LICENSE](./LICENSE) file for details.
