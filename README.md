<!-- align a paragraph to the center -->
<p align="center">
<a href="https://github.com/dgunning/edgartools">
    <img src="https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/edgartools-logo.png" alt="edgar-tools-logo" height="80">
</a>
</p>
<p align="center">The world's easiest, most powerful edgar library</p>

[![PyPI - Version](https://img.shields.io/pypi/v/edgartools.svg)](https://pypi.org/project/edgartools)
![GitHub last commit](https://img.shields.io/github/last-commit/dgunning/edgartools)
![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/dgunning/edgartools/python-hatch-workflow.yml)
[![CodeFactor](https://www.codefactor.io/repository/github/dgunning/edgartools/badge)](https://www.codefactor.io/repository/github/dgunning/edgartools)
[![Hatch project](https://img.shields.io/badge/%F0%9F%A5%9A-Hatch-4051b5.svg)](https://github.com/pypa/hatch)
![GitHub](https://img.shields.io/github/license/dgunning/edgartools)
-----

<p align="center">
<a href="https://github.com/dgunning/edgartools">
    <img src="https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/edgar-demo.gif" alt="edgardemo" height="500">
</a>
</p>

# Features

- 🧠 **Intuitive and easy to use**: **edgartools** has a super simple API that is easy to use.
- 🛠️ **Works as a library or a CLI**: You can use edgartools as a library in your code or as a CLI tool.
- 📁 **Access any SEC filing**: You can access any SEC filing since 1994.
- 📅 **List filings for any date range**: You can list filings for any **year, quarter** e.g. or date range `2024-02-29:2024-03-15`
- 🌟 **Best looking edgar library**: Uses **[rich](https://rich.readthedocs.io/en/stable/introduction.html)** library to display SEC Edgar data in a beautiful way.
- 🔄 **Page through filings in the cli**: Use `filings.next()` and `filings.previous()` to page through filings in the terminal.
- 🏗️ **Build Data Pipelines**: Build data pipelines by finding, filtering, transforming and saving filings
- ✅ **Select a filing**: You can select a filing from the list of filings.
- 📄 **View the filing as HTML or text**: Find a filing then get the content as HTML or text.
- 🔢 **Chunk filing text**: You can chunk the filing text into sections for vector embedding.
- 🔍 **Preview the filing**: You can preview the filing in the terminal or a notebook.
- 🔎 **Search through a filing**: You can search through a filing for a keyword.
- 📊 **Parse XBRL**: If a filing has XBRL, you can parse it to a dataframe.
- 💾 **Data Objects**: edgartools automatically downloads and parses the filing into a data object for many form types.
- 📥 **Download any attachment**: You can download any attachment from the filing.
- 🔢 **Get company by Ticker or Cik**: You can get a company using a ticker `Company("SNOW")` or a cik `Company(1640147)`
- 📚 **Get company filings**: You can get all the company's historical filings using `company.get_filings()`
- 📈 **Get company facts**: You can get company facts using `company.get_facts()`
- 💰 **Company Financials**: You can get company financials using `company.financials`
- 🔍 **Lookup Ticker by CUSIP**: You can lookup a ticker by CUSIP
- 📑 **Dataset of SEC entities**: You can get a dataset of SEC companies and persons
- 📈 **Fund Reports**: Search for and get 13F-HR fund reports
- 👤 **Insider Transactions**: Search for and get insider transactions

## Getting started

Install using pip
```bash
pip install edgartools
```

Import and start using
```python
from edgar import *

# Tell the SEC who you are
set_identity("Michael Mccallum mike.mccalum@indigo.com")

filings = get_filings()
```

# Concepts

## How do I find a filing?
Depends on what you know

### A. I know the accession number

```python
filing = find("0001065280-23-000273")
```

### B. I know the company ticker or cik

```python
filings = Company("NFLX").get_filings(form="10-Q").latest(1)
```

### C. Show me a list of filings

```python
filings = get_filings(form="10-Q")
filing = filings[0]
```

## What can I do with a filing

You can **view** it in the terminal or **open** it in the browser, get the filing as **html**, **xml** or **text**, 
and download **attachments**. You can extract data from the filing into a data object.

## What can I do with a company

You can get the company's **filings**, **facts** and **financials**.

# How to use edgartools

| Task                                 | Code                                                  |
|--------------------------------------|-------------------------------------------------------|
| Set your EDGAR identity in Linux/Mac | `export EDGAR_IDENTITY="First Last email@domain.com"` |
| Set your EDGAR identity in Windows   | `set EDGAR_IDENTITY="First Last email@domain.com"`    |
| Set identity in Windows Powershell   | `$env:EDGAR_IDENTITY="First Last email@domain.com"`   |
| Set identity in Python               | `set_identity("First Last email@domain.com")`         |
| Importing the library                | `from edgar import *`                                 |

### Working with filings

| Task                               | Code                                          |
|------------------------------------|-----------------------------------------------|
| Get filings for the year to date   | `filings = get_filings()`                     |
| Get only xbrl filings              | `filings = get_filings(index="xbrl")`         |
| Get filings for a specific year    | `filings = get_filings(2020)`                 |
| Get filings for a specific quarter | `filings = get_filings(2020, 1)`              |
| Get filings for multiple years     | `filings = get_filings([2020, 2021])`         |
| Get filigs for a range of years    | `filings = get_filings(year=range(2010, 2020)` |
| Get filings for a specific form    | `filings = get_filings(form="10-K")`          |
| Get filings for a list of forms    | `filings = get_filings(form=["10-K", "10-Q"])` |
| Show the next page of filings      | `filings.next()`                              |
| Show the previous page of filings  | `filings.prev()`                              |
| Get the first n filings            | `filings.head(20)`                            |
| Get the last n filings             | `filings.tail(20)`                            |
| Get the latest n filings by date   | `filings.latest(20)`                          |
| Get a random sample of the filings | `filings.sample(20)`                          |
| Filter filings on a date           | `filings = filings.filter(date="2020-01-01")` |
| Filter filings between dates       | `filings.filter(date="2020-01-01:2020-03-01")` |
| Filter filings before a date       | `filings.filter(date=":2020-03-01")`          |  
| Filter filings after a date        | `filings.filter(date="2020-03-01:")`          |
| Get filings as a pandas dataframe  | `filings.to_pandas()`                         |

### Working with a filing

| Task                                      | Code                                                      |
|-------------------------------------------|-----------------------------------------------------------|
| Get a single filing                       | `filing = filings[3]`                                     |
| Get a filing by accession number          | `filing = get_by_accession_number("0000320193-20-34576")` |
| Get the filing homepage                   | `filing.homepage`                                         |
| Open a filing in the browser              | `filing.open()`                                           |
| Open the filing homepage in the browser   | `filing.homepage.open()`                                  |
| View the filing in the terminal           | `filing.view()`                                           |
| Get the html of the filing document       | `filing.html()`                                           |
| Get the XBRL of the filing document       | `filing.xbrl()`                                           |
| Get the filing document as markdown       | `filing.markdown()`                                       |
| Get the full submission text of a filing  | `filing.text()`                                           |
| Get and parse the data object of a filing | `filing.obj()`                                            |
| Get the filing attachments                | `filing.attachments`                                      |
| Get a single attachment                   | `attachment = filing.attachments[0]`                      |
| Open an attachment in the browser         | `attachment.open()`                                       |
| Download an attachment                    | `content = attachment.download()`                         |

### Working with a company

| Task                                     | Code                                                          |
|------------------------------------------|---------------------------------------------------------------|
| Get a company by ticker                  | `company = Company("AAPL")`                                   |
| Get a company by CIK                     | `company = Company("0000320193")`                             |
| Get company facts                        | `company.get_facts()`                                         |
| Get company facts as a pandas dataframe  | `company.get_facts().to_pandas()`                             |
| Get company filings                      | `company.get_filings()`                                       |
| Get company filings by form              | `company.get_filings(form="10-K")`                            |
| Get a company filing by accession_number | `company.get_filing(accession_number="0000320193-21-000139")` |
| Get the company's financials             | `company.financials`                                          |
| Get the company's balance sheet          | `company.financials.balance_sheet`                            |
| Get the company's cash flow statement    | `company.financials.cash_flow_statement`                      |

# Installation

```console
pip install edgartools
```

# Usage


## Set your Edgar user identity

Before you can access the SEC Edgar API you need to set the identity that you will use to access Edgar.
This is usually your name and email, or a company name and email.
```bash
Sample Company Name AdminContact@<sample company domain>.com
```

The user identity is sent in the User-Agent string and the Edgar API will refuse to respond to your request without it.

EdgarTools will look for an environment variable called `EDGAR_IDENTITY` and use that in each request.
So, you need to set this environment variable before using it.

### Setting EDGAR_IDENTITY in Linux/Mac
```bash
export EDGAR_IDENTITY="Michael Mccallum mcalum@gmail.com"
```

### Setting EDGAR_IDENTITY in Windows Powershell
```bash
 $Env:EDGAR_IDENTITY="Michael Mccallum mcalum@gmail.com"
```
Alternatively, you can call `set_identity` which does the same thing.

```python
from edgar import set_identity
set_identity("Michael Mccallum mcalum@gmail.com")
```
For more detail see https://www.sec.gov/os/accessing-edgar-data

## Usage

### Importing edgar

```python
from edgar import *
```

### Getting filings
```python

# Get filings for the current year and quarter
filings = get_filings() 

# Get filings for 2022
filings = get_filings(2022)                 # OR filings = get_filings(year=2022)

# Get filings for 2022 quarter 4
filings = get_filings(2022, 4)              # OR filings = get_filings(year=2022, quarter=4)

# Get filings for 2020, 2021 and 2022
filings = get_filings([2020, 2021, 2022])   # OR filings = get_filings(year=range(2020, 2023))

# Get filings for 2020 quarters 1 and 2
filings = get_filings(2020, quarter=[1,2])
```
![Get filings](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/get_filings.jpg)



### Filtering filings

```python
# Filter for form D
filings.filter(form="D")

# Filter for form 10-K and 10-Q 
filings.filter(form=["10-K", "10-Q"])

# When you filter by form e.g. "D" it includes amendments e.g. "D\A". You can omit amendments
filings.filter(form="D", amendments=False)

# Filter by filing_date. date and filing_date mean the same thing
# Get all filings on 2023-02-23
filings.filter(date="2023-02-23")                      
# OR
filings.filter(filing_date="2023-02-23")

# Filter to get all filings between 2023-01-23 and 2023-02-23     
filings.filter(date="2023-01-23:2023-02-23")

# Filter to get all filings since 2023-01-23   
filings.filter(date="2023-01-23")

# Filter to get all filings before 2023-02-23     
filings.filter(date=":2023-02-23")
```

### Combining getting and filtering
```python
get_filings(2022, form="D")
```

### Convert the filings to a pandas dataframe

The filings data is stored in the `Filings` class as a `pyarrow.Table`. You can get the data as a pandas dataframe using
`to_pandas`
```python
df = filings.to_pandas()
```


## Navigating filings

The Filings object allows you to navigate through filings using `filings.next()` and `filings.prev()`. 
This shows you pages of the data - the page size is about 50. 

```python
# To see the next page of data
filings.next()

# To see the previous page
filings.prev()

# To see the current page
filings.current()
```

![Get next filings](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/filings_next.jpg)

## Getting the latest filings

You can get the latest **n** filings by filing_date from a filings using `filings.latest()`.

If you provide the parameter `n` it will return the latest `n` filings.

```python
filing = filings.latest(n=5)
filing
```
![Latest filings](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/latest_filings.jpg)


If you omit this parameter, or set `n=1` it will return a single `Filings object.

```python
filing = filings.latest()
filing
```
![Latest filing](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/latest_filing.jpg)


## Filtering filings

You can filter the filings object using te `filter()` function. This allows you to filter
by filing date, or by form.

### Filtering filings by date

To filter by filing date specify the filing date in **YYYY-MM-DD** format e.g. **2022-01-24**
(Note the parameters `date` and `filing_date` are equivalent aliases for each other)
```python
filings.filter(date="2021-01-24") # or filings.filter(filing_date="2021-01-24")
```
You can specify a filing date range using the colon

```python
filings.filter(date="2021-01-12:2021-02-28") 
```
To filter by dates before a specified date use `:YYYY-MM-DD'

```python
filings.filter(date=":2021-02-28") 
```

To filter by dates after a specified date use `YYYY-MM-DD:'

```python
filings.filter(date="2021-02-28:") 
```

### Filtering filings by form

You can filter filings by form using the `form` parameter. 

```python
filings.filter(form="10-K") 
```

To filter by form e.g. **10-K** and include form amendments use `amendments = True`. 

```python
filings.filter(form="10-K", amendments=True) 
```
![Filter with amendments](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/filter_amendments.jpg)

## Working with a single filing

You can get a single filing from the filings using the bracket operator `[]`, 
specifying the index of the filing. The index is the value displayed in the leftmost
position in the filings table. For example, to get the **10-Q** for **Costco** in the table above
use `filings[3]`

```python
filing = filings[3]
```

![Costco 10Q filing](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/costco_10Q.jpg)

### View the filing homepage
You can view the filing homepage in the terminal using `filing.homepage`

This gives you access to the `FilingHomepage` class that you can use to list all the documents
and datafiles on the filing.

```python
filing.homepage
```
![Filing homepage](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/filing_homepage.jpg)

### Open a filing

You can open the filing in your browser using `filing.open()`. This will work on environments with access to the browser, 
will probably not work on a remote server.
```python
filing.open()
```

### Open the Filing Homepage
You can open the filing homepage in the browser using `filing.homepage.open()`.
```python
filing.homepage.open()
```

### View the filing as Markdown
You can view the filing's HTML content as markdown in the console using `view()`. It works for all filing types
but can be a little slow for filings with large HTML files
```python
filing.view()
```

### Get the filing's html
You can get the html content of the filing using`.html()`
```python
filing.html()
```

### Get the filing's html as Markdown
You can get the html content as markdown using`.markdown()`
```python
filing.markdown()
```

## Viewing and downloading attachments

Every filing has a list of attachments. You can view the attachments using `filing.attachments`

```python
# View the attachments
filing.attachments
```
![Filing attachments](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/filing_attachments.png)

You can access each attachment using the bracket operator `[]` and the index of the attachment.
    
```python
# Get the first attachment
attachment = filing.attachments[0]
```

![Filing attachments](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/filing_attachment.png)

You can download the attachment using `attachment.download()`. This will download the attachment to string or bytes in memory. 

## Automatic parsing of filing data

Now the reason you may want to download attachments is to get information contained in data files.
For example, **13F-HR** filings have attached infotable.xml files containing data from the holding report for that filing.

Fortunately, the library handles this for you. If you call `filing.obj()` it will automatically download and parse the data files
into a data object, for several different form types. Currently, the following forms are supported:

| Form                       | Data Object            | Description                           |
|----------------------------|------------------------|---------------------------------------|
| 10-K                       | `TenK`                 | Annual report                         |
| 10-Q                       | `TenQ`                 | Quarterly report                      |
| 8-K                        | `EightK`               | Current report                        |
| MA-I                       | `MunicipalAdvisorForm` | Municipal advisor initial filing      |
| Form 144                   | `Form144`              | Notice of proposed sale of securities |
| C, C-U, C-AR, C-TR         | `FormC`                | Form C Crowdfunding Offering          |
| D                          | `FormD`                | Form D Offering                       |
| 3,4,5                      | `Ownership`            | Ownership reports                     |
| 13F-HR                     | `ThirteenF`            | 13F Holdings Report                   |
| NPORT-P                    | `FundReport`           | Fund Report                           |
| EFFECT                     | `Effect`               | Notice of Effectiveness               |
| And other filing with XBRL | `FilingXbrl`           |                                       |

For example, to get the data object for a **13F-HR** filing you can do the following:

```python
filings = get_filings(form="13F-HR")
filing = filings[0]
thirteenf = filing.obj()
```

![Filing attachments](docs/images/thirteenF.png)

If you call `obj()` on a filing that does not have a data file, then it will return `None`.


## Working with XBRL filings

Some filings are in **XBRL (eXtensible Business Markup Language)** format. 
These are mainly the newer filings, as the SEC has started requiring this for newer filings.

If a filing is in XBRL format then it opens up a lot more ways to get structured data about that specific filing and also 
about the company referred to in that filing.

The `Filing` class has an `xbrl` function that will download, parse and structure the filing's XBRL document if one exists.
If it does not exist, then `filing.xbrl()` will return `None`.

The function `filing.xbrl()` returns a `FilingXbrl` instance, which wraps the data, and provides convenient
ways of working with the xbrl data.


```python
filing_xbrl = filing.xbrl()
```

![Filing homapage](https://raw.githubusercontent.com/dgunning/edgartools/main/docs/images/10Q_xbrl.jpg)


## [Using the Company API](COMPANY_API.md)

With the Company API you can find a company by ticker or CIK, and get the company's filings, facts and financials.

```python
Company("AAPL")
        .get_filings(form="10-Q")
        .latest(1)
        .obj()
```

![expe](docs/images/aapl-10Q.png)

See **[Using the Company API](COMPANY_API.md)**

# Contributing

Contributions are welcome! We would love to hear your thoughts on how this library could be better at working with SEC Edgar.

## Reporting Issues
We use GitHub issues to track public bugs. 
Report a bug by [opening a new issue](https://github.com/dgunning/edgartools/issues); it's that easy!

## Making code changes
- Fork the repo and create your branch from master.
- If you've added code that should be tested, add tests.
- If you've changed APIs, update the documentation.
- Ensure the test suite passes.
- Make sure your code lints.
- Issue that pull request!



# License

`edgartools` is distributed under the terms of the [MIT](https://spdx.org/licenses/MIT.html) license.

## Contact

[LinkedIn](https://www.linkedin.com/in/dwight-gunning-860124/)


## Supporters
[![Stargazers repo roster for @dgunning/edgartools](https://reporoster.com/stars/dgunning/edgartools)](https://github.com/dgunning/edgartools/stargazers)
[![Forkers repo roster for @dgunning/edgartools](https://reporoster.com/forks/dgunning/edgartools)](https://github.com/dgunning/edgartools/network/members)

## Subscribe to Polar
<picture>
2  <source media="(prefers-color-scheme: dark)" srcset="https://polar.sh/embed/subscribe.svg?org=polarsource&label=Subscribe&darkmode">
3  <img alt="Subscribe on Polar" src="https://polar.sh/embed/subscribe.svg?org=polarsource&label=Subscribe">
4</picture>
