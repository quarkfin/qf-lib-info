---
permalink: /about/
title: "About"
multi-tool-gallery:
  - url: /assets/images/about/multi-tool-example-1.png
    image_path: /assets/images/about/multi-tool-example-1.png
    alt: "Multi-tool example picture"
  - url: /assets/images/about/multi-tool-example-2.png
    image_path: /assets/images/about/multi-tool-example-2.png
    alt: "Multi-tool example picture"
  - url: /assets/images/about/multi-tool-example-3.png
    image_path: /assets/images/about/multi-tool-example-3.png
    alt: "Multi-tool example picture"  
backtester-gallery:
  - url: /assets/images/about/backtester-example-1.png
    image_path: /assets/images/about/backtester-example-1.png
    alt: "Backtester example picture"
  - url: /assets/images/about/backtester-example-2.png
    image_path: /assets/images/about/backtester-example-2.png
    alt: "Backtester example picture"
  - url: /assets/images/about/backtester-example-3.png
    image_path: /assets/images/about/backtester-example-3.png
    alt: "Backtester example picture"  
backtest-reports-gallery:
  - url: /assets/images/about/backtest-report-1.png
    image_path: /assets/images/about/backtest-report-1.png
    alt: "Backtest report"
  - url: /assets/images/about/backtest-report-2.png
    image_path: /assets/images/about/backtest-report-2.png
    alt: "Backtest report"
toc: true
toc_sticky: true
toc_label: "On this page"
toc_icon: "cog"       
---

QF-Lib is a Python library that provides high quality tools for quantitative finance. Among the features, there are modules for portfolio construction, time series analysis, risk monitoring and diverse charting package. The library allows analyzing financial data in a convenient way, while providing a wide variety of tools for data processing and presentation of the results.

QF-Lib is a convenient environment for conducting your own analysis. The results will be presented in a practical form and include number of charts and statistical measures.  

An extensive part of the project is dedicated to backtesting investment strategies. The Backtester uses an event-driven architecture and simulates the events such as daily market opening or closing. Thanks to the architecture based on interfaces, it is easy to introduce custom settings. Tested strategies can consist of different alpha models, position-sizing techniques, risk management settings and can specify commission pricing or slippage models. After testing a strategy on historical data, user can put it into trading environment without any modifications.

## Multi-tool for any financial research
QF-Lib is a Python library that provides various tools for portfolio construction, time series analysis, and risk monitoring. It allows analysing financial data in a convenient way and provides a wide variety of tools to process data and to present the results.

### Tech Specs
- Flexible data sourcing (Bloomberg, Quandl, IB, Excel, local DB)
- Adapted data containers (Based on Pandas)
- Rich charting package
- Export to Excel, PDF or Email notifications

### Applications
- Financial analysis
- Building custom market indicators
- Financial products evaluation
- Portfolio construction
- Risk management
- Academic research
- Timeseries analysis

{% include gallery id="multi-tool-gallery" %}

## A powerful, event-driven Backtester
A large part of the project is dedicated to backtesting investment strategies. The Backtester uses an event-driven architecture and simulates events such as daily market opening or closing. It is designed to test and evaluate any custom investment strategy.

### Tech Specs
- Modular design (Alpha Models, Risk Management, Position Sizing)
- Easy to build custom strategies
- Tools to prevent look-ahead bias
- Detailed summary of the backtest
- Deploy strategies on testing or production environment

### Applications
- Financial engineering
- Investment strategy development evaluation and testing
- Risk management
- Financial analysis
- Verification of investment ideas

{% include gallery id="backtester-gallery" %}

## Examples of Backtest Reports

{% include gallery id="backtest-reports-gallery" %}

# Modules
To find more specific information please check the class
documentation in the source code or refer to the examples of the usage in `qf-lib/demo_scripts` directory.

### Analysis
The components included in this catalogue are used to analyze strategy progress and generate files containing
the analysis results. Examples of some documents created using these components are as follows:
* [TearsheetWithoutBenchmark](readme_example_files/tearsheet_without_benchmark.pdf),
* [PortfolioTradingSheet](readme_example_files/portfolio_trading_sheet.pdf),
* [TimeseriesAnalysis](readme_example_files/timeseries_analysis.xlsx),
* [TradesAnalysis](readme_example_files/trades_analysis.csv),
* [ModelParamsEvaluator](readme_example_files/model_params_evaluator.pdf).

### Backtesting
The module contains the code of a Backtester, which  uses an event-driven architecture. The class that controls the
flow of the events is `EventManager`. `EventManager` contains an events queue. When the `dispatch_next_event` is called,
then the manager takes the event from the queue and notifies all interested components. Components may
also generate new events by using the `publish(event)` method.

The module contains the following tools:
- **alpha_model** - a part of the Strategy responsible for calculating Signals. Each Signal contains information such as suggested exposure, fraction at risk (helpful to determine the stop loss levels), signal confidence or expected price move.
- **broker** - components which simulate a broker in the backtests. The Broker abstract class is an interface for all
potential specific implementations of brokers.
- **contract**:
    - **contract_to_ticker_conversion** - this directory contains tools that allow to map Broker specific contract objects onto corresponding Tickers
- **data_handler** - a wrapper which can be used with any DataProvider in both live and backtest environment.
It makes sure that data "from the future" is not passed into components in the backtest environment. DataHandler should be
used by all the Backtester's components.
- **events** - this module contains all events crucial for the Backtester as well as event listeners and notifiers. More
details may be found [here](../backtest_flow/).
- **execution_handler** - the `ExecutionHandler` abstract class handles the interaction between a set of order objects
and the set of Transaction objects that actually occur in the market. Its subclass `SimulatedExecutionHandler` is used
in the Backtester and surrounded with various components specialised in handling different types of Orders or
responsible for applying slippage, commission costs, etc.
- **fast_alpha_models_tester** - FastAlphaModelsTester is a non-event-driven version of the backtester. It allows for quick
testing of AlphaModels' signal suggestions. As a result it generates a timeseries of portfolio returns and a table of
trades for each asset (both as BacktestSummary). The operation time of FastAlphaModelsTester is significantly shorter
in comparison to the use of Backtester, but instead the results accuracy might be lower.
- **monitoring**:
    - `BacktestMonitor` - allow for the observation of backtest results. Displays the portfolio value as the backtest progresses and generates multiple PDF files with details about the backtest,
    saves the portfolio values and trades to an Excel file.
    - `BacktestResult` is a class providing simple data model containing information about the backtest:
    for example it contains a portfolio with its timeseries and trades. It can also gather additional information.
- **order** - orders are generated by a strategy, then processed by `PositionSizer` and finally executed
by `ExecutionHandler`. Their type (market order, stop order, etc.) is determined as `ExecutionStyle`.
- **orders_filter** - components which are able to adjust the final orders list to meet various requirements e.g. volume limitations.
- **portfolio** - object, which stores the actual `BacktestPosition` objects.
- **position_sizer** - `PositionSizer` is used to convert signals generated by `AlphaModel` to `Orders`. There are
different types available.
- **signals**:
    - **signal** - objects of this class are used in the portfolio construction process. They are returned by `AlphaModels` to
    determine the suggested trend direction as well as its strength.
    - **signals_register** - components used to save signals processed by the `PositionSizer`. The allow to later analyze all signals generated by
    the model and to present them in a readable form.
- **strategies**:
    - **abstract_strategy** - basic interface used to create a generic strategy.
    - **alpha_model_strategy** - puts together AlphaModels with corresponding settings and features.
    - **signals_generators** - contains wrappers, which facilitate the subscription process of the Strategy to events (e.g. to the BeforeMarketOpenEvent).
- **trading_session** - the component which wires all other components together. It keeps all the necessary settings for
the session (e.g. start date and end date of trading). It has the events' loop in which `EventManager` takes events from
the events' queue and dispatches to event listeners.

### Common
The package contains all the generic tools:
- **enums** - predefined constants that are used in multiple project components
- **exceptions** - additional exception types which are specific to this project
- **tickers** - classes representing tickers of different kinds, ex. BloombergTicker or QuandlTicker
- **timeseries_analysis** - aggregating different measures of the timeseries such as total return, volatility,
sharpe ratio and many others
- **utils** - various tools:
    - *close_open_gap* - analysing the price jumps during the break after market close and before market open
    - *confidence_interval* - used for performance vs. expectation studies. Tools to check if the strategy performs withing the expectations
    - *dateutils* - manipulating the dates (e.g. change format, get the end of month date)
    - *factorization* - multi-linear regression tools to analyse the sensitivity
    - *logging* - making entries in the system log (all messages should be printed through loggers)
    - *miscellaneous* - everything that is hard to categorize
    - *numberutils* - processing numbers (e.g. checking if a variable is a finite number)
    - *ratios* - calculating financial ratios (measurements like Sharpe Ratio or Omega Ratio)
    - *returns* - measurements of returns (e.g. drawdowns, linear regression, CVar) and tools for manipulating them
    (e.g. aggregating, calculating compound annual growth rates, converting simple returns to log-returns)
    - *technical_analysis* - facilitating the usage of TA-Lib functions in the project
    - *volatility* - calculating volatility (e.g. intraday_volatility, total volatility, rolling volatility)

### Containers
Data structures that extend the functionality of `pandas Series`, `pandas DataFrame` and `numpy DataArray` containers
and facilitate the computations performed on time-indexed structures of prices or price returns. Depending on the stored
data, the 1D and 2D structures have their sub-types, such as e.g. `PricesSeries` or `SimpleReturnsDataFrame`.
The most generic 1D and 2D types are `QFSeries` and `QFDataFrame`. Any time-indexed `DataFrame` or `Series`
can be cast to a specific type using the `cast_dataframe` and `cast_series` functions.

All containers used in the system are listed below:

#### 1-Dimensional containers
##### pandas.Series
Vector of values. Can be indexed using both integer-based indices or label-based indices. Usually, it is labeled with
dates (pandas.DateTimeIndex/pandas.PeriodsIndex).

##### TimeIndexedContainer
It is an abstract class which introduces methods specific for time-indexed containers (timeseries, multi-timeseries).

##### QFSeries
It inherits from pandas.Series and from TimeIndexedContainer. It is meant to store timeseries. Normally it shouldn't be
instantiated if the more specific type of data is known (e.g shouldn't be used for storing prices or returns), because
a lot of its methods throw NotImplementedError() (e.g conversions to log-returns or simple returns).

It has 2 direct subclasses:
- PricesSeries,
- ReturnsSeries.

QFSeries concrete subclasses (LogReturnsSeries, SimpleReturnsSeries, PricesSeries) can be converted from one to another
(each concrete class knows how to be converted to each of the remaining classes). It is important to remember that some
operations on Series may result with the incorrect type of the series. In those cases, one may use the convenience
method: cast_series, which just changes the type of the series without changing values of actual data stored inside.

All QFSeries subclasses are described in the following sections:

##### qf_lib.containers.PricesSeries
Container meant for storing timeseries of prices.

##### qf_lib.containers.ReturnsSeries
Super-class for LogReturnsSeries and SimpleReturnsSeries. It contains the logic that is common for all series of returns.

##### qf_lib.containers.LogReturnsSeries
Container meant for storing timeseries of log-returns: r_log = log(p2/p1), where p2 is the next price after p1
and r_log is the log-return. log is a natural logarithm.

##### qf_lib.containers.SimpleReturnsSeries
Container meant for storing timeseries of simple returns: r = p2/p1 - 1, where p2 is the next price after p1
and r is the simple return (arithmetic return).

#### 2-Dimensional containers
##### pandas.DataFrame
DataFrame is the 2-D container (matrix-like) for storing data. It may also have just one column (but still won't be
considered a Series, however it can be easily converted then by calling the squeeze() method.

##### QFDataFrame
It inherits from pandas.DataFrame. It is a corresponding class for QFSeries. It has 3 direct subclasses:
- PricesDataFrame,
- SimpleReturnsDataFrame,
- LogReturnsDataFrame.

All of the QFDataFrame subclasses can be converted one to another. It is important to remember, that some operations
on DataFrame may result with a lost information about a containers type or the type may be wrong. That's why there is
a convenience method: cast_dataframe which can be used to change the container's type without doing any conversions
(without changing the actual values stored inside of the container).

In QFDataFrame it is assumed that all columns have the same frequency, consider more or less the same time frame
and contain data of the same type (e.g. only log-returns or only prices).

##### qf_lib.containers.PricesDataFrame
DataFrame which contains only prices.

##### qf_lib.containers.SimpleReturnsDataFrame
DataFrame which contains only simple returns.

##### qf_lib.containers.LogReturnsDataFrame
DataFrame which contains only log-returns.

#### 3-Dimensional containers
##### QFDataArray
The only 3-D container in the system is QFDataArray. It inherits from xr.DataArray. Its dimensions are usually DATES,
TICKERS, FIELDS (as in `qf_lib.containers.dimension_names`). It should be created using the create() class method
or converted from a regular xr.DataArray with from_xr_data_array(). Use of QFDataArrays instead of different 3-D structures
enables simple slicing and conversion to 2-D and 1-D QF-Lib containers.

#### Futures
In order to support futures contracts chaining `FutureContract`, `FutureTicker` and `FuturesChain` structures were introduced.

### Data providers
Their purpose is to download the financial data from data providers such as Bloomberg or Quandl. Providers shall return data in the
containers defined in `qf_lib.containers` (like `QFSeries` or `QFDataFrame`).

### Documents utils
The package contains the following tools:
- *document_exporting* - templates, styles and components used to export the results and save them as files
- *email_publishing* - creation and sending emails from given templates
- *excel* - exporting and importing data to/from Excel files

### Indicators
Market indicators that can be implemented in strategies or used for the analysis.

### Interactive Brokers
This catalogue contains an interface which allows to communicate with the Interactive Brokers platform. The `IBBroker`
class can be used in the live trading of your strategy.

### Plotting
To make plotting easier we implemented a lot of chart templates along with some easy-to-use decorators. Examples of their
use are shown in the `qf-lib/demo_scripts/charts` catalogue.

Each chart is a class that has a plot() method taking no arguments. An object should be initialised, then the decorators
can be added (e.g. `DataElementDecorator` or `LegendDecorator`) and finally plot() method should be called. Running
the plot() method will not display the figure. It will only draw on the axis. In order to display all the figures
that were already plotted run plt.show(block=True) where plt is defined as `import matplotlib.pyplot as plt`.
It is therefore possible to save the charts as files or add them to the report without displaying them.

### Portfolio Construction
The components in this catalogue can be helpful in the process of portfolio construction - they allow to calculate
the covariance matrix of assets and take it as input to build the portfolio according to suggested models.
The construction process involves covariance matrix optimization with one of the implemented optimizers.


### Testing tools
Basic tools that are used in software testing. They include functions that allow e.g. comparing data structures
or creating sample column names for the test containers.
