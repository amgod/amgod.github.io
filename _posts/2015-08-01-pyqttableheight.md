---
title: 设置PYQT中table的行高和列宽
date: 2015-08-01 21:12
status: public
thread: 0
categories: 日志
tags: pyqt
---

#### 1、指定某个行或者列的大小
```python
self.MyTable.setColumnWidth(2,50)  #将第2列的单元格，设置成50宽度
self.MyTable.setRowHeight(2,60)   #将第2行的单元格，设置成60的高度
```
#### 2、将行和列的大小设为与内容相匹配
```python
self.MyTable.resizeColumnsToContents()   #将列调整到跟内容大小相匹配
self.MyTable.resizeRowsToContents()   #将行大小调整到跟内容的大小相匹配
```
#### 3、设置所有行和列为固定值
```python
self.tableWidget.horizontalHeader().setDefaultSectionSize(80)  #设置所有列宽为80
self.tableWidget.verticalHeader().setDefaultSectionSize(21)   #设置所有行高为21
```
