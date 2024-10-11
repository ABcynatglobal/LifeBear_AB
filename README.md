
# CSV Data Cleaning Script

## Overview

This Python script is designed to clean a CSV file (`JapanLifeBear.csv`) by:
1. Validating email addresses using a regular expression.
2. Dropping rows with missing values in specific columns (`birthday_on` and `gender`).
3. Renaming columns for consistency.
4. Filtering valid email addresses, removing duplicates, and saving the cleaned data to separate CSV files.

## Prerequisites

- **Python 3.x** installed
- **pandas** library installed (`pip install pandas`)
- The input file `JapanLifeBear.csv` should be located in the same directory as the script.

## How It Works

1. **Loading the CSV**:
    - The script reads the CSV file (`JapanLifeBear.csv`) with semicolon (`;`) as the separator.
    - If the file is empty or not found, appropriate error messages are shown, and the script exits.
  
2. **Data Cleaning**:
    - The script drops rows where the `birthday_on` or `gender` columns have missing values.
    - It renames the columns `mail_address` to `email` and `birthday_on` to `date_of_birth`.

3. **Email Validation**:
    - The script checks if the email addresses are valid using a regular expression.
    - It separates valid and invalid email addresses into two DataFrames.
  
4. **Handling Duplicates**:
    - The script identifies and removes duplicate rows based on the `email` and `login_id` columns.
    - Duplicated rows are saved in a separate file.

5. **Saving Output**:
    - Invalid email addresses are saved in a file called `Invalid_emails.csv` inside the `LifeBearGarbage` folder.
    - Duplicate entries are saved in a file called `Duplicate_entries.csv` in the same folder.
    - Cleaned data with valid, unique email addresses is saved to `Clean_Data4.csv` inside the `CleanedLifeBear` folder.

## Folder Structure

- **LifeBearGarbage**: Contains files for invalid emails and duplicates.
- **CleanedLifeBear**: Contains the cleaned CSV file.

## File Paths

- The script uses hardcoded paths to save files:
    - Invalid emails and duplicates: `C:\Users\PROTEXXA\Desktop\LifeBear\LifeBearGarbage`
    - Cleaned data: `C:\Users\PROTEXXA\Desktop\LifeBear\CleanedLifeBear`

## Functions

- `is_valid_email(email)`: Validates email format using a regex.
- `save_dataframe_to_csv(df, file_path)`: Saves a DataFrame to a specified CSV file.

## Error Handling

- The script handles the following errors:
  - **FileNotFoundError**: Raised if the input CSV file is missing.
  - **EmptyDataError**: Raised if the CSV file is empty.
  - **RecursionError**: Raised if too much recursion occurs during saving.

---

## Frequently Asked Questions (FAQ)

### 1. **What happens if the CSV file is empty?**
   - The script will display a warning and exit without performing any further operations.

### 2. **How does the script validate email addresses?**
   - It uses a regular expression (`regex`) that checks for valid email formats, ensuring that the email has the correct structure (e.g., `name@domain.com`).

### 3. **Where are invalid email addresses saved?**
   - Invalid email addresses are saved in `Invalid_emails.csv` located in the `LifeBearGarbage` folder.

### 4. **What does the script do with duplicate entries?**
   - Duplicates (rows with the same `email` and `login_id`) are removed, and the duplicate rows are saved in `Duplicate_entries.csv` in the `LifeBearGarbage` folder.

### 5. **What if I want to use a different CSV file or folder paths?**
   - You can change the file path in the `pd.read_csv()` function for the input file and modify the `garbage_folder` and `cleaned_file_path` variables to point to the desired output directories.

### 6. **What should I do if I encounter a recursion error?**
   - The script increases the recursion limit to 10,000 to handle large datasets, but if the error persists, consider breaking the DataFrame into smaller chunks or optimizing the saving logic.

### 7. **Why does the script use `low_memory=True` when reading the CSV?**
   - This helps to optimize memory usage when working with large CSV files.

---

### Conclusion

This script efficiently cleans the input CSV file by validating email addresses, removing invalid or duplicate entries, and saving the results in designated folders. Modify the file paths as needed, and ensure that the required libraries and files are in place before running the script.
