# IP-Threat-Filter
Filter out IP's based on categorization

Genereal Description:
- This script should look through a CSV with categorization for IP addresses, detect if an IP is categorized
as scanning, add it to a list of unique IPs, and then search the IP feed CSV for any other
instances of those IPs. It will write out to a new file only lines that DO NOT include IPs
from the unique IP(scan_ip_list) list detected in relation to scanning even if they were
categorized as something different.

Usage:
- To run the script, it requires one argument, the CSV file name that you would like to process.
- Example: 
      C:\Users\username\PycharmProjects\IP-Threat-Filter>python ip_filter.py ip_document_to_filter.csv

Input Requirements:
- A CSV file where column 1 includes IP addresses, titled "IP". Column 2 includes the categorization of that IP (i.e. scanning, malicious, C&C, botnet), titled "category". 
- The CSV can contain additional columns, but the script does not look at any others at this time. Feel free to modify to fit your need.

Processing:
- Create a list(actually a set in python) to store IPs categorized as scanners.
- The processing will check to see if the IP is already in the list, and if not, the IP will be added. This ensures that only unique IPs are added to the list.
- The file pointer then returns to the beginning of the CSV and skips the header row.
- Next, the IP list is compared to the "IP" column in each row of the CSV and if the IP is not in that column, write the row to the output file.
            
Output:
- CSV output file should contain only info for IPs that had not been categorized as a scanner.
