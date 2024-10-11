
# LifeBear Script Breakdown

This script processes a CSV file, removes duplicate and invalid email addresses, and saves cleaned and erroneous entries to separate files. It handles common file I/O errors and utilizes regex for email validation. The output includes cleaned data, duplicate entries, and invalid email entries, all saved into designated folders.

## Prerequisites
<!-- python code block -->
```python
`pip install pandas`
```
- Python 3.x
- pandas library (`pip install pandas`)

## Script Overview

1. **Loading CSV File:**
   - The script reads a CSV file named `JapanLifeBear.csv` with `;` as the separator.
   - If the file is not found or is empty, appropriate error messages are displayed.

2. **Renaming Columns:**
   - The script renames the columns of the dataframe for clarity:
     - `mail_address` → `email`
     - `birthday_on` → `date_of_birth`
     - `login_id` → `login`
     - `created_at` → `created`

3. **Duplicate Removal:**
   - The script identifies duplicate entries based on the columns `email` and `login`, keeping only the first occurrence.
   - Duplicates are saved to a CSV file (`Duplicate_entries.csv`) in a garbage folder.

4. **Email Validation:**
   - The script validates email addresses using regular expressions (regex).
   - Valid emails are retained, while invalid ones are saved in a separate CSV file (`Garbage_data.csv`).

5. **Saving Cleaned Data:**
   - The final cleaned data (valid emails and no duplicates) is saved to a specified folder as `Cleaned_Data.csv`.

## Usage

1. **Run the Script:**
  <!-- python code block -->
```python
# Read the initial CSV file with separator modification and low memory usage
try:
    df = pd.read_csv("JapanLifeBear.csv", sep=';', low_memory=True)
    if df.empty:
        print("Warning: The input CSV file is empty.")
    else:
        print("CSV file loaded successfully.")
except FileNotFoundError:
    print("Error: The file 'JapanLifeBear.csv' was not found.")
    sys.exit(1)
except pd.errors.EmptyDataError:
    print("Error: The file is empty.")
    sys.exit(1)
except Exception as e:
    print(f"An error occurred while reading the file: {e}")
    sys.exit(1)
```
   Ensure the `JapanLifeBear.csv` file exists in the same directory as the script, or provide the correct path.

2. **Input:**
   - CSV file (`JapanLifeBear.csv`) with fields like `email`, `login`, etc.

3. **Output:**
   - Cleaned data file: `Cleaned_Data.csv`
   - Duplicates file: `Duplicate_entries.csv`
   - Invalid email file: `Garbage_data.csv`

## Folder Structure

- The script creates or uses two main directories:
  - **Garbage Folder**: Stores invalid emails and duplicates.
  - **Cleaned Folder**: Stores the final cleaned data file.

```plaintext
C:\Users\PROTEXXA\Desktop\LifeBear\
    ├── LifeBearGarbage\
    │   ├── Duplicate_entries.csv
    │   └── Garbage_data.csv
    └── CleanedLifeBear\
        └── Cleaned_Data.csv
```

## Functions

### `is_valid_email(email)`
- **Description**: Validates an email address using regex.
- **Input**: `email` (string)
- **Output**: `True` if valid, `False` if invalid.

### `save_dataframe_to_csv(df, file_path)`
- **Description**: Saves a DataFrame to a CSV file.
- **Input**: 
  - `df`: DataFrame to be saved.
  - `file_path`: Destination file path.
- **Output**: None (prints a success message or an error).

### `remove_and_save_duplicates(df, subset_columns, garbage_folder)`
- **Description**: Removes duplicates from a DataFrame and saves them to a CSV file.
- **Input**:
  - `df`: Input DataFrame.
  - `subset_columns`: Columns to check for duplicates.
  - `garbage_folder`: Folder to save duplicate entries.
- **Output**: Cleaned DataFrame with duplicates removed.

---

## Frequently Asked Questions (FAQ)

### 1. **What happens if the CSV file is empty or not found?**
- If the file is empty, the script prints a warning and stops. If the file is not found, it shows an error and exits.

### 2. **What kind of emails are considered valid?**
- An email is valid if it follows this regex pattern: `^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$`. This includes standard email formats like `example@domain.com`.

### 3. **Where are duplicates saved?**
- Duplicates are saved in a file named `Duplicate_entries.csv` in the `LifeBearGarbage` folder.

### 4. **What happens to invalid email addresses?**
- Invalid emails are saved in the `Garbage_data.csv` file inside the `LifeBearGarbage` folder.

### 5. **Can I change the file paths for saving the cleaned data?**
- Yes, you can modify the paths by changing the variables `garbage_file_path` and `cleaned_file_path` in the script.

### 6. **What should I do if I encounter a recursion error?**
- The script increases the recursion limit to handle larger datasets. If a recursion error occurs, you can increase the limit by modifying the `sys.setrecursionlimit(10000)` line.
