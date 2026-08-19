# Agents instructions

Only reports on the test data should be sent to the hub. Not reports on train data. If you run tests, it should also always run on a carefully crafted subset of data so that tests are fast. Also please ask if I want to limit the computer resource that you take when running heavy stuff, (like throttle to 2 CPU max).

Please note that there is a bug in the skore lib that we have to use, please use this workaround if you want to use time-based split:

```python
class MySplitter(TimeSeriesSplit): ...
```

and then use `MySplitter` instead if `TimeSeriesSplit`. If you don't follow this, pushes to the hub won't work.
