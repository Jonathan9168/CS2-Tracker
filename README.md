# CSGO-Tracker

Provides a Price Tracking Spreadsheet, Inventory Scraper, and Price Updater for CSGO items.

## Spreadsheet

```
Provides price tracking and metrics on the user's CSGO items.
```

### Example

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/397e875d-df81-4e75-9a44-4b64d01e1535)

### Columns and Metrics

Below is an explanation of each column and metric used in the spreadsheet:

- **Purchase Date:** Date the item was bought.
- **Item:** Item name as seen on the Steam market.
- **Condition:** Wear of the item where applicable.
- **Purchase Platform:** Platform from which the item was bought (e.g., Steam or third-party marketplaces).
- **Purchase Price:** Price at which the item was bought.
- **Current Value [Steam]:** Current lowest Steam market listing price for the item.
- **Current Value % Change:** Percentage change from the last value in the corresponding 'Current Value [Steam]' column.
- **Price Difference:** Difference between the current value and the purchase price.
- **Sold Price:** Price for which the item was sold, where applicable.
- **Current Value Updated:** Denotes whether an item's value was updated. 'y' for successful updates and 'n' for unsuccessful ones (e.g., due to incorrect spelling or error 429).
- **Expected Profit (Steam):** The expected profit that can be realized if unsold items are listed at the Steam market value price, accounting for the ~15% Steam fee.
- **Actual Profit:** The actual profit made from confirmed sales.

### Sorting

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/24e16cd7-d89e-4b6a-945b-7c896392f4e0)

To utilize Excel's built-in sorting and analysis features wihtout including summary boxes on the right:

1. **Select Relevant Columns:** Highlight the relevant column letters.
   
3. **Access the Sort Ribbon:** Navigate to the "Home" tab in Excel's ribbon.

4. **Initiate Sorting:** Click the ```'Sort & Filter'``` ribbon and select ```'Custom Sort'```, the user can then select which column to use as the key along with the sort direction.

## File Paths [```config.py```]

- **base_path:** By default, the ```inventory.py``` script assumes that ```'base_file.xslx'``` (template to be populated) is at the same directory level, if not, change accordingly.
- **file_path_local:** The output directory of the newly created spreadsheet after scraping items with ```inventory.py```, change the output name as desired. This is also used as the input file in ```csgo.py``` when updating values for a given spreadsheet.
- **file_path_desktop:** Same file as ```'file_path_local'```.  If the file should also be available on your desktop, you can specify your desktop directory here, or you can leave as ```None``` if not needed.
- **chrome_driver_executable_path:** Full path to the Chromdriver executable downloaded (ideally in the same directory as the scripts). If there is no chromedriver version mismatch, leave as ```None```.
  
```python
1. base_path = 'base_file.xlsx'  # template file
2. file_path_local = '<file_name>.xlsx'  # output file in same directory as scripts
3. file_path_desktop = None  # file output to desktop (if you want to) e.g., r'<path_to_desktop>/<file_name>.xlsx'
4. chrome_driver_executable_path = None  # full path to chromedriver executable if driver not found

```

The ```save_excel()``` functions in ```inventory.py``` and ```csgo.py``` save the output files to the directories specified in ```config.py```.

```python
def save_excel():
    """Saves the updated Excel file with the original formatting to specified directories"""

    wb.save(file_path_local)

    if file_path_desktop is not None:
        wb.save(file_path_desktop)
```

## Inventory Scraper [```inventory.py```]


Populates the template file with the user's marketable CSGO inventory items.  

![25e7c5b4109a1527aba62bc7097cdf20](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/b9361c20-5ed6-488b-bf08-52c794c1c722)


### Chromedriver (attempts to fetch automatically)  

If by chance your Chrome version is very new, there may be a driver vesrison mismatch error,
Chromedrivers can be downloaded from:   
https://googlechromelabs.github.io/chrome-for-testing/#stable and https://chromedriver.chromium.org/downloads

Simply drag and drop the Chromedriver executable into the same folder as the script.

View your Chrome version here: chrome://settings/help

## Price Updater [```csgo.py```]


Updates the user's spreadsheet with the current lowest Steam market price listing values (option A) or CSGO Trader daily/weekly averages (options B and C).  

Option A is prone to rate limits so item requests are throttled by default to one every three seconds.


![bc6eca941edfa96e8cc96dbc161b2e53](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/9658140d-790c-4725-8dae-43beda4cbd86)


## How To Run

1. ```pip install -r requirements.txt```
2. Configure file paths in ```config.py```
3. ```python inventory.py``` Input your Steam inventory URL when prompted (inventory must be public)
4. Fill in item purchase prices in the generated spreasheet
5. ```python csgo.py``` to update item current values

## Additional Requirements 

- Google Chrome (only for ```inventory.py```)
