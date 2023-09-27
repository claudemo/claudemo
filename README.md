<p align="center">
  <img
    src="https://socialify.git.ci/athul/waka-readme/image?description=1&font=Source%20Code%20Pro&forks=1&issues=1&name=1&owner=1&pulls=1&stargazers=1&theme=Auto"
    alt="waka-readme"
    width="640"
    height="320"
  />
</p>

# Dev Metrics in Readme [![Unit Tests](https://github.com/athul/waka-readme/actions/workflows/testing.yml/badge.svg?branch=master)](https://github.com/athul/waka-readme/actions/workflows/testing.yml)

[WakaTime](https://wakatime.com) coding metrics on your profile readme.

<!-- prettier-ignore-start -->
<picture>
  <source srcset="https://github.com/athul/waka-readme/assets/38415384/60a6bcd0-01f8-421a-8730-7e872d216e09"
    media="(prefers-color-scheme: dark)" />
  <img src="https://github.com/athul/waka-readme/assets/38415384/29541cbc-0e39-47c4-93c2-514032b47276"
    alt="new_secrets_actions" />
</picture>
<!-- prettier-ignore-end -->

:speech_balloon: **Forum** | [GitHub discussions][gh_discuss]

## New to WakaTime?

> Nope? Skip to [#Prep work](#prep-work).

WakaTime gives you an idea of the time you spent on coding.
This helps you boost your productivity and competitive edge (aka _flex_ :muscle:).

1. Head over to <https://wakatime.com/> and create an account.
2. After logging in get your WakaTime API Key from <https://wakatime.com/api-key/>.
3. Install [WakaTime plugin][waka_plugins] in your favorite editor / IDE.
4. Paste in your API key to start telemetry.

:information_source: **Info** | You can read [WakaTime help][waka_help] to know more about configurations.
Alternatively, you can fetch data from WakaTime compatible services such as [Wakapi][wakapi] or [Hakatime][hakatime].

## Prep Work

A GitHub repository and a `README.md` file is required. We'll be making use of readme in the [profile repository][profile_readme].

- Save the `README.md` file after copy-pasting the following special comments. Your dev-metics will show up in between.

  ```md
  <!--START_SECTION:waka-->
  <!--END_SECTION:waka-->
  ```

  `<!--START_SECTION: -->` and `<!--END_SECTION: -->` are placeholders and must be retained as is. Whereas "`waka`" can be replaced by any alphanumeric string. See [#Tweaks](#tweaks) section for more.

- Navigate to your repo's `Settings`:
  - Go to `Secrets` (at `https://github.com/USERNAME/USERNAME/settings/secrets/actions/new` by replacing the `USERNAME` with your own username) and add a new secret "_Named_" `WAKATIME_API_KEY` with your API key as it's "_Secret_".

    <!-- prettier-ignore-start -->
    <picture>
      <source srcset="https://github.com/athul/waka-readme/assets/38415384/04dee9dc-65a1-43f9-9df4-7545646b9a72"
        media="(prefers-color-scheme: dark)" />
      <img src="https://github.com/athul/waka-readme/assets/38415384/9110cc3e-66cc-46ed-89d4-36644aa258e1"
        alt="new_secrets_actions" />
    </picture>
    <!-- prettier-ignore-end -->

    > If you're not using [profile repository][profile_readme], add another secret "_Named_" `GH_TOKEN` and in place of "_Secret_" insert your [GitHub token][gh_access_token].

  - Go to `Workflow permissions` under `Actions` (at `https://github.com/USERNAME/USERNAME/settings/actions` by replacing the `USERNAME` with your own username) and set `Read and write permissions`.

    <!-- prettier-ignore-start -->
    <picture>
      <source srcset="https://github.com/athul/waka-readme/assets/38415384/a1b86a0b-4065-4ff1-847b-b52e681bf247"
        media="(prefers-color-scheme: dark)" />
      <img src="https://github.com/athul/waka-readme/assets/38415384/de9cb7d0-fd40-43cf-8fed-7c6f57207788"
        alt="new_secrets_actions" />
    </picture>
    <!-- prettier-ignore-end -->

- Create a new workflow file named `waka-readme.yml` inside `.github/workflows/` folder of your repository.
- Clear all existing contents, add following lines and save the file.

  ```yml
  name: Waka Readme

  on:
    # for manual workflow trigger
    workflow_dispatch:
    schedule:
      # runs at 12 AM UTC (5:30 AM IST)
      - cron: "0 0 * * *"

  jobs:
    update-readme:
      name: WakaReadme DevMetrics
      runs-on: ubuntu-latest
      steps:
        - uses: athul/waka-readme@master
          with:
            WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
  ```

  Refer [#Example](#example) section for a full blown workflow file.

## Tweaks

There are many flags that you can modify as you see fit.

### Meta Tweaks

| Environment flag | Options (`Default`, `Other`, ...)                                                        | Description                                                                   |
| ---------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `API_BASE_URL`   | `https://wakatime.com/api`, `https://wakapi.dev/api`, `https://hakatime.mtx-dev.xyz/api` | Use WakaTime compatible services like [Wakapi][wakapi] & [Hakatime][hakatime] |
| `REPOSITORY`     | `<gh_username>/<gh_username>`, `<gh_username>/<repo_name>`                               | Waka-readme stats will appear on the provided repository                      |

### Content Tweaks

| Environment flag   | Options (`Default`, `Other`, ...)                                       | Description                                                                       |
| ------------------ | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `SHOW_TITLE`       | `false`, `true`                                                         | Add title to waka-readme stats blob                                               |
| `SECTION_NAME`     | `waka`, any alphanumeric string                                         | The generator will look for section name to fill up the readme.                   |
| `BLOCKS`           | `░▒▓█`, `⣀⣄⣤⣦⣶⣷⣿`, `-#`, `=>`, you can be creative                      | Ascii art used to build stats graph                                               |
| `CODE_LANG`        | `txt`, `python` `ruby` `json` , you can use other languages also        | Language syntax based highlighted text                                            |
| `TIME_RANGE`       | `last_7_days`, `last_30_days`, `last_6_months`, `last_year`, `all_time` | String representing a dispensation from which stats are aggregated                |
| `LANG_COUNT`       | `5`, any plausible number                                               | Number of languages to be displayed                                               |
| `SHOW_TIME`        | `true`, `false`                                                         | Displays the amount of time spent for each language                               |
| `SHOW_TOTAL`       | `false`, `true`                                                         | Show total coding time                                                            |
| `SHOW_MASKED_TIME` | `false`, `true`                                                         | Adds total coding time including unclassified languages (overrides: `SHOW_TOTAL`) |
| `STOP_AT_OTHER`    | `false`, `true`                                                         | Stop when language marked as `Other` is retrieved (overrides: `LANG_COUNT`)       |



[//]: #(Links)
[wakapi]: https://wakapi.dev
[hakatime]: https://github.com/mujx/hakatime
[waka_plugins]: https://wakatime.com/plugins
[waka_help]: https://wakatime.com/help/editors
[profile_readme]: https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme
[gh_access_token]: https://docs.github.com/en/actions/configuring-and-managing-workflows/authenticating-with-the-github_token
[gh_discuss]: https://github.com/athul/waka-readme/discussions
