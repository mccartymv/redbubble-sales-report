# Redbubble Sales Report

A Node.js script to aggregate artist sales report CSVs from multiple stores on redbubble.com and display a breakdown of sales by store in the console. Built with JavaScript promises and asynchronous patterns, this sales report script is engineered to process reports and display output very quickly.

The purpose of this script is to help Redbubble artists with multiple storefronts aggregate their sales data and view a breakdown of sales separated by store.

example output:<br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/squarebiz-earnings.png?raw=true)

# The Problem
Redbubble.com, a print-on-demand marketplace, offers its artist users sales reports in CSV form. Every row in the document has details of a single sale and each report covers up to a six-month time period.<br><br>
![alt text](https://github.com/mccartymv/redbubble-sales-report/blob/main/sales-report-screenshot.png?raw=true)<br><br>
For a Redbubble artist with a single shop, the only issue with aggregating multiple sales reports is the potential redundancy, i.e. counting the same sale multiple times. This risk is easy enough to avoid given each row's unique `Order #` field. 

However, an artist with multiple storefronts on Redbubble would typically want to see sales breakdowns seperated by store. Redbubble's CSV reports have no header containing the store name and the default file name only contains a date.

# The Solution
With no storefront name in the CSV or the filename, we have to ask the user of redbubble-sales-report for a **Regular Expression**, one that will match the `Work` field of every product that could potentially be sold from the shop. The script will then check the `Work` field of the first row from every CSV file in the target directory.

We need this info entered manually to the `config.js` file as below:<br>
```
module.exports = { 
    'shops' : [
        {
            'name' : 'squarebiz',
            'productRegex' : /^100% /
        },
        {
            'name' : 'itmustbemagic',
            'productRegex' : /^Life's Better /
        }
    ],
    'targetDir' : 'redbubble-reports',
    'currencySymbol' : '$',
    'salesReportTopListCount' : 10
};
```
Looking at the first item in the `shops` array, we have the name of one of our stores, `squarebiz`, and a Regular Expression, `/^100% /` which matches any string of text which begins with "100% ". This example corresponds to the output in the example at the top of this README.

Not every shop would have such a strict naming convention that applies to every single product available of course. Luckily, regular expressions can take conditional rules, so a (large) regular expression could be written with the OR (|) operator that would match any artwork name in a store with many diverse product names. More information on conditional regular expressions is available here: [https://regexone.com/lesson/conditionals](https://regexone.com/lesson/conditionals).

