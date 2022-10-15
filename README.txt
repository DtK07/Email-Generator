Info:
Email ID Generator is a python code which guesses the mail IDs of the prospects when First Name, Last Name and Domain is given as an input.

Libraries Used:
1.Openpyxl

Process:
1.This is coded in a way such that the input is automaticaaly pulled from an excel where prospect name and domain names are given. 
2.In case domain name is not found there is an additional column where prospect's company website is given, code will look for that column and pull out a domain name from company website.
3.If there is more than first namd eand last name for a prospect(Middle name is included), code will execute a string manipulation and detects the first and last name alone and then proceeds further.
4.Once input(First Name, Last Name and Domain Name) is in place now again with the help of string manipulation code will generate six possible guesses.

Output:
As mentioned above this coe will generate six possible guesses and store it in a separate excel in a same workbook-where input is taken from.

