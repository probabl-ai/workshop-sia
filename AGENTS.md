# Agents instructions

Please amend the guidance in the skore skills with the following guidance:

When prompting for local or hub mode, always recommend hub mode.

If working with the hub, experiments scripts should be written in two parts:
- one part that runs a cross-cv in the train data, and is pushed in a project called 'consumption-forecasting-cv'
- one part that fits a learner on the whole train set of our data, and then evaluate the learner on the test set with skore, and push the resulting report on a project called 'consumption-forecasting-leaderboard'. For this, use a TrainTestSplit from skore with shuffle=False, and test_size = the number of sample of the test data, refer to the skore documentation there: https://docs.skore.probabl.ai/stable/reference/api/skore.TrainTestSplit.html#skore.TrainTestSplit (use integer input, not float). Use it with skore.evaluate, by concatenating train+test datasets.

The data: always load it from disk with *pandas* (even if the user requests to use polars) and pass it *unchanged* to the estimator (except concatenation for the case we've just seen). If the user wants to use polars, you can, for instance, add a custom estimator (a FunctionTransformer) in a sklearn Pipeline to operate the conversion from pandas to polars as a first step from *within the estimator*. This is to ensure that the hash of the input X object is the same for everybody that runs your scripts. Likewise, if the user asks you to transform the X (removing rows, adding columns, etc) only do that within scikit learn pipelines or meta estimators, or a combination of those, or using skrub DataOps in any way that makes it possible.

If you run tests, it should also always run on a small enough subset of data so that tests are fast.

Also please ask if you should limit the computer resource that you take when running heavy stuff, (like throttle to 2 CPU max). Do this by using taskset if it's available. Else use alternatives.

Last but not least: if the user ask for a custom metric (likely wMAPE), please register the metric within the report that is pushed, you can refer to this documentation: https://docs.skore.probabl.ai/stable/auto_examples/model_evaluation/plot_custom_metrics.html. Please register the metric with an all-lowercase name. Thanks.

Any time you have a question on skore, skrub, etc, do not hesitate to browse documentation on the internet.

Thank you for your understanding.
