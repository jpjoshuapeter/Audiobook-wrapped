# Audiobook Wrapped

Audiobook Wrapped is a lightweight single-file web app that turns audiobook listening data from an Excel workbook into a polished, shareable year-in-review dashboard.

Users can drag in an `.xlsx` file, choose the worksheet that contains their data, and instantly generate a personalized summary with total listening time, books finished, top authors, notable books, listening sources, and a reading timeline.

## Features

* Drag-and-drop or file-picker upload for Excel workbooks
* Worksheet selector that defaults to the workbook's active tab
* Automatic parsing of audiobook data from spreadsheet rows
* Summary stats for hours listened, books finished, unique authors, and best listening pace
* Top author ranking with visual progress bars
* Notable book cards for longest, shortest, fastest-paced, and most leisurely listens
* Listening source breakdown
* Monthly timeline grouped by audiobook start date
* Built-in light and dark theme toggle with saved theme preference in local storage
* Friendly error handling for unreadable files, empty sheets, and invalid row formats

## Demo Behavior

Once a valid spreadsheet is loaded, the app builds a “Wrapped” style dashboard that includes:

* Hero section with the listening year and date range
* Stats grid with headline metrics
* Top authors section
* Notable books section
* Listening sources section
* Reading timeline section
* Quick reload button for switching to another file

## Tech Stack

* HTML5
* CSS3
* Vanilla JavaScript
* .xlsx


## Project Structure

This project is intentionally simple and can be hosted almost anywhere as a static page.

```text
.
├── audiobook_wrapped.html
└── Audiobook Tracking.xlsx
```

## How to Run

Because this is a standalone HTML app, there is no build step.

### Open locally

* Download or clone the repository
* Keep `audiobook_wrapped.html` and `Audiobook Tracking.xlsx` together if you want to ship the sample template with the project
* Open `audiobook_wrapped.html` in your browser


## Included Template Workbook

This repository can include the sample workbook `Audiobook Tracking.xlsx` as a ready-to-use template for the app.

### Template structure

* `2026 Data` is the main input sheet and the active tab in the workbook
* `2026 Stats` is a supporting stats sheet with summary calculations and pivot-style outputs
* The app should be pointed at `2026 Data` when generating the Wrapped dashboard

### Columns included in the template

The `2026 Data` sheet already includes the fields the app expects, including:

* `Title`
* `Author`
* `Hours`
* `Number`
* `Sped Up`
* `Mins`
* `Start Date`
* `End Date`
* `Num of Days`
* `Avg Min / Day`
* `Source`

### Notes about using the template

* The workbook already contains formulas for helper fields such as `Number`, `Sped Up`, `Mins`, `Num of Days`, and `Avg Min / Day`
* The app can still parse the file as long as each audiobook row has a title and a usable listening duration
* If you upload this workbook, the sheet selector should default to `2026 Data` because it is the saved active tab
* The `2026 Stats` sheet is useful for workbook analysis, but the Wrapped display is built from the row-level listening data sheet

## Expected Input Data

The app reads one worksheet at a time and looks for audiobook-related columns. Column matching is case-insensitive for the supported field names. The highlighted fields are required for full use of application

### Supported columns

* `Title`
* `Author`
* `Mins`
* `Hours` (used as a fallback when `Mins` is not present)
* `Num of Days` or `Days`
* `Avg Min / Day` or `Avg Min/Day`
* `Source`
* `Start Date` or `Start`
* `End Date` or `End`
* `Number`

### Minimum useful fields

For the app to render a valid entry, each row should have:

* A title
* Listening time that can be parsed into minutes

Rows without a title or a valid listening duration are filtered out.

## How the Parsing Works

* If a `Mins` column is present, the app uses it first
* If `Mins` is missing, the app looks for a column containing “hour” and tries to parse either:
  * A `HH:MM` style string
  * A decimal hour value
* The app converts parsed hours into minutes
* The listening year in the hero section is inferred from the worksheet name when it contains a 4-digit year

## Generated Insights

The dashboard calculates and displays:

* Total minutes and rounded total hours
* Total books completed
* Unique author count
* Highest average minutes per day
* Top authors by total listening time
* Longest and shortest books by listening time
* Fastest and slowest pace among books with valid day counts
* Source distribution by number of books
* Month-by-month reading/listening timeline

## Theme Customization

The UI uses CSS custom properties, so it is easy to retheme.

### Current palette

#### Light mode

* `#f0e3d2`
* `#b6b19e`
* `#c5a491`
* `#a46e42`
* `#757047`

#### Dark mode

* `#152013`
* `#240502`
* `#3d3236`
* `#0A1344`
* `#4e3424`

To adjust the visual style, update the variables inside the `:root` and `[data-theme="dark"]` blocks near the top of the HTML file.

## Customization Ideas

* Add cover art or author photos
* Export the wrapped dashboard as an image or PDF
* Support CSV uploads in addition to Excel
* Add charts for monthly listening volume
* Add genre, rating, or narrator summaries
* Support multiple years in one workbook

## Known Limitations

* Input is designed for `.xlsx` workbooks
* The app depends on a CDN-hosted SheetJS script
* There is no backend or persistent storage
* Date parsing depends on values that JavaScript can interpret reliably
* The layout is optimized for browser viewing rather than print/export

## Why This Repo Is Easy to Share

* No framework setup required
* No package manager required
* No server required
* Easy to fork, customize, and publish


