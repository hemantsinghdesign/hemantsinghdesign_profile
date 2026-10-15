# Animated profile maintenance

This repository displays on [Hemant Singh's GitHub profile](https://github.com/hemantsinghdesign).

## First publication

Create a **public** GitHub repository named `hemantsinghdesign`, and grant your connected
GitHub app access to it. The repository name must match your account for the README
to appear on your profile. Upload these files to its default `main` branch, including
the `.github/workflows` directory, or push this local repository using Git.

The initial push starts the update workflow. Confirm a successful run in the Actions
tab after publishing. The SVG files are already generated, so the profile images work
as soon as the files are published, even before the first scheduled refresh.

## Daily refresh

The contribution calendar and stats refresh daily at approximately **06:17 UTC**.
You can also run **Actions → Update profile art → Run workflow**.
Only public contribution data is fetched. No personal access token or repository secret is required;
the workflow uses GitHub's built-in `GITHUB_TOKEN` to commit generated assets.
Scheduled Actions may be disabled by GitHub after 60 days without repository activity.

## Regenerate locally

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip install -r scripts/requirements.txt
python scripts/fetch_contributions.py
python scripts/render_heatmap_svg.py
python scripts/render_stats_svg.py
```

To change the portrait, replace `source-photo.png` with your own square photo, then:

```sh
python -m pip install -r scripts/requirements-portrait.txt
python scripts/prep_photo.py source-photo.png
python scripts/make_ascii_svg.py
```

The first portrait run downloads the lightweight U2NetP background-removal model. Portrait dependencies are
only needed locally; daily automation installs the smaller `requirements.txt` set.
Edit your biography in `README.md`. Regenerate and commit the SVG files after changes.

## Source

Adapted from [Avi Vashishta's animated profile guide](https://www.avivashishta.com/blog/build-animated-github-profile-readme)
and [profile repository](https://github.com/AVIVASHISHTA29/AVIVASHISHTA29),
source revision `28a51b99a2f7f3011b1c8409162ff7a633176226`.
The current upstream source uses a live stats card beside the portrait in place of
the article's older info card. This installation follows that layout with Hemant's
public biography beneath it and uses the direct GitHub contribution fetcher.
