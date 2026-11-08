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
3. After the refresh, check page 1: Parcels and Share complete should match the README. Pick **yes** on the Liquefaction zone slicer: the share complete should match the README's liquefaction column.

## The model

- **Parcels**: one row per parcel (`data/tables/parcels.csv`) with its tier, status, completion date and ground. Measures: `Parcels`, `Complete`, `Share complete`, `Non-compliant`, `In a liquefaction zone`.
- **Years**: the share done by year for all parcels, in and out of liquefaction zones (`share_done_by_year.csv`), with `Share done`.

## The map setting Power BI asks for by hand

- **Shape Map** (page 1). Select the map. In **Format visual, Visual, Map settings**, set the map type to **Custom map**, choose **Add map type**, and pick `..\\data\\geometry\\soft_story_parcels.topojson`. The keys are the parcels' `blklot`. If the Shape Map isn't in the Visualizations pane, turn it on in **Options, Preview features, Shape map visual**. If it comes up empty, drag `Parcels[blklot]` to Location and `Parcels[status]` to Legend.

Then save with **File, Save**.

## Save a .pbix too

After the refresh and the map settings, use **File, Save as** with the type **Power BI file (\*.pbix)** to save `powerbi\SFSoftStory.pbix`. It includes the data, so it opens without a refresh.

## Publish (only if you choose to)

Use **Home, Publish**. In the Power BI service, set the semantic model's **Data source credentials** for the GitHub address to **Anonymous**. Scheduled refresh then works with no gateway. **Publish to web** makes a public link, so only use it if you mean the report to be public.

## Shot list for the website and the video

| # | Shot | How | Length |
|---|---|---|---|
| 1 | The program today | No slicer | still |
| 2 | In liquefaction zones | Liquefaction zone: yes | still |
| 3 | Year by year | The line chart | still |
