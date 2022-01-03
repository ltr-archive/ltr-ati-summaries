# Long-term retention Access to Information summaries

This repository contains archived downloads of the Government of Canada's [completed Access to Information request summaries](https://open.canada.ca/en/search/ati), in CSV format.

These CSV files are downloaded automatically, at the end of each month, from [the CSV dataset of completed ATI summaries](https://open.canada.ca/data/en/dataset/0797e893-751e-4695-8229-a5066e4fe43c). At present, the official dataset has a two-year retention period, and older ATI summaries are automatically deleted.

This repository retains those summaries indefinitely, for research and historical purposes. 

Each CSV file stored in this repository is a point-in-time download of the official dataset. Each file only contains two years worth of data. For longer-term analysis, you can manually combine multiple CSV files together.

## How it works

1. At the end of each month, a [scheduled AWS Lambda function](https://github.com/ltr-archive/ltr-lambda-helpers#lambda-download-to-s3py) downloads the CSV file from open.canada.ca and stores it in an S3 bucket. 

2. The following day, a [GitHub Action function](https://github.com/ltr-archive/ltr-ati-summaries/blob/main/.github/workflows/sync-s3-data.yml) pulls the data from the S3 bucket and updates this repository with the contents.

Note that GitHub has a [per-file-size limit of 100MB](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github#file-size-limits). To use this approach with larger datasets, an in-between step of splitting the original CSV file into several smaller files would be required.

Inspired by the [ATI Review – Interim What We Heard Report](https://www.canada.ca/en/treasury-board-secretariat/services/access-information-privacy/reviewing-access-information/the-review-process/ati-review-interim-what-we-heard-report.html#toc2-2).

As always, [feedback](https://twitter.com/sboots) and [issue requests](https://github.com/ltr-archive/ltr-ati-summaries/issues) welcome!
