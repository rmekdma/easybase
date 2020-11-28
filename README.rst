EasyBase
========

.. image:: https://travis-ci.com/wgzhao/easybase.svg?branch=master
    :target: https://travis-ci.com/wgzhao/easybase

.. image:: https://img.shields.io/codecov/c/github/wgzhao/easybase.svg
    :target: https://codecov.io/gh/wgzhao/easybase

.. image:: https://img.shields.io/pypi/dm/easybase.svg
    :target: https://pypi.org/project/easybase/

.. image:: https://img.shields.io/pypi/v/easybase.svg
    :target: https://pypi.org/project/easybase/

.. image:: https://img.shields.io/pypi/pyversions/easybase.svg
    :target: https://pypi.org/project/easybase/

.. image:: https://img.shields.io/pypi/implementation/easybase.svg
    :target: https://pypi.org/project/easybase/


**EasyBase** is a developer-friendly Python library to interact with
`Apache HBase <https://hbase.apache.org>`__ . The orignal source code
forked from `HappyBase <https://github.com/wbolster/happybase>`__.


Feature highlight
=================

-  easy using

-  support HBase Thrift 2 protocol

-  using `thriftpy2 <http://github.com/thriftpy/thriftpy2>`__ instead of
   old thriftpy


Installation
============

.. code:: shell

   pip install easybase


Usage
=====


Connect
-------

.. code:: python

   import easybase
   host, port = 'localhost', 9000
   tbl = 'test1'
   conn = easybase.connect(host=host, port=port)
   table = conn.table(tbl)
   rs = conn.scan(limit=10)
   for row in rs:
     print(row)


Create Table
------------

.. code:: python

   table_def = {'cf1':dict(),
                'cf2':{'max_versions':2000}}
   conn.create_table('test1', table_def)


Write row to table
------------------

.. code:: python

   puts = {'cf1:c1': 'v1',
           'cf1:c2': 'v2'
          'cf2:c2': 'v3'}
   tbl = conn.table('test1')
   tbl.put(row='rk1', puts)


Get row from table
------------------

.. code:: python

   rk = 'rk1'
   tbl = conn.table('test1')
   rs = tbl.row(rk)


Scan rows 
----------

.. code:: python

   tbl = conn.table('test1')
   scanner = tbl.scan(row_start='rk_0001', row_stop='rk_0100')
   for row in scanner:
     print(row)

You can get detail in
`DemoClient.py <https://github.com/wgzhao/easybase/blob/master/DemoClient.py>`__


License
=================
MIT License   `<http://www.opensource.org/licenses/MIT>`_. 