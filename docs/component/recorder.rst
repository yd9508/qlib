.. _recorder:

====================================
Qlib Recorder: Experiment Management
====================================
.. currentmodule:: qlib

Introduction
===================
``Qlib`` contains an experiment management system named ``QlibRecorder``, which is designed to help users handle experiment and analyse results in an efficient way. 

There are three components of the system:

- `ExperimentManager`
    a class that manages experiments.

- `Experiment`
    a class of experiment, and each instance of it is responsible for a single experiment.

- `Recorder`
    a class of recorder, and each instance of it is responsible for a single run.

Here is a general view of the structure of the system:

.. code-block::

    ExperimentManager
        - Experiment 1
            - Recorder 1
            - Recorder 2
            - ...
        - Experiment 2
            - Recorder 1
            - Recorder 2
            - ...
        - ...
This experiment management system defines a set of interface and provided a concrete implementation based on the machine learning platform: ``MLFlow`` (`link <https://mlflow.org/>`_). 


Qlib Recorder
===================
``QlibRecorder`` provides a high level API for users to use the experiment management system. The interfaces are wrapped in the variable ``R`` in ``Qlib``, and users can directly use ``R`` to interact with the system. The following command shows how to import ``R`` in Python:

.. code-block:: Python

        from qlib.workflow import R

``QlibRecorder`` includes several common API for managing `experiments` and `recorders` within a workflow. For more available APIs, please refer to the following section about `Experiment Manager`, `Experiment` and `Recorder`.

Here are the available interfaces of ``QlibRecorder``:

.. autoclass:: qlib.workflow.__init__.QlibRecorder
    :members:

Experiment Manager
===================

The ``ExpManager`` module in ``Qlib`` is responsible for managing different experiments. Most of the APIs of ``ExpManager`` are similar to ``QlibRecorder``, and the most important API will be the ``get_exp`` method. User can directly refer to the documents above for some detailed information about how to use the ``get_exp`` method.

.. autoclass:: qlib.workflow.expm.ExpManager
    :members: get_exp, list_experiments

For other interfaces such as `create_exp`, `delete_exp`, please refer to `Experiment Manager API <../reference/api.html#experiment-manager>`_.

Experiment
===================

The ``Experiment`` class is solely responsible for a single experiment, and it will handle any operations that are related to an experiment. Basic methods such as `start`, `end` an experiment are included. Besides, methods related to `recorders` are also available: such methods include `get_recorder` and `list_recorders`.

.. autoclass:: qlib.workflow.exp.Experiment
    :members: get_recorder, list_recorders

For other interfaces such as `search_records`, `delete_recorder`, please refer to `Experiment API <../reference/api.html#experiment>`_.

``Qlib`` also provides a default ``Experiment``, which will be created and used under certain situations when users use the APIs such as `log_metrics` or `get_exp`. If the default ``Experiment`` is used, there will be related logged information when running ``Qlib``. Users are able to change the name of the default ``Experiment`` in the config file of ``Qlib`` or during ``Qlib``'s `initialization <../start/initialization.html#parameters>`_, which is set to be '`Experiment`'.

Recorder
===================

The ``Recorder`` class is responsible for a single recorder. It will handle some detailed operations such as ``log_metrics``, ``log_params`` of a single run. It is designed to help user to easily track results and things being generated during a run.

Here are some important APIs that are not included in the ``QlibRecorder``:

.. autoclass:: qlib.workflow.recorder.Recorder
    :members: list_artifacts, list_metrics, list_params, list_tags

For other interfaces such as `save_objects`, `load_object`, please refer to `Recorder API <../reference/api.html#recorder>`_.

Record Template
===================

The ``RecordTemp`` class is a class that enables generate experiment results such as IC and backtest in a certain format. We have provided three different `Record Template` class:

- ``SignalRecord``: This class generates the `prediction` results of the model.
- ``SigAnaRecord``: This class generates the `IC`, `ICIR`, `Rank IC` and `Rank ICIR` of the model.
- ``PortAnaRecord``: This class generates the results of `backtest`. The detailed information about `backtest` as well as the available `strategy`, users can refer to `Strategy <../component/strategy.html>`_ and `Backtest <../component/backtest.html>`_.

For more information about the APIs, please refer to `Record Template API <../reference/api.html#module-qlib.workflow.record_temp>`_.
