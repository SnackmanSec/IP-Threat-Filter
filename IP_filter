import csv
import sys

def sortIp(filename):
    with open(filename) as filein:
        # try to guess the format because we don't control that
        dialect = csv.Sniffer().sniff(filein.read(10000))
        filein.seek(0)
        csvin = csv.DictReader(filein, dialect=dialect)

        with open('feed_ip_filtered.csv', 'w') as fileout:
            fields = ['IP', 'category', 'org', 'date_added', 'country']
            csv_writer = csv.DictWriter(fileout, fieldnames=fields, dialect=dialect, escapechar='\\')
            csv_writer.writeheader()

            '''
            -create list to store IPs categorized as scanners
            -loop through csv and if scan is in the column for itype, take the corresponding
            IP from srcip, check if it's in the list. If not, add the IP
            '''
            scan_ip_list = set()
            for line in csvin:
                if "scan" in line['category']:
                    if line['IP'] not in scan_ip_list:
                        scan_ip_list.add(line['IP'])

            '''
            -return the file pointer to the beginning of the file, then skip header row
            -nested loop, compare the IP list to the src IP column in each line of the
            csv and the IP is not in that column, write the line to the output file
            -output file should contain only info for IPs that had not been tagged 
            as a scanner
            '''
            filein.seek(0)
            csvin.__next__()
            for line in csvin:
                if line['IP'] not in scan_ip_list:
                    csv_writer.writerow(line)

if __name__ == "__main__":
    sortIp(sys.argv[1])
