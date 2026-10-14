Introduction:
Data cleaning is an important part of the data analysis process because the quality of a dataset can affect the accuracy and reliability of the insights obtained from it. Real-world datasets may contain duplicate records, inconsistent text, missing values, incorrectly formatted phone numbers, and information stored in a way that makes analysis more difficult.
In this project, I worked with a customer call list and used Python, particularly the Pandas library, to explore and clean the dataset. My aim was to improve the consistency and organisation of the information so that it would be easier to work with in subsequent stages of data analysis.
1. Loading the Dataset:
The first thing I did was load the dataset into Python so I could begin working with the customer information. I imported the Pandas library and used its Excel-reading functionality to load the file into a DataFrame named df.
Pandas provides functions that make it easier to read, manipulate, and analyse structured data. I used pd as a shorter way to reference the library throughout the notebook, while df served as the variable holding the customer call list.
After loading the file, I displayed the DataFrame in the notebook to inspect the information available, including customer IDs, first names, last names, phone numbers, and other customer-related fields.
Examining the dataset at this stage helped me understand the information I was working with before making any changes.
2. Checking for Duplicate Records:
After loading the dataset, I moved on to checking for duplicate records. Duplicate entries can affect the accuracy of customer records and may lead to the same person being counted more than once during analysis.
I used Pandas' drop_duplicates() method to identify and remove duplicate rows. I first examined the result of the operation and then assigned the deduplicated DataFrame back to df so that subsequent operations would use the updated data.
Removing duplicates was an important step towards improving the quality of the customer list and reducing unnecessary repetition in the data.
3. Removing an Unnecessary Column
The next thing I did was remove a column that was not useful for my intended analysis. Keeping unnecessary columns can make a dataset more difficult to navigate, so I removed the column named Not_Useful_Column.
I used Pandas' drop() method to specify the column I wanted to remove. After examining the result, I assigned the modified DataFrame back to df to ensure that the column was removed from the version of the dataset used in subsequent operations.
This step helped simplify the dataset by removing information I did not need for the subsequent cleaning operations.
4. Cleaning Inconsistencies in Last Names:
After removing the unnecessary column, I focused on the Last_Name field. While inspecting the data, I noticed that some last names contained unwanted characters at their beginnings or ends. For example, a name appeared as /White rather than White.
To address this, I used the Pandas string method str.strip() to remove unwanted characters from both ends of the names. The characters I targeted included numbers such as 1, 2, and 3, as well as periods, underscores, and forward slashes.
I assigned the cleaned values back to the Last_Name column so that the changes would be reflected in the dataset.
This helped make the names more consistent and presentable. During this step, I also explored the difference between strip(), lstrip(), and rstrip(). The strip() method removes specified characters from both ends of a string, lstrip() works on the left side, and rstrip() works on the right side.
Understanding these methods helped me see how Python can be used to handle unwanted characters in text data.
5. Working on the Phone Number Column:
I then moved on to the Phone_Number column, where the numbers were not consistently formatted. Some contained hyphens, others used forward slashes or vertical bars, and some records had missing phone numbers.
My first attempt was to use a regular expression with Pandas' str.replace() method to remove characters that were not letters or numbers. My intention was to eliminate separators such as hyphens, slashes, and vertical bars so that the phone numbers would be easier to standardise.
However, I did not assign the result of this first operation back to the Phone_Number column. Therefore, the operation displayed the cleaned values but did not update the original column. This is something I would correct in a revised version of the notebook.
Converting phone numbers to strings
Next, I converted the values in the phone number column to strings. I did this because phone numbers are identifiers rather than quantities intended for mathematical calculations. Treating them as strings allows me to work with their individual characters and apply consistent formatting.
I used the apply() method to perform the conversion on each value in the column. This helped prepare the phone numbers for the formatting operation that followed.
One consideration is that a missing value represented by NaN becomes the text "nan" when converted this way. This means missing phone numbers need to be handled carefully before formatting.
Formatting the phone numbers
After converting the values to strings, I attempted to format each phone number by dividing it into sections and joining those sections with hyphens.
My intention was to create a consistent pattern in which the first three characters formed the first section, the next three formed the second section, and the following four formed the third section.
However, because the earlier operation intended to remove existing separators did not update the column, some of the original hyphens and slashes remained in the values before additional hyphens were added. As a result, some phone numbers became incorrectly formatted.
I repeated the string conversion and formatting operations later in the notebook, but these repetitions did not resolve the underlying problem.
Handling missing phone numbers
I then attempted to remove text generated from missing phone numbers by replacing specific patterns, including "nan----" and "Na----", with empty strings.
The purpose of these operations was to prevent missing phone numbers from appearing as literal text in the cleaned dataset.
However, these replacements only work when the values match the specified patterns exactly. They do not reliably address all missing values or the incorrectly formatted numbers produced earlier.
Reflecting on this section, I learned that the order of data-cleaning operations matters. Removing unwanted separators before applying a formatting pattern is important because formatting inconsistent values can create further problems instead of solving them.
6. Splitting the Address Column:
After working on the phone numbers, I moved to the Address column. The addresses contained different pieces of information, including street addresses, states, and ZIP codes. These details were stored together in a single column, which could make it more difficult to analyse them separately.
I used Pandas' str.split() method to separate the address information using commas as delimiters. I limited the operation to a maximum of two splits and used the expanded output so that the separated values would appear in individual columns.
After examining the result, I assigned the split values to three new columns named Address_Streetname, State, and Zipcode.
This step was intended to make the address information easier to access and analyse. For example, separating states from street addresses could make it easier to group customers by location.
However, the split depends on the address information being separated by commas. Where an address does not contain all the expected components, the resulting fields may be missing. This means the new columns would need to be checked to ensure that each component was assigned correctly.
7. Standardising the Paying Customer Column:
The next step involved standardising the values in the Paying Customer column. I replaced the full words Yes and No with the shorter values Y and N.
I used Pandas' str.replace() method to make these substitutions within the column and assigned the results back to the original field.
The purpose was to create a more consistent and compact representation of customer payment status. Using shorter labels can make a dataset easier to scan and can simplify some reporting tasks.
This operation only changes the specified text patterns, so any other inconsistent values would still need to be examined separately.
8. Replacing Inconsistent Missing-Value Labels:
After standardising the customer payment information, I used Pandas' replace() method to address entries recorded as N/a. I replaced these occurrences with a space.
This was intended to make the representation of these entries more consistent across the dataset.
An important distinction is that a space is not the same as a genuinely missing value. A cell containing a space is still a string containing a character. Therefore, in a more complete cleaning process, I would consider whether these entries should instead be converted to proper missing values, depending on the requirements of the analysis.
9. Standardising the Do Not Contact Column:
I then applied a similar cleaning approach to the Do_Not_Contact column.
I replaced Yes with Y and No with N to make the values more consistent with the format I used in the Paying Customer column.
This step helped standardise the way contact preferences were represented in the dataset. Because the column concerns whether a customer should be contacted, its values should also be checked carefully before the data is used for any customer outreach.
10. Handling Remaining Missing Values:
Finally, I used Pandas' fillna() method to replace missing values with a space.
My intention was to prevent missing entries from appearing as NaN in the resulting table. However, I did not assign the result back to df or use an in-place operation.
Consequently, the operation displays a version of the DataFrame with missing values replaced, but the underlying DataFrame remains unchanged by this final statement.
This was an important learning point because a cleaning operation can produce the expected output in a notebook cell without necessarily changing the dataset that will be used in subsequent steps.

Conclusion:
Through this project, I practised using Python and Pandas to clean a customer call list and prepare it for further analysis. I worked on removing duplicate records, dropping an unnecessary column, correcting unwanted characters in names, handling phone number inconsistencies, splitting address information into separate fields, and standardising customer-related values.
One of the key lessons I took from this exercise was that data cleaning involves more than applying individual functions. It also requires understanding how each operation affects the dataset, checking the results, and ensuring that the changes are applied correctly. For example, I learned the importance of assigning the output of a cleaning operation back to the DataFrame when I want the changes to persist.
This project strengthened my practical understanding of Pandas and showed me how Python can be used to prepare real-world data for analysis. It also helped me identify areas where I can improve my approach, particularly in handling missing values and ensuring that phone numbers are cleaned before formatting.
