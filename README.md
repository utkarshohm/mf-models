# mutual-fund-models
Models (data structures) required to make a mutual fund investment platform

## Context
### Real-life application of library
I built and operated a mutual fund investing platform as an AMFI licensed mutual fund distributor for a year. I used this library to store all my data. Since my investing website was built on django, I have used django models. You can build this platform without or with any other framework of your choice.

### Open source in fintech?!
The finance industry believes that differentiation in fintech can come from building an execution/transaction platform. I believe that, on the contrary, execution will soon be commoditized and differentiation will come from better products, ease of their use and large-scale distribution. This is why I am open-sourcing my [whole mutual fund execution platform](https://github.com/utkarshohm/mutual-fund-platform), and these models are just its subset.

## Models
### Data structure
4 key data structures are necessary for a mutual fund transaction platform. Regulations require to carefully archive this data for 5 years. 
* `funds.py` stores mutual fund schemes' official SID details, ratings, returns, owner, rta, managers, benchmark indices, portfolio and history.
* `graphs.py` stores time series data of funds and indices (like BSE Sensex, SBI fixed deposit rate), at daily frequency. 
* `users.py` stores kyc, bank, fatca and mandate details for each investor.
* `transactions.py` stores each purcahse/redeem transaction's key details incl status, datetime stamps, payment details,  corresponding API queries made to BSEStarMF and corresponding responses received. The BSE tables are used for the placing transactions through [BSEStarMF API](https://github.com/utkarshohm/mutual-fund-platform#about-bse-star-mf).

### Choice of database
#### Relational data
I used a relational database MySQL to store all funds, users and transactions data. PostgreSQL would also be a great choice. This ER diagram should help. ![ER diagram](/erd.png)

#### Time series data
I chose document database MongoDB to store the graphs models. Every scheme was a document because time series data was mostly requested fund-by-fund for graph visualisations. Note that aggregates of risk and return like average return etc are periodically calculated on top of the time series data and stored in funds models. Time series databases like Druid and InfluxDB would have been good options too.

## Need help setting this up or want to contribute?
Feel free to raise an issue and I will get back asap
