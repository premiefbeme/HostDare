
# Enhanced eBay Product Scraper with Pagination and VBA Optimization

Extracting product data from eBay can be a tedious process if done manually. This article outlines a VBA-based solution to scrape eBay product data, troubleshoot issues, and improve functionality such as handling multiple pages and running dynamic search queries.

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Current VBA Code for eBay Scraping

The provided VBA script is designed to extract product details such as the title, price, and links from eBay listings. However, it currently only works on `ebay.com` and does not handle multiple pages or dynamic search queries effectively.

### Code Overview

```vba
Public IE As New SHDocVw.InternetExplorer
Sub GetData()

    Dim HTMLdoc As MSHTml.HTMLDocument
    Dim othwb As Variant
    Dim objShellWindows As New SHDocVw.ShellWindows

    Set IE = CreateObject("internetexplorer.application")

        With IE
            .Visible = True
            .Navigate "https://www.ebay.com/sch/i.html?_nkw=ralph+lauren"
            While .Busy Or .readyState <> 4: DoEvents: Wend

            Set HTMLdoc = IE.document
            ProcessHTMLPage HTMLdoc

            .Quit
        End With
End Sub

Sub ProcessHTMLPage(HTMLPage As MSHTml.HTMLDocument)

    Dim HTMLItem As MSHTml.IHTMLElement
    Dim HTMLItems As MSHTml.IHTMLElementCollection
    Dim rownum As Long

    rownum = 1

    ' Extract Titles
    Set HTMLItems = HTMLPage.getElementsByClassName("s-item__title")
    For Each HTMLItem In HTMLItems
        Cells(rownum, 1).Value = HTMLItem.innerText
        rownum = rownum + 1
    Next HTMLItem

    rownum = 1

    ' Extract Prices
    Set HTMLItems = HTMLPage.getElementsByClassName("s-item__price")
    For Each HTMLItem In HTMLItems
        Cells(rownum, 2).Value = HTMLItem.innerText
        rownum = rownum + 1
    Next HTMLItem

    rownum = 1

    ' Extract Links
    Set HTMLItems = HTMLPage.getElementsByClassName("s-item__link")
    For Each HTMLItem In HTMLItems
        Cells(rownum, 3).Value = HTMLItem.href
        rownum = rownum + 1
    Next HTMLItem

    ' Convert Links to Hyperlinks
    Range("C1:C25000").Select
    For Each xCell In Selection
        ActiveSheet.Hyperlinks.Add Anchor:=xCell, Address:=xCell.Formula
    Next xCell
End Sub
```

---

## Enhancements for Better Functionality

### 1. **Support for Multiple Pages**

Add logic to iterate through a set number of pages. Here's the updated snippet for pagination:

```vba
Dim pageNumber As Long
pageNumber = 1

Do
    ' Process the current page
    Set HTMLdoc = IE.document
    ProcessHTMLPage HTMLdoc

    ' Check if the next page exists and click
    On Error Resume Next
    Set nextPageButton = HTMLdoc.querySelector(".pagination__next")
    If nextPageButton Is Nothing Then Exit Do

    nextPageButton.Click
    Do While IE.Busy Or IE.readyState <> 4: DoEvents: Loop

    pageNumber = pageNumber + 1
    If pageNumber > 10 Then Exit Do ' Stop after 10 pages
Loop
```

### 2. **Dynamic Search Query from Excel Cell**

Modify the script to take the search query from a cell (e.g., `Sheet1` cell `A1`) and output data starting from `A2`.

```vba
Dim searchQuery As String
searchQuery = Worksheets("Sheet1").Range("A1").Value
url = "https://www.ebay.com/sch/i.html?_nkw=" & Replace(searchQuery, " ", "+")

With IE
    .Navigate url
    Do While .Busy Or .readyState <> 4: DoEvents: Loop
End With
```

---

## Addressing Specific Issues

### **Issue 1: Compatibility with `ebay.co.uk`**
The current script works on `ebay.com` but not on `ebay.co.uk`. Ensure the `.Navigate` URL includes the correct domain.

```vba
.Navigate "https://www.ebay.co.uk/sch/i.html?_nkw=" & Replace(searchQuery, " ", "+")
```

### **Issue 2: Limited to One Page**
The pagination logic shared earlier resolves this. Ensure that the pagination element's class name (`.pagination__next`) matches eBay's current structure.

### **Issue 3: Input Query After eBay Opens**
To input the query dynamically after opening eBay, modify the code to interact with the search bar element:

```vba
Dim searchInput As MSHTml.IHTMLElement
Set searchInput = HTMLdoc.querySelector("#gh-ac")
searchInput.Value = searchQuery

Dim searchButton As MSHTml.IHTMLElement
Set searchButton = HTMLdoc.querySelector("#gh-btn")
searchButton.Click
Do While IE.Busy Or IE.readyState <> 4: DoEvents: Loop
```

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Alternative Approach for Large-Scale Scraping

For large-scale or more complex eBay scraping, consider using Python with Selenium or ScraperAPI. Here's an example using ScraperAPI:

### Python Example for eBay Scraping

```python
import requests
from parsel import Selector

API_KEY = "SCRAPE9837861"
BASE_URL = "https://www.ebay.co.uk/sch/i.html"

def scrape_ebay(search_query, pages=5):
    for page in range(1, pages + 1):
        params = {
            "_nkw": search_query.replace(" ", "+"),
            "_pgn": page
        }
        response = requests.get(BASE_URL, params=params, headers={"api_key": API_KEY})
        selector = Selector(response.text)

        titles = selector.css(".s-item__title::text").getall()
        prices = selector.css(".s-item__price::text").getall()
        links = selector.css(".s-item__link::attr(href)").getall()

        for title, price, link in zip(titles, prices, links):
            print(f"Title: {title}, Price: {price}, Link: {link}")

# Example usage
scrape_ebay("laptop", pages=3)
```

---

## Conclusion

By enhancing the VBA code for pagination and dynamic input or leveraging tools like ScraperAPI, you can efficiently scrape eBay data for your needs. With these updates, you can extract data across multiple pages and handle various eBay domains seamlessly.

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)
