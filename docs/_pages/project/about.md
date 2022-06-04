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

## Modules
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
**pandas.Series**
Vector of values. Can be indexed using both integer-based indices or label-based indices. Usually, it is labeled with
dates (pandas.DateTimeIndex/pandas.PeriodsIndex).

**TimeIndexedContainer**
It is an abstract class which introduces methods specific for time-indexed containers (timeseries, multi-timeseries).

**QFSeries**
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

**qf_lib.containers.PricesSeries**
Container meant for storing timeseries of prices.

**qf_lib.containers.ReturnsSeries**
Super-class for LogReturnsSeries and SimpleReturnsSeries. It contains the logic that is common for all series of returns.

**qf_lib.containers.LogReturnsSeries**
Container meant for storing timeseries of log-returns: r_log = log(p2/p1), where p2 is the next price after p1
and r_log is the log-return. log is a natural logarithm.

**qf_lib.containers.SimpleReturnsSeries**
Container meant for storing timeseries of simple returns: r = p2/p1 - 1, where p2 is the next price after p1
and r is the simple return (arithmetic return).

#### 2-Dimensional containers
**pandas.DataFrame**
DataFrame is the 2-D container (matrix-like) for storing data. It may also have just one column (but still won't be
considered a Series, however it can be easily converted then by calling the squeeze() method.

**QFDataFrame**
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

**qf_lib.containers.PricesDataFrame**
DataFrame which contains only prices.

**qf_lib.containers.SimpleReturnsDataFrame**
DataFrame which contains only simple returns.

**qf_lib.containers.LogReturnsDataFrame**
DataFrame which contains only log-returns.

#### 3-Dimensional containers
**QFDataArray**
The only 3-D container in the system is QFDataArray. It inherits from xr.DataArray. Its dimensions are usually DATES,
TICKERS, FIELDS (as in `qf_lib.containers.dimension_names`). It should be created using the create() class method
or converted from a regular xr.DataArray with from_xr_data_array(). Use of QFDataArrays instead of different 3-D structures
enables simple slicing and conversion to 2-D and 1-D QF-Lib containers.

### Futures
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


## Events
Events comprise a crucial part of the Backtester architecture. This section covers the overall specification of TimeEvents,
EventNotifiers and EventListeners and contains a few examples of customly defined Events.

### General types of events
The event-driven architecture of the Backtester, defines and utilizes the following types of events:
- `Event` - super-type for all events,
- `EmptyQueueEvent` - occurs whenever there are no events to dispatch in the `EventManager`,
- `EndTradingEvent`- occurs when the trading should stop (e.g. when the backtest should be terminated). For now it is
generated by `DataHandler` in the backtest if there is no more data available for the backtest. However, in the future,
this could be triggered by the user (from GUI or console),
- `TimeEvent` - various events which have the notion of time. Examples of events, which are based on the `TimeEvent`,
 would be `RegularTimeEvent` and `PeriodicEvent`, described in more details in the subsequent section.

### Notifiers
Each of the events is correlated with a certain type of notifier. The notifiers should be registered along with their
corresponding events types (defined by `EventNotifier.events_type()`) in the `EventManager` using the
`EventManager.register_notifiers()` method. After being registered notifier can have listeners added to it.
Hence, whenever an event of type associated with the `EventNotifier` occurs, `EventManager` will tell the notifier
to notify all its listeners. Currently the following notifiers, grouped together in the `Notifiers` class, are defined
in the Backtester:
- `AllEventNotifier` - corresponds to the most general type of events (the `Event`).
- `EmptyQueueEventNotifier` - corresponds to the `EmptyQueueEvents`.
- `EndTradingEventNotifier` - corresponds to the `EndTradingEvents`.
- `Scheduler` - corresponds to various types of `TimeEvents`. Scheduler is responsible for generating the time events,
whenever the `EventManager` queue is empty. Then the `TimeFlowController` triggers the Scheduler to generate the events.

### Listeners
In order to subscribe a listener to a certain type of Event, the `subscribe` function should be used. For example, in
order to subscribe a listener to a certain type of `TimeEvent`, the following function should be used:

```python
Scheduler.subscribe(TypeOfEvent, listener)
```

Listener will be only notified of events of this concrete type (e.g. `MarketOpenEvent` and not all `TimeEvents`).
Listener needs to have a proper callback method, defined in `TimeEvent.notify()` method.

```python
class CustomTimeEvent (TimeEvent):
    def notify(self, listener) -> None:
        listener.on_custom_event()

class CustomTimeEventListener:
    def on_custom_event(self):
        ...
```


### Specific Time Events
In order to facilitate the operation of Backtester, the following events, based on `TimeEvents`, where defined:

#### `RegularTimeEvent`  
These are events which occur on a regular basis (e.g. each day at 17:00, each first Wednesday of a month, etc.).
An example of a `RegularTimeEvent` may be the `MarketOpenEvent`, occurring at every market open.

To facilitate the definition of `RegularTimeEvent` the `RegularDateTimeRule` helper class may be used. It allows
to easily compute the next trigger time.  It accepts a "time dictionary", consisting of a subset of following fields:
year, month, weekday, day, hour, minute, second, microsecond. In order to schedule the event for 8:15 a.m. every day,
all the fields: hour, minute, second, microsecond should be filled. The `RegularTimeEvent` needs to implement
`trigger_time`, `next_trigger_time` and `notify` functions (see example below).

```python
class CustomRegularTimeEvent(RegularTimeEvent):
    """
    Rule which is triggered every Monday at 8:15 a.m.
    The listeners for this event should implement the
    on_monday_morning() method.
    """

    _trigger_time_dictionary = {
        "weekday": 0, "hour": 8, "minute": 15,
        "second": 0, "microsecond": 0
    }
    _time_rule = RegularDateTimeRule(**trigger_time_dict)

    @classmethod
    def trigger_time(cls) -> RelativeDelta:
        return RelativeDelta(**cls.trigger_time_dict)

    def next_trigger_time(self, now: datetime) -> datetime:
        next_trigger_time = self._time_rule.next_trigger_time(now)
        return next_trigger_time

    def notify(self, listener) -> None:
        listener.on_monday_morning(self)
```

Examples of predefined `RegularTimEvents`:
- `MarketOpenEvent`,
- `MarketCloseEvent`

#### `PeriodicEvent`
These are events which occur on a regular basis, similarly to `RegularTimeEvents`. The only diffrence is that, they may
occur with a predefined frequency (e.g. daily frequency, 1 minute frequency etc.) within a given time range. For example

The `PeriodicEvent` is triggered only within the [start_time, end_time] time range with the given frequency.
It is triggered always at the start_time, but not necessarily at the end_time. For example:

```python
start_time = {
    "hour": 13, "minute": 20,
    "second": 0, "microsecond": 0
}
end_time = {
    "hour": 16, "minute": 0,
    "second": 0, "microsecond": 0
}
frequency = Frequency.MIN_30
```

This event will be triggered at 13:20, 13:50, 14:20, 14:50, 15:20, 15:50, but not at 16:00.

The `next_trgiger_time()` in case of `PeriodicEvent` skips automatically Saturdays and Sundays.

#### `IntradayBarEvent`
`IntradayBarEvent` is a special type of `PeriodicEvent`, used by `SimulatedExecutionHandler` to support
intraday trading. The frequency is hardcoded to be equal to 1 minute and the time range is equal to the range
between market open and market close times. They call on_new_bar function on the listener at every trigger time between
start_time and end_time, which denote the time range between market open (exclusive) and market close (exclusive).

#### `SingleTimeEvent`
`SingleTimeEvent` represents type of all these events that associated with one specific date time (e.g. 2017-05-13 13:00)
and which will never be repeated in the future.

This type of events is mostly used along with data being passed between different components. In order to schedule
new single time event, `SingleTimeEvent.schedule_new_event(datetime, data)` function should be used. Then, whenever
this event occurs, it is possible to access this data using `get_data` function.

#### `ScheduleOrderExecutionEvent`
`ScheduleOrderExecutionEvent` is a special type of `SingleTimeEvent`. It is used in the Backtester to schedule the
execution of Orders in the future.

Similarly to `SingleTimeEvent`, it also schedules new event by adding the (datetime, data) pair to the _datetimes_to_data
dictionary, but it also assumes data has the structure of a dictionary, which maps orders executor instance to orders,
which need to be executed. Multiple events can be scheduled for the same time - the orders and order executors will be
appended to existing data.

### Backtester Events Flow

The following graphics depicts the typical flow of events in the Backtester. It presents the content of Events Queue
in the `EventManager` and order of executed events in a certain point of time. At the beginning of each Backtest
execution the Events Queue is empty. The following example illustrates an intraday events flow, considering a point
of time after the market open and before market close, when already a `ScheduleOrderExecutionEvent` was created.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/qflib_events_flow.png){: .align-center}

1. The Events Queue is currently empty. When the `EventManager.dispatch_next_event()` function is called, the
`EmptyQueueEvent` is returned.

2. The `EmptyQueueEvent` notifier notifies its listener - `TimeFlowController`, which triggers `Scheduler` to generate
new `TimeEvents`. All the generated `TimeEvents` are appended to the Events Queue in the following order:
   * `ScheduleOrderExecutionEvent` have the highest priority and thus, they appear first in the queue,
   * `IntradayBarEvent` - these events have the same priority as `MarketOpenEvent` and `MarketCloseEvent`,
   * all other defined `TimeEvents`.

3. `EventManager.dispatch_next_event()` returns the `ScheduleOrderExecutionEvent`.

4. The notifier of`ScheduleOrderExecutionEvent` (`Scheduler`) notifies its listener - `SimulatedExecutionHandler`. At this
point, all scheduled Orders are being accepted by corresponding `SimulatedExecutor` (e.g. market orders are appended
to the list of awaiting orders of `MarketOrderExecutor`).

   Afterwards, the  `EventManager.dispatch_next_event()` function is called and `IntradayBarEvent` is returned.

5. The notifier of`IntradayBarEvent` (`Scheduler`) notifies its listener - `SimulatedExecutionHandler`. At this point of time,
all of the orders, that are stored in the lists of awaiting orders in each of the `SimulatedExecutors`, are being processed
and if they fulfill the necessary conditions (e.g. a price for the specified asset is currently available), they are
being executed. In the backterster, the execution of a single order is simulated by converting the Order into Transaction.

   When the processing and execution of the orders is finished, all positions that are currently open in the Portfolio
   are updated, by getting their most recent prices (`Portfolio.update()`). In case of intraday trading, the Portfolio
   is updated additionally at the time of market open on `MarketOpenEvent`, and after the market close on
   `AfterMarketCloseEvent`.

   Afterwards, the  `EventManager.dispatch_next_event()` function is called and a custom event is returned.

6. The notifier of the custom event notifies its listeners, which then perform the necessary actions.  Then, the
`EventManager.dispatch_next_event()` function is called and the next custom event is returned.

7. The notifier of the next custom event notifies its listeners and the Events Queue becomes empty again.

### Daily variant

The above described example presents the intraday variant. In case of daily trading, the `SimulatedExecutionHandler` does not
subscribe to `IntradayBarEvent`. It is only subscribed to `MarketOpenEvent`, `MarketCloseEvent`, `AfterMarketCloseEvent`
and the `ScheduleOrderExecutionEvent`. The Portfolio in this case is updated only on the `AfterMarketCloseEvent`.
