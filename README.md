# CSGO-Tracker

Provides a Price Tracking Spreadsheet, Inventory Scraper, and Price Updater for CSGO items.

## Spreadsheet

```
Provides price tracking and metrics on the user's CSGO items.
```

### Example

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/e0d51a7b-61c5-4df2-ba56-0622cd829f30)

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

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/627b8c87-60a9-4326-88c0-6532b8dfb880)

To utilize Excel's built-in sorting and analysis features wihtout including summary boxes on the right:

1. **Select Relevant Columns:** Highlight the relevant column letters.
   
3. **Access the Sort Ribbon:** Navigate to the "Home" tab in Excel's ribbon.

4. **Initiate Sorting:** Click the ```'Sort & Filter'``` ribbon and select ```'Custom Sort'```, the user can then select which column to use as the key along with the sort direction.


## Inventory Scraper [```inventory.py```]

```
Populates the template file with the user's marketable CSGO inventory items.
```

### File Paths

- **base_path:** By default, the script assumes that ```'base_file.xslx'``` (template) is at the same directory level, if not, change accordingly.
- **file_path_local:** The output directory of the newly created spreadsheet after scraping items, change the output name as desired. 
- **file_path_desktop:** Same file as ```'file_path_local'```.  If the file should also be available on your desktop, you can specify your desktop directory here, or you can simply omit this line if it's not needed.
  
```python
170. base_path = 'base_file.xlsx'
171. file_path_local = 'modified_spreadsheet.xlsx'
172. file_path_desktop = r'C:\Users\<your_user_name>\Desktop\modified_spreadsheet.xlsx'
```

```'base_file.xslx'``` is not overwritten, a new spreadsheet containing the user's item is created at the same directory level as the script and a copy is saved to the desktop (where applicable) via the ```save_excel()``` function.

```python
150. def save_excel():
151.     """Saves the updated Excel file with the original formatting to specified directories"""
152.
153.     wb.save(file_path_local)
154.     wb.save(file_path_desktop)
```

## Price Updater [```csgo.py```]

```
Updates the user's spreadsheet with the current lowest Steam market price listing values for their items.
```

### File Paths

- **file_path_local:** By default, the script assumes that the user's spreadsheet is at the same directory level, if not, change accordingly.
- **file_path_desktop:** = Same file as ```'file_path_local'```.  If the file should also be available on your desktop, you can specify your desktop directory here, or you can simply omit this line if it's not needed.

```python
209.    file_path_local = '<file_name>.xlsx'
210.    file_path_desktop = r'C:\Users\<your_user_name>\Desktop\<file_name>.xlsx'
```

The user's original spreadsheet is overwritten and a copy is saved to the desktop (where applicable) via the ```save_excel()``` function.

```python
199. def save_excel():
200.     """Saves the updated Excel file with the original formatting to specified directories"""
201.
202.     wb.save(file_path_local)
203.     wb.save(file_path_desktop)
```

## How To Run

1. ```pip install requirements.txt```
2. Configure file paths in ```inventory.py``` and ```csgo.py```
3. ```python inventory.py``` Input your Steam inventory URL when prompted (inventory must be public)
4. Fill in item purchase prices in the generated spreasheet
5. ```python csgo.py``` to update item current values

## Additional Requirements 

- Google Chrome (only for ```inventory.py```)
