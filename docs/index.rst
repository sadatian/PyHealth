.. PyHealth documentation master file, created by
   sphinx-quickstart on Wed Aug  5 21:17:59 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to PyHealth's documentation!
====================================


**Deployment & Documentation & Stats**

.. image:: https://img.shields.io/pypi/v/pyhealth.svg?color=brightgreen
   :target: https://pypi.org/project/pyhealth/
   :alt: PyPI version


.. image:: https://readthedocs.org/projects/pyhealth/badge/?version=latest
   :target: https://pyhealth.readthedocs.io/en/latest/?badge=latest
   :alt: Documentation status


.. image:: https://mybinder.org/badge_logo.svg
   :target: https://mybinder.org/v2/gh/yzhao062/pyhealth/master
   :alt: MyBinder


.. image:: https://img.shields.io/github/stars/yzhao062/pyhealth.svg
   :target: https://github.com/yzhao062/pyhealth/stargazers
   :alt: GitHub stars


.. image:: https://img.shields.io/github/forks/yzhao062/pyhealth.svg?color=blue
   :target: https://github.com/yzhao062/pyhealth/network
   :alt: GitHub forks


.. image:: https://pepy.tech/badge/pyhealth
   :target: https://pepy.tech/project/pyhealth
   :alt: Downloads


.. image:: https://pepy.tech/badge/pyhealth/month
   :target: https://pepy.tech/project/pyhealth
   :alt: Downloads


-----


**Build Status & Coverage & Maintainability & License**

.. image:: https://travis-ci.org/yzhao062/pyhealth.svg?branch=master
   :target: https://travis-ci.org/yzhao062/pyhealth
   :alt: Build Status


.. image:: https://circleci.com/gh/yzhao062/PyHealth.svg?style=svg
   :target: https://circleci.com/gh/yzhao062/PyHealth
   :alt: Circle CI


.. image:: https://ci.appveyor.com/api/projects/status/1kupdy87etks5n3r/branch/master?svg=true
   :target: https://ci.appveyor.com/project/yzhao062/pyhealth/branch/master
   :alt: Build status


.. image:: https://api.codeclimate.com/v1/badges/bdc3d8d0454274c753c4/maintainability
   :target: https://codeclimate.com/github/yzhao062/pyhealth/maintainability
   :alt: Maintainability


.. image:: https://img.shields.io/github/license/yzhao062/pyhealth
   :target: https://github.com/yzhao062/pyhealth/blob/master/LICENSE
   :alt: License


-----


.. image:: https://raw.githubusercontent.com/yzhao062/PyHealth/master/docs/images/logo.png
   :target: https://raw.githubusercontent.com/yzhao062/PyHealth/master/docs/images/logo.png
   :alt: PyHealth Logo
   :align: center


**PyHealth** is a comprehensive **Python package** for **healthcare AI**, designed for both **ML researchers** and **healthcare and medical practitioners**.
**PyHealth** accepts diverse healthcare data such as longitudinal electronic health records (EHRs), continuous signials (ECG, EEG), and clinical notes (to be added), and supports various predictive modeling methods using deep learning and other advanced machine learning algorithms published in the literature.

The library is proudly developed and maintained by researchers from `Carnegie Mellon University <https://www.cmu.edu/>`_, `IQVIA <https://www.iqvia.com/>`_, and `University of Illinois at Urbana-Champaign <https://illinois.edu/>`_.
PyHealth makes many important healthcare tasks become accessible, such as **phenotyping prediction**, **mortality prediction**,
and **ICU length stay forecasting**, etc. Running these prediction tasks with deep learning models can be as short as 10 lines of code in PyHealth.


**PyHealth comes with three major modules**: (i) *data preprocessing module*; (ii) *learning module*
and (iii) *evaluation module*. Typically, one can run the data prep module to prepare the data, then feed to the learning module for prediction, and finally assess
the result with the evaluation module.
Users can use the full system as mentioned or just selected modules based on the own need:

* **Deep learning researchers** may directly use the processed data along with the proposed new models.
* **Medical personnel**, may leverage our data preprocessing module to convert the medical data to the format that learning models could digest, and then perform the inference tasks to get insights from the data.


PyHealth is featured for:

* **Unified APIs, detailed documentation, and interactive examples** across various types of datasets and algorithms.
* **Advanced models**\ , including **latest deep learning models** and **classical machine learning models**.
* **Wide coverage**, supporting **sequence data**, **image data**, **series data** and **text data** like clinical notes.
* **Optimized performance with JIT and parallelization** when possible, using `numba <https://github.com/numba/numba>`_ and `joblib <https://github.com/joblib/joblib>`_.
* **Customizable modules and flexible design**: each module may be turned on/off or totally replaced by custom functions. The trained models can be easily exported and reloaded for fast execution and deployment.


**API Demo for LSTM on Phenotyping Prediction with GPU**\ :


   .. code-block:: python


       # load pre-processed CMS dataset
       from pyhealth.data.expdata_generator import sequencedata as expdata_generator

       expdata_id = '2020.0810.data.mortality.mimic'
       cur_dataset = expdata_generator(exp_id=exp_id)
       cur_dataset.get_exp_data(sel_task='mortality', )
       cur_dataset.load_exp_data()

       # initialize the model for training
       from pyhealth.models.sequence.lstm import LSTM
       # enable GPU
       expmodel_id = 'test.model.lstm.0001'
       clf = LSTM(expmodel_id=expmodel_id, n_batchsize=20, use_gpu=True, n_epoch=100)
       clf.fit(cur_dataset.train, cur_dataset.valid)

       # load the best model for inference
       clf.load_model()
       clf.inference(cur_dataset.test)
       pred_results = clf.get_results()

       # evaluate the model
       from pyhealth.evaluation.evaluator import func
       r = func(pred_results['hat_y'], pred_results['y'])
       print(r)



**Citing PyHealth**\ :

`PyHealth paper <https://arxiv.org/abs/2101.04209>`_ is under review at
`JMLR <http://www.jmlr.org/>`_ (machine learning open-source software track).
If you use PyHealth in a scientific publication, we would appreciate
citations to the following paper::

    @article{zhao2021pyhealth,
      title={PyHealth: A Python Library for Health Predictive Models},
      author={Zhao, Yue and Qiao, Zhi and Xiao, Cao and Glass, Lucas and Sun, Jimeng},
      journal={arXiv preprint arXiv:2101.04209},
      year={2021}
    }

or::

    Zhao, Y., Qiao, Z., Xiao, C., Glass, L. and Sun, J., 2021. PyHealth: A Python Library for Health Predictive Models. arXiv preprint arXiv:2101.04209.


**Key Links and Resources**\ :


* `View the latest codes on Github <https://github.com/yzhao062/pyhealth>`_
* `Execute Interactive Jupyter Notebooks <https://mybinder.org/v2/gh/yzhao062/pyhealth/master>`_
* `Check out the PyHealth paper <https://github.com/yzhao062/pyhealth>`_



----


Preprocessed Datasets & Implemented Algorithms
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**(i) Preprocessed Datasets** (customized data preprocessing function is provided in the example folders):

====================  ================  ======================================================================================================    ======================================================    ===============================================================================================================
Type                  Abbr              Description                                                                                               Processed Function                                        Link
====================  ================  ======================================================================================================    ======================================================    ===============================================================================================================
Sequence: EHR-ICU     MIMIC III         A relational database containing tables of data relating to patients who stayed within ICU.               \\examples\\data_generation\\dataloader_mimic             https://mimic.physionet.org/gettingstarted/overview/
Sequence: EHR-ICU     MIMIC_demo        The MIMIC-III demo database is limited to 100 patients and excludes the noteevents table.                 \\examples\\data_generation\\dataloader_mimic_demo        https://mimic.physionet.org/gettingstarted/demo/
Sequence: EHU-Claim   CMS               DE-SynPUF: CMS 2008-2010 Data Entrepreneurs Synthetic Public Use File                                     \\examples\\data_generation\\dataloader_cms               https://www.cms.gov/Research-Statistics-Data-and-Systems/Downloadable-Public-Use-Files/SynPUFs
Image: Chest X-ray    Pediatric         Pediatric Chest X-ray Pneumonia (Bacterial vs Viral vs Normal) Dataset                                    N/A                                                       https://academictorrents.com/details/951f829a8eeb4d2839c4a535db95078a9175010b
Series: ECG           PhysioNet         AF Classification from a short single lead ECG recording Dataset.                                         N/A                                                       https://archive.physionet.org/challenge/2017/#challenge-data
====================  ================  ======================================================================================================    ======================================================    ===============================================================================================================

You may download the above datasets at the links. The structure of the generated datasets can be found in datasets folder:

* \\datasets\\cms\\x_data\\...csv
* \\datasets\\cms\\y_data\\phenotyping.csv
* \\datasets\\cms\\y_data\\mortality.csv


The processed datasets (X,y) should be put in x_data, y_data correspondingly, to be appropriately digested by deep learning models. We include some sample datasets under \\datasets folder.


**(ii) Machine Learning and Deep Learning Models** :


**For sequence data**:

===================  ================  ============================================================  ======================================================================================================  =====  ========================================
Type                 Abbr              Class                                                         Algorithm                                                                                               Year   Ref
===================  ================  ============================================================  ======================================================================================================  =====  ========================================
Classical Models     RandomForest      :class:`pyhealth.models.sequence.rf.RandomForest`             Random forests                                                                                          2000   :cite:`a-breiman2001random`
Classical Models     XGBoost           :class:`pyhealth.models.sequence.xgboost.XGBoost`             XGBoost: A scalable tree boosting system                                                                2016   [#Chen2016Xgboost]_
Neural Networks      LSTM              :class:`pyhealth.models.sequence.lstm.LSTM`                   Long short-term memory                                                                                  1997   [#Hochreiter1997Long]_
Neural Networks      GRU               :class:`pyhealth.models.sequence.gru.GRU`                     Gated recurrent unit                                                                                    2014   [#Cho2014Learning]_
Neural Networks      RETAIN            :class:`pyhealth.models.sequence.retain.RetainAttention`      RETAIN: An Interpretable Predictive Model for Healthcare using Reverse Time Attention Mechanism         2016   [#Choi2016RETAIN]_
Neural Networks      Dipole            :class:`pyhealth.models.sequence.dipole.Dipole`               Dipole: Diagnosis Prediction in Healthcare via Attention-based Bidirectional Recurrent Neural Networks  2017   [#Ma2017Dipole]_
Neural Networks      tLSTM             :class:`pyhealth.models.sequence.tlstm.tLSTM`                 Patient Subtyping via Time-Aware LSTM Networks                                                          2017   [#Baytas2017tLSTM]_
Neural Networks      RAIM              :class:`pyhealth.models.sequence.raim.RAIM`                   RAIM: Recurrent Attentive and Intensive Model of Multimodal Patient Monitoring Data                     2018   [#Xu2018RAIM]_
Neural Networks      StageNet          :class:`pyhealth.models.sequence.stagenet.StageNet`           StageNet: Stage-Aware Neural Networks for Health Risk Prediction                                        2020   [#Gao2020StageNet]_
===================  ================  ============================================================  ======================================================================================================  =====  ========================================


**For image data**:

===================  ================  =================================================================================  ======================================================================================================  =====  ========================================
Type                 Abbr              Class                                                                              Algorithm                                                                                               Year   Ref
===================  ================  =================================================================================  ======================================================================================================  =====  ========================================
Neural Networks      CNN               :class:`pyhealth.models.sequence.basiccnn.BasicCNN`                                Face recognition: A convolutional neural-network approach                                               1997   :cite:`a-lawrence1997face`
Neural Networks      Vggnet            :class:`pyhealth.models.sequence.typicalcnn.TypicalCNN`                            Very deep convolutional networks for large-scale image recognition                                      2014Neural Networks      Inception         pyhealth.models.sequence.typicalcnn       Rethinking the Inception Architecture for Computer Vision
Neural Networks      Resnet            pyhealth.models.sequence.typicalcnn                                                Deep Residual Learning for Image Recognition
Neural Networks      Resnext           pyhealth.models.sequence.typicalcnn                                                Aggregated Residual Transformations for Deep Neural Networks
Neural Networks      Densenet          pyhealth.models.sequence.typicalcnn                                                Densely Connected Convolutional Networks
Neural Networks      Mobilenet         pyhealth.models.sequence.typicalcnn                                                MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications
===================  ================  =================================================================================  ======================================================================================================  =====  ========================================


**For ecg/egg data**:

===================  ================  ========================================  ========================================================================================================  =====  ========================================
Type                 Abbr              Class                                     Algorithm                                                                                                 Year   Ref
===================  ================  ========================================  ========================================================================================================  =====  ========================================
Classical Models     RandomForest      pyhealth.models.ecg.rf                    Random Forests                                                                                            2000   [#Breiman2001Random]_
Classical Models     XGBoost           pyhealth.models.ecg.xgboost               XGBoost: A scalable tree boosting system                                                                  2016   [#Chen2016Xgboost]_
Neural Networks      BasicCNN1D        pyhealth.models.ecg.conv1d                Face recognition: A convolutional neural-network approach                                                 1997   [#Lawrence1997Face]_
Neural Networks      DBLSTM-WS         pyhealth.models.ecg.dblstm_ws             A novel wavelet sequence based on deep bidirectional LSTM network model for ECG signal classification     2018
Neural Networks      DeepRes1D         pyhealth.models.ecg.deepres1d             Heartbeat classification using deep residual convolutional neural network from 2-lead electrocardiogram   2019
Neural Networks      AE+BiLSTM         pyhealth.models.ecg.sdaelstm              Automatic Classification of CAD ECG Signals With SDAE and Bidirectional Long Short-Term Network           2019
Neural Networks      KRCRnet           pyhealth.models.ecg.rcrnet                K-margin-based Residual-Convolution-Recurrent Neural Network for Atrial Fibrillation Detection            2019
Neural Networks      MINA              pyhealth.models.ecg.mina                  MINA: Multilevel Knowledge-Guided Attention for Modeling Electrocardiography Signals                      2019
===================  ================  ========================================  ========================================================================================================  =====  ========================================


Examples of running ML and DL models can be found below, or directly at \\examples\\learning_examples\\


**(iii) Evaluation Metrics** :

=======================  =======================  ======================================================================================================  ===============================================
Type                     Abbr                     Metric                                                                                                  Method
=======================  =======================  ======================================================================================================  ===============================================
Binary Classification    average_precision_score  Compute micro/macro average precision (AP) from prediction scores                                       pyhealth.evaluation.xxx.get_avg_results
Binary Classification    roc_auc_score            Compute micro/macro ROC AUC score from prediction scores                                                pyhealth.evaluation.xxx.get_avg_results
Binary Classification    recall, precision, f1    Get recall, precision, and f1 values                                                                    pyhealth.evaluation.xxx.get_predict_results
Multi Classification     To be done here
=======================  =======================  ======================================================================================================  ===============================================


**(iv) Supported Tasks**:

=======================  =======================  ======================================================================================================  =========================================================
Type                     Abbr                     Description                                                                                             Method
=======================  =======================  ======================================================================================================  =========================================================
Multi-classification     phenotyping              Predict the diagnosis code of a patient based on other information, e.g., procedures                    \\examples\\data_generation\\generate_phenotyping_xxx.py
Binary Classification    mortality prediction     Predict whether a patient may pass away during the hospital                                             \\examples\\data_generation\\generate_mortality_xxx.py
Regression               ICU stay length pred     Forecast the length of an ICU stay                                                                      \\examples\\data_generation\\generate_icu_length_xxx.py
=======================  =======================  ======================================================================================================  =========================================================




Algorithm Benchmark
^^^^^^^^^^^^^^^^^^^

**The comparison among of implemented models** will be made available later
with a benchmark paper. TBA soon :)



----


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Getting Started

   install
   example


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Documentation

   api_cc
   api


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Additional Information

   about
   faq
   whats_new


----


.. rubric:: References

.. bibliography:: references.bib
   :cited:
   :labelprefix: A
   :keyprefix: a-



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
