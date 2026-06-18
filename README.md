# downdetector

A small cron watchdog that checks whether other personal scripts have logged errors and sends a
[Pushover](https://pushover.net/) notification when they have.

## How it works

On each run it looks for known error files in `/tmp` and, if any exist and are non-empty, posts a
message to the Pushover API:

| Error file | Alerts about |
| --- | --- |
| `/tmp/startrektweeter.err` | the Star Trek tweeter job |
| `/tmp/youtubenotifier.err` | the YouTube downloader job |

The monitored jobs are expected to redirect their stderr to these files, so a non-empty file means
something went wrong.

## Setup

1. Fill in your Pushover credentials at the top of `main.py`:
   - `pushover_api_user_key`
   - `pushover_api_app_token` / `pushover_api_youtubedl_token`
2. Adjust the error-file paths to match your own jobs.
3. Schedule it with cron:
   ```cron
   */15 * * * * /usr/bin/python3 /path/to/main.py
   ```

## License

[MIT](LICENSE) © Corbin Johnson
