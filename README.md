# Email--Generator

The Email ID Generator is a Python code that generates potential email IDs for prospects based on their first name, last name, and domain name. The libraries utilized in this code include Openpyxl.

The process involves the following steps:

The input data is automatically pulled from an Excel sheet containing prospect names and domain names.
In the event that the domain name is not found, the code will reference an additional column in the Excel sheet that contains the prospect's company website and extract the domain name from it.
If the prospect has a middle name in addition to their first and last name, the code will use string manipulation to identify just the first and last name and proceed with the process.
With the first name, last name, and domain name in place, the code will then use string manipulation to generate six potential email ID guesses.
The output of this code is the generation of six potential email ID guesses, which are stored in a separate sheet within the same workbook as the input data.
