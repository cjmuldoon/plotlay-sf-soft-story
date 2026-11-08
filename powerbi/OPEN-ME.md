# Opening the Power BI report

`SFSoftStory.pbip` is a Power BI Project: the report (`SFSoftStory.Report`, PBIR format) and the semantic model (`SFSoftStory.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). Projects and the PBIR report format are standard in current versions. If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `SFSoftStory.pbip`, or in Desktop use **File, Open report, Browse reports** with the file type set to *Power BI project files (\*.pbip)*.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-sf-soft-story/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash** (for example `\\Mac\Home\plotlay-sf-soft-story\data\`). Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes. (After Apply external changes one export drew the page at about 57% inside a much larger canvas; a full close and reopen put it right.)

## Check the numbers after Refresh

After **Refresh**, on **The program today** with nothing picked in the Liquefaction zone slicer (as the report opens):

| Card | Should read |
|---|---|
| Parcels on the list | 4,901 |
| Share listed complete | 95.1% |
| Listed non-compliant | 227 |
| In a liquefaction zone | 698 |

Pick **yes** in the slicer (one value at a time) and the cards read 698, 94.1%, 37 and 698, the README's liquefaction column.

On **Year by year** the three lines end in 2026 at 86.1% (all parcels), 85.5% (in a liquefaction zone) and 86.2% (outside).

## The model

- **Parcels**: one row per parcel (`data/tables/parcels.csv`) with its tier, status, completion date and ground. Measures: `Parcels`, `Complete`, `Share complete`, `Non-compliant`, `In a liquefaction zone`.
- **Years**: the share done by year for all parcels, in and out of liquefaction zones (`share_done_by_year.csv`), with `Share done` (always one year: the point of the line, or 2026 when no year is in the filter) and `Finished that year`.

## The map

- **Shape Map** (page 1). The custom map, `data/geometry/soft_story_parcels.topojson`, is saved inside the report (`SFSoftStory.Report/StaticResources/RegisteredResources/soft_story_parcels.topojson`, a copy that keeps only the parcel's `blklot`), so the 4,899 parcels draw on open, coloured by status. The Shape Map has no base map of its own, so the file also carries the context: census tract boundaries (US Census TIGERweb, public domain) in a pale ground tone, with the bay, the ocean and Lake Merced showing as the map's pale blue background. Each parcel is only a few pixels across at city scale; hover a parcel for its address and status. Loading the plain file from `data/` by hand (below) gives the parcels without that context. If the map shows the United States instead (an older Desktop can ignore a saved map): select it, then **Format visual** (the paintbrush), **Visual**, **Map settings**, **Map type: Custom map**, **Add map type** (or **Browse**), and choose `..\data\geometry\soft_story_parcels.topojson`. Under **View map keys** the block and lot numbers (0024024...) should be matched. If the Shape Map is not in the Visualizations pane at all, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop. If it comes up empty, drag `Parcels[blklot]` to Location and `Parcels[status]` to Legend.

## Save a .pbix too

After the refresh, use **File, Save as** with the type **Power BI file (\*.pbix)** to save `powerbi\SFSoftStory.pbix`. It includes the data, so it opens without a refresh.

## Publish (only if you choose to)

Use **Home, Publish**. In the Power BI service, set the semantic model's **Data source credentials** for the GitHub address to **Anonymous**. Scheduled refresh then works with no gateway. **Publish to web** makes a public link, so only use it if you mean the report to be public.

## Shot list for the website and the video

| # | Shot | How | Length |
|---|---|---|---|
| 1 | The program today | No slicer | still |
| 2 | In liquefaction zones | Liquefaction zone: yes | still |
| 3 | Year by year | The line chart | still |
