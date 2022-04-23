# redbubble-sales-report
Node.js built script to aggregate artist sales reports from multiple stores on redbubble.com and display a breakdown of sales information in the console. Built with javascript promises and asynchronous pattens, this sales report script is designed to process reports and display output very quickly.

example output:<br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/squarebiz-earnings.png?raw=true)

# The Problem
Redbubble.com, a print-on-demand marketplace, offers its artist users sales reports in CSV form. Every row in the document has details of a single sale and each report covers a six-month time period.<br><br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/sales-report-screenshot.png?raw=true)<br><br>
For a Redbubble artist with a single shop, the only issue with aggregating multiple sales reports is the potential redundancy, i.e. counting the same sale multiple times. This problem is easy enough to manage given each row's unique `Order #` field. But an artist with multiple storefronts on Redbubble would typically want to see sales breakdowns seperated by store. Redbubble's CSV reports have no header contianing the store name and the default file name only contains a date.

# The Solution
With no storefront name in the CSV or the filename, we have to ask to user of redbubble-sales-report for a **Regular Expression**, one that will match the `Product` field of every single product available in the shop. We need this info entered manually to the `config.js` file as below:<br><br>
```
module.exports = { 
    'shops' : [
        {
            'name' : 'squarebiz',
            'productRegex' : /^100% /
        }
    ],
    'targetDir' : 'redbubble-reports',
    'currencySymbol' : '$',
    'salesReportTopListCount' : 10
};
```
Looking at the `shops` array, we have the name of our store and a RegEx, `/^100% /` which matches any string of text which begins with "100% ". This matches the output in the example at the top of this README.
Not all shops have such a strict naming convention that applies to every single product available of course. Luckily, regular expressions can take conditional rules, a regular expression could be written with the OR (|) operator to account for any product name in a diverse store. More information on conditional regular expressions is available [here](https://regexone.com/lesson/conditionals).

