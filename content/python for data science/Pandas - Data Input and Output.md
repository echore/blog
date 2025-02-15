---
share: true
---

### **Common Formats Supported by Pandas**

|Format Type|Description|Reader Method|Writer Method|
|---|---|---|---|
|**CSV**|Comma-Separated Values|`read_csv`|`to_csv`|
|**JSON**|JavaScript Object Notation|`read_json`|`to_json`|
|**HTML**|Hypertext Markup Language|`read_html`|`to_html`|
|**Excel**|Microsoft Excel (XLS, XLSX)|`read_excel`|`to_excel`|
|**SQL**|SQL Databases|`read_sql`, `read_sql_query`|`to_sql`|
|**Parquet**|Columnar Storage|`read_parquet`|`to_parquet`|
|**Pickle**|Python Object Serialization|`read_pickle`|`to_pickle`|

---

### **File Handling with Examples**

#### **1. CSV Input/Output**

- **Reading a CSV:**
    
    ```python
    df = pd.read_csv('example.csv')  # Reads CSV into DataFrame
    ```
    
- **Writing a CSV:**
    
    ```python
    df.to_csv('new_file.csv', index=False)  # Saves DataFrame to CSV
    ```
    

#### **2. HTML Input/Output**

- **Reading HTML Tables:**
    
    ```python
    tables = pd.read_html('https://en.wikipedia.org/wiki/World_population')
    ```
    
    - This reads all `<table>` elements from a webpage into a list of DataFrames.
- **Writing to HTML:**
    
    ```python
    df.to_html('output.html', index=False)
    ```
    

#### **3. Excel Input/Output**

- **Reading Excel Sheets:**
    
    ```python
    df = pd.read_excel('file.xlsx', sheet_name='Sheet1')
    ```
    
- **Writing to Excel:**
    
    ```python
    df.to_excel('output.xlsx', sheet_name='Sheet1', index=False)
    ```
    

#### **4. SQL Connections**

- **Creating a temporary SQLite database:**
    
    ```python
    from sqlalchemy import create_engine
    engine = create_engine('sqlite:///:memory:')
    df.to_sql('table_name', con=engine)
    ```
    
- **Querying the SQL database:**
    
    ```python
    result = pd.read_sql("SELECT * FROM table_name", con=engine)
    ```
    

---

### **Additional Notes**

- For **Excel**, install necessary libraries: `pip install openpyxl xlrd`.
- For **HTML**: Ensure you have libraries like `lxml`, `html5lib`, and `BeautifulSoup4`.
- For **SQL**: Use appropriate libraries for your database (e.g., `sqlalchemy` for SQLite).

---

### **Practical Tips**

1. Always validate the file paths and libraries needed for reading/writing specific formats.
2. If working with large data, consider columnar formats like **Parquet** for better performance.
3. For troubleshooting permissions or library-specific errors, refer to documentation or community resources.
