## changed version by schwt
- new makefile configure, suitable for my spark context. (done by Sean.Zhong)
- new predict function (`def my_predict()`), which easy to evaluate.
##### notes:
1. added new function `my_predict()` from premal `predict()` in version: java, scala, spark.scala
2. tocheck: in java version, DMatrix.getLabel(), keep order?

<img src=https://raw.githubusercontent.com/dmlc/dmlc.github.io/master/img/logo-m/xgboost.png width=135/>  eXtreme Gradient Boosting
===========
[![Build Status](https://travis-ci.org/dmlc/xgboost.svg?branch=master)](https://travis-ci.org/dmlc/xgboost)
[![Build Status](https://ci.appveyor.com/api/projects/status/5ypa8vaed6kpmli8?svg=true)](https://ci.appveyor.com/project/tqchen/xgboost)
[![Documentation Status](https://readthedocs.org/projects/xgboost/badge/?version=latest)](https://xgboost.readthedocs.org)
[![GitHub license](http://dmlc.github.io/img/apache2.svg)](./LICENSE)
[![CRAN Status Badge](http://www.r-pkg.org/badges/version/xgboost)](http://cran.r-project.org/web/packages/xgboost)
[![PyPI version](https://badge.fury.io/py/xgboost.svg)](https://pypi.python.org/pypi/xgboost/)
[![Gitter chat for developers at https://gitter.im/dmlc/xgboost](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dmlc/xgboost?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[Documentation](https://xgboost.readthedocs.org) |
[Resources](demo/README.md) |
[Installation](https://xgboost.readthedocs.org/en/latest/build.html) |
[Release Notes](NEWS.md) |
[RoadMap](https://github.com/dmlc/xgboost/issues/873)

NOTES on the build
==========
1. git clone --recursive https://github.com/dmlc/xgboost.git
2. Make sure the gcc version >= 4.8. Make sure g++/gcc can be found on PATH env. Make sure the GCC library can be found in runtime.
   ```
   export LD_LIBRARY_PATH=${YOUR_GCC_DIRECTORY}/lib64
   ```
3. Make sure you use a new verion of ld. I use binutils version 2.2.8. Make sure ld can be found on PATH env.
4. Make sure the cmake version > 3.2. Make sure cmake can be found on PATH env. 
5. export JAVA_HOME=/path/to/your/jdk
6. To enable HDFS support, please modify jvm-packages/create_jni.py. ```"USE_HDFS": "ON"```
   libhdfs.a is not compiled with -fPIC flag, which will cause building problems. 
   We need to recompile libhdfs.a with -fPIC support by following link https://github.com/dmlc/dmlc-core/issues/10#issuecomment-202246423
   I have compiled a new libhdfs.a for CDH 5.3.2.
   ```
   export HADOOP_HOME=${YOUR_XGBOOST_SRC_DIR}/hadoop-hdfs-2.5.0-cdh5.3.2
   ```
7. Make the build
   ```
   make clean
   make -j4
   cd jvm-packages
   mvn clean
   mvn package
   ```    
8. The build has been verified with gcc 4.8.2, cmake 3.8.2 on a CentOS 6.6 machine.
   
XGBoost
===========
XGBoost is an optimized distributed gradient boosting library designed to be highly ***efficient***, ***flexible*** and ***portable***.
It implements machine learning algorithms under the [Gradient Boosting](https://en.wikipedia.org/wiki/Gradient_boosting) framework.
XGBoost provides a parallel tree boosting (also known as GBDT, GBM) that solve many data science problems in a fast and accurate way.
The same code runs on major distributed environment (Hadoop, SGE, MPI) and can solve problems beyond billions of examples.

What's New
----------
* [XGBoost GPU support with fast histogram algorithm](https://github.com/dmlc/xgboost/tree/master/plugin/updater_gpu)
* [XGBoost4J: Portable Distributed XGboost in Spark, Flink and Dataflow](http://dmlc.ml/2016/03/14/xgboost4j-portable-distributed-xgboost-in-spark-flink-and-dataflow.html), see [JVM-Package](https://github.com/dmlc/xgboost/tree/master/jvm-packages)
* [Story and Lessons Behind the Evolution of XGBoost](http://homes.cs.washington.edu/~tqchen/2016/03/10/story-and-lessons-behind-the-evolution-of-xgboost.html)
* [Tutorial: Distributed XGBoost on AWS with YARN](https://xgboost.readthedocs.io/en/latest/tutorials/aws_yarn.html)
* [XGBoost brick](NEWS.md) Release

Ask a Question
--------------
* For reporting bugs please use the [xgboost/issues](https://github.com/dmlc/xgboost/issues) page.
* For generic questions or to share your experience using XGBoost please use the [XGBoost User Group](https://groups.google.com/forum/#!forum/xgboost-user/)

Help to Make XGBoost Better
---------------------------
XGBoost has been developed and used by a group of active community members. Your help is very valuable to make the package better for everyone.
- Check out [call for contributions](https://github.com/dmlc/xgboost/issues?q=is%3Aissue+label%3Acall-for-contribution+is%3Aopen) and [Roadmap](https://github.com/dmlc/xgboost/issues/873) to see what can be improved, or open an issue if you want something.
- Contribute to the [documents and examples](https://github.com/dmlc/xgboost/blob/master/doc/) to share your experience with other users.
- Add your stories and experience to [Awesome XGBoost](demo/README.md).
- Please add your name to [CONTRIBUTORS.md](CONTRIBUTORS.md) and after your patch has been merged.
  - Please also update [NEWS.md](NEWS.md) on changes and improvements in API and docs.

License
-------
© Contributors, 2016. Licensed under an [Apache-2](https://github.com/dmlc/xgboost/blob/master/LICENSE) license.

Reference
---------
- Tianqi Chen and Carlos Guestrin. [XGBoost: A Scalable Tree Boosting System](http://arxiv.org/abs/1603.02754). In 22nd SIGKDD Conference on Knowledge Discovery and Data Mining, 2016 
- XGBoost originates from research project at University of Washington, see also the [Project Page at UW](http://dmlc.cs.washington.edu/xgboost.html).
