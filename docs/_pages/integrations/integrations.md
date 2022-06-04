---
permalink: /integrations/
title: "Integrations"
toc: true
toc_sticky: true
toc_label: "On this page"
toc_icon: "cog"
---

## Overview

This document describes the basic integrations offered by QF-Lib. This list will be extended in the future as we 
constantly work on further developments.


## Portara

![](../../assets/images/Portara-CQG_logo.png)

[Portara](https://portaracqg.com/) is a staple CQG product providing CQG Datafactory data to hedge funds, CTA’s quants
and traders globally. Portara allows the extraction
of [continuous intraday data](https://portaracqg.com/continuous-futures-data/) and individual data down to the 1 minute
resolution. Data output is homogenous ASCII/CSV/TXT is platform neutral and is guaranteed to operate through any
database solution. Portara and CQG have the largest reach of data access globally covering all futures FX and cash
market exchanges.

**Four Integrated Databases:**

Portara provides up to 123 years
of [historical daily futures data](https://portaracqg.com/historical-daily-futures-data/) from 1899. Portara daily
database contain FIVE price points so you can base the close on either Last Price or Settle. Portara
has [historical intraday futures data](https://portaracqg.com/historical-intraday-futures-data/)
starting from 1983 and also
has [historical tick data and level 1 futures data](https://portaracqg.com/historical-futures-tick-data/) covering
global markets. CQG data integrity department ensures the data is clean and hedge fund ready half hour after markets
close.

**Accessibility & Awards:**

Portara infrastructure has been built in collaboration with CQG to solve the huge cost burden associated typically with
institutional database modelling of this nature. Portara's $10m CQG Datafactory databases are available via flexible
subscriptions and one-off data dumps 100x fold less in cost than conventional CQG Data Factory purchases. Portara has
many of the world's top CTA's, banks and hedge funds who have Portara integrated into their daily trading solutions.
Portara has won [Best Futures Data Provider](https://portaracqg.com/2018/09/20/best-long-time-historical-intraday-data/)
award FOUR times voted by industry leaders and Hedge Fund Magazine.

**Portara integration**

For Portara integration, we introduced `PortaraDataProvider` and the specific tickers: `PortaraTicker` and `PortaraFutureTicker`.
 
`PortaraDataProvider` is a dedicated data provider that loads Portara data for future contracts into the backtest. It supports both continuous series and individual contracts (tenors). The required format is .csv for pricing data (with headers) and .txt for expiration dates (as it is in Portara). Currently the only supported data frequencies are daily frequency and 1-minute bar frequency. After preloading 1-minute bars, it is possible to aggregate them selecting a different frequency in the get price method.
 
`PortaraTicker` is a simple ticker used with continuous data, and `PortaraFutureTicker` is used to work with tenors.
 
In order to see exemplary files which may be used with the PortaraDataProvider (e.g. structure of expiration
  dates file), check the mock files in the tests directory:
  qf_lib_tests > unit_tests > data_providers > portara > input_data.

The input files are the examples of the expected structure of the files (there are not directly from Portara)
 
To see examples using Portara data provider, check the demo scripts:
  demo_scripts > data_providers > portara
 
The files used in demo can be run with the data that is available here: [CQG Sample Data | Download CQG Data Factory Samples at PortaraCQG](
https://mmm.cern.ch/owa/redir.aspx?C=nJ1q2tM5gwqbs97qIoeYHNV2k6q_A5_pVyuxRUYX1Pl0CSUqHEbaCA..&URL=https%3a%2f%2fportaracqg.com%2fsample-data%2f)


## Bloomberg
QF-Lib offers a well tested DataProvider implementation for Bloomberg. Specifically please refer to the modules below:
#### Bloomberg Standard API
`BloombergDataProvider` `FuturesDataProvider`

#### Bloomberg Enterprise Access Point (BEAP) HAPI
`BloombergBeapHapiDataProvider` 

#### Bloomberg Execution Management System (EMSX) z
Will become available soon 

## Binance

#### Broker
`BinaceBroker`
class implements synchronous interactions with Binance API. 
Binance Broker provides all basic functions of the Broker interface
#### Data provider
`BinaceDataProvider`
Binance Data Provider downloads data directly from Binance. Particularly, the data provider can be used in backtests and live trading.
Downloaded data is saved in .csv format.

## Haver
`HaverDataProvider` is an implementation of a DataProvider interface for  Haver Analytics - the premier provider of time series data for the global strategy and research community.

## Interactive Brokers
#### Broker
`IBBroker`
class implements synchronous interactions with IB API. 
 Main purpose of this class is to connect to the API of IB broker and send orders. It provides the functionality, 
which allows to retrieve a.o. the currently open positions and the value of the portfolio.

## CSV
`CSVDataProvider`
Generic Data Provider that uses local csv files. Is very flexible and can accommodate most files. 


