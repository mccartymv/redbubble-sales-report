# redbubble-sales-report
Node.js built script to aggregate artist sales reports from multiple stores on redbubble.com and display a breakdown of sales information in the console. Built with javascript promises and asynchronous pattens, this sales report script is designed to process reports and display output very quickly.

example output:<br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/squarebiz-earnings.png?raw=true)

# The Problem
Redbubble.com, a print-on-demand marketplace, offers its artist users sales reports in CSV form. Every row in the document has details of a single sale and each report covers a six-month time period.<br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/sales-report-screenshot.png?raw=true)<br>
For a Redbubble artist with a single shop, the only issue with aggregating multiple sales reports is the potential redundancy, i.e. counting the same sale multiple times. This problem is easy enough to manage given each row's unique `Order #` field. But an artist with multiple storefronts on Redbubble would typically want to see sales breakdowns seperated by store. Redbubble's CSV reports have no header contianing the store name and the default file name only contains a date.

# The Solution
