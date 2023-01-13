---
title: PyQT使用教程
date: 2015-09-08 20:27
status: public
thread: 0
categories: 日志
tags: pyqt
---
**PyQt4 QListWidget 使用教程**
listWidget = QListWidget() #实例化一个(item base)的列表
listWidget.addItem('dd') #添加一个项
listWidget.addItems([]) # 从序列中添加子项
listWidget.setDragEnabled(True) #设置拖拉
listWidget.sortItems() #排序
listWidget.selectAll()#全选
listWidget.setSortingEnabled(bool) #设置自动排序
listWidget.setSelectionMode(QtGui.QAbstractItemView.ExtendedSelection) #设置选择模式
选择模式有:ExtendedSelection 按住ctrl多选, SingleSelection 单选 MultiSelection 点击多选 ContiguousSelection 鼠标拖拉多选
listWidget.setCurrentRow(0) #设置当前选择行 默认为-1
listWidget.count() #得到子项总数
listWidget.item(row).text() #得到第row行的内容listWidget.item(row)返回一个item 对象
listWidget.takeItem(row) #返回row行的所在的item对象，可以用在insertItem()中
listWidget.insertItem(2,item) #在第二行插入一项item可谓为一个listviewitem对象或者string
listWidget.setCurrentItem('dd') #设置'dd'为当前项
listWidget.selectedItems() #返回一个包含item对象 的list 对象
**修改item 的内容**
item.setText('dsds') # 设置item的内容为dsds item为对象,可从listWidget.item(row) takeItem(row) 得到
**PyQt4 QAction()使用教程**
exit=QtGui.QAction(QtGui.QIcon('pix/Moon.bmp'),'Exit',self) #创建一个action "exti"为title self 为parent
exit.setSeparator(bool)#设置设置该action为分离器 也就是分隔符？ 当为true时 QIcon会无效
exit.setShortcut('Ctrl+Q') #设置快捷键
也可以 exit.setShortcut(QKeySequence.New) # QKeySequence 保护标准的快捷按钮 QKeySequence.Paste
exit.setStatusTip('Exit Application') #设置状态栏说明
exit.setToolTip("exit") #设置tip
exit.setText("sdf") #设置title
exit.setWhatsThis("string") #设置what's this
当checked状态发生改变时,发出toggled(bool) 信号
当点击 触发状态发生变化时,发出triggered(bool)信号
self.connect(exit,QtCore.SIGNAL('triggered()'),QtCore.SLOT('close()')) #设置信号、插槽
**创建的action 可以使用在 menubar toolbar**
fileMenu = QMenuBar().addMenu(tr("&Exit"));
fileMenu.addAction(exit);
fileToolBar = addToolBar(tr("Exit"));
fileToolBar.addAction(exit);
self.label_img.setContextMenuPolicy(Qt.ActionsContextMenu) #设置右键菜单,添加action为右键菜单
因为创建一个QAction 需要6行代码左右,如果一个窗口有几个QAction的话 会很繁琐 所以我们可以定义一个方法 这个可以简单点
```python
def createAction(self,text,slot=None,shortcut=None,icon=None,tip=None,checkable=False,signal="triggered()"):
     action=QAction(text,self)
     if icon is not None:
        action.setIcon(QIcon("im.png"))
      if shortcut is not None:
        action.setShortcut(shortcut)
       if tip is not None:
        acton.setToolTip(tip)
        action.setStatusTip(tip)
      if slot is not None:
         self.connect(action,SIGNAL(signal),slot)
      if checkable:
         action.setCheckable(checkable)
return action
```
**PyQt4 QSettings 使用教程**
setting=QSettings()
setting.setValue("lab",QVariant(50)) #设置一个lab键的值
setting.value("lab")
为了使QSettings()起作用 在程序运行段 也就是app=QApplication() 以后加上以下一行 app.setOrganizationName("ds")
**PyQt4 QDockWidget 使用教程**
在pyqt4 中 dock 是一个镶嵌在主窗口而又能拉出来成立一个独立窗口的控件 ,dock是QDockWidget 的对象
dock=QDockWidget('title',self) #实例化一个dock title为标题self为parent 因为QDockWidget不添加到布局管理器中,所以我们需要传一个parent 给他
dock.setObjectName("dock") #设置dock的对象名称
dock.setAllowedAreas(Qt.LeftDockWidgetArea |Qt.RightDockWidgetArea) #设置dock只能在左边 或者右边显示
allowedareas 有Qt.LeftDockWidgetArea Qt.RightDockWidgetArea Qt.TopDockWidgetArea Qt.BottomDockWidgetArea Qt.AllDockWidgetAreas
dock.setWidget(QLabel) #添加一个label控件
dock.setFeatures(QDockWidget.NoDockWidgetFeatures) #设置dock是否可以关闭 拉出等
参数还有 QDockWidget.DockWidgetClosable 可以关闭 DockWidgetMovable 可以移动
DockWidgetFloatable #可以独立出来 DockWidgetVerticalTitleBar 垂直显示标题 AllDockWidgetFeatures 除垂直标题以外 以上所有 NoDockWidgetFeatures
self.addDockWidget(Qt.RightDockWidget,dock) 添加dock到主窗口 第一个参数为显示位置
**PyQt4 QCheckBox 使用教程**
setChecked(bool) #设置是否选择
isChecked() #返回bool
发出toggled(bool)信号
 **PyQt4 QTableWidget 使用教程**
self.table=QTableWidget() #实例化
self.table.setColumnCount(4) #设置列数
self.table.setRowCount(6) #设置行数
self.table.setWhatsThis("mantou") ###
self.table.setEditTriggers(QTableWidget.NoEditTriggers) #设置为不能编辑单元格
   #set Column tab title
self.table.setHorizontalHeaderLabels(list(range(5,10)))
self.table.setVerticalHeaderLabels(["a","d"] ) #设置 行title
self.table.setAlternatingRowColors(bool) #设置交替行颜色
```python
for i in range(0,5):
    for x in range(0,7):
        item=QTableWidgetItem(str(i+x))# 实例一个item对象
        item.setTextAlignment(Qt.AlignLeft |Qt.AlignCenter) #设置对齐方式
        item.setBackgroundColor(Qt.green) #设置背景
        self.table.setItem(x,i,item) #添加Item
```
**PyQt4 QInputDialog 使用教程**
string, ok = QInputDialog.getText(self, '标题', '说明文字') #   显示一个标题为标题 说明文字为说明问题的输入对话框！string 为输入的内容 ok 为点击的按钮
```python
if ok and not string.isEmpty(): #如果点击了确定   输入了内容
      pass
```
**PyQt4 QPushButton 使用教程**
button = QPushButton('***') # 实例化一个text为***)的按钮
button.setFocusPolicy() #设置焦点样式 样式有:Qt.NoFocus: 无焦点,Qt.TabFocus:用tab切换焦点,Qt.ClickFocus:点击切换焦点,Qt.StrongFocus:貌似跟click一样 Qt.WheelFocus
button.setCheckable(True) #设置为开关按钮 toggle 就是按下按钮不会弹起
button.isChecked() 返回bool值 只有setCheckable()为true时有效
button.setShortcut('Ctrl+F') #设置快捷方式
**PyQt4 QMessageBox() 使用教程**
message=QtGui.QMessageBox.question(self,u'提示:',u'你确认要退出？',QtGui.QMessageBox.Yes,QtGui.QMessageBox.No,QtGui.QMessageBox.Cancel|QMessageBox::Escape) #弹出对话框 QMessageBox.question ,QMessageBox.warning 为类型
```python
if message ==QtGui.QMessageBox.Yes:
   event.accept()
else:
    event.ignore()       
message=QtGui.QMessageBox.warning(parent,"title",u"message")
```
**PyQt4 QFont QPixmap QIcon 使用教程**
font = QFont("Helvetica", 36, QFont.Bold) #得到一个font object 参数依次是 字体名，大小 ，其他字体属性
fm = QFontMetrics(font) # 获得font字体输出后占据的矩形大小
fm.height() fm.width() #长宽
icon=QIcon("sd.png")
**PyQt4 QTextBrowser 使用教程**
browser = QTextBrowser() #实例化一个textbrowser
browser.append('sdfsdfds') #追加内容
browser.setOpenLinks(True) #打开文档内部链接 默认为True
browser.setOpenExternalLinks(True) #打开外部链接 默认false 当openlinks设置false时 该选项无效
textbrowser.setSearchPaths(["ldks",":/sdfs"]) #设置文档搜索路径 参数为包含目录的List
textbrowser.setSource("index.html") #设置文档
dt=textbrowser.documentTitle() #返回文档的标题
self.connect(textbrowser,SIGNAL("SourceChanged(QUrl)"),self.update) #发出一个SourceChanged(QUrl)信号
textbrowser同时 具有以下插槽: home() :返回主文档, backward() #返回上一文档,forward()前进
browser.setDocumentTitle('dsds') #设置文档标题
**PyQt4 QLineEdit 使用方法**
QLineEdit #单行输入框
lineedit = QLineEdit()# 实例化一个输入框
lineedit.setText(‘abc’)  #设置'abc'给 lineedit 
lineedit.toPlainText()   #获得lineedit的值
lineedit =setReadOnly(True) #设置为只读
lineedit.setDragEnabled(True) #设置能接受拖放
lineedit.setMaxLength(5) #设置最大长度
lineedit.selectAll() #全选
lineedit.setFocus() #得到焦点
lineedit.setInputMask("dx") #设置修饰 该输入框必须输入两个字符
punctuationRe = QRegExp(r"[ ,;:.]") #得到一个regexp对象 可用下面的验证
lineedit.setValidator(QRegExpValidator(QRegExp(r"[0-9]+")),self) #设置验证 检验用户输入内容
lineedit.emit(SIGNAL('textChanged(QString)')) 发出 信号 （设置为只读时貌似发不出 没有具体测试）
lineedit.emit(SIGNAL(textEdited(QString)')) 发出 信号 如果设置了验证 该信号在通过验证才能发出 （设置为只读时貌似发不出 没有具体测试）
QTextEdit  #多行输入框
textedit=QTextEdit()
textedit.setText(data)
textedit.append(data)
textedit.toPlainText() 
**PyQt4 QDial QSpinbox 使用方法**
dial = QDial() #实例化一个dial
dial.setNotchesVisible(True) #设置边缘
dial.emit('SIGNAL(valueChanged(int))') #发出信号
具有 SLOT("setValue(int)") 的插槽
spin=QSpinBox() #实例化
spinbox.setSingleStep(2) #设置步长 ( QDial 有)
spinbox.setRange(1,50)#范围
spinbox.setMaximum(10) #设置最大值 ( QDial 有)
spinbox.setMinimum(5) 设置最小值 ( QDial 有)
spinbox.setValue(6) 设置当前值 ( QDial 有)
print spinbox.value() 得到当前值 ( QDial 有)
**PyQt4 QComboBox QDoubleSpinBox 使用方法**
fromComboBox = QComboBox() #添加一个 combobox
fromComboBox.addItem(rates) #添加一个下拉选项
fromComboBox.addItems(["%d years" % x for x in range(2, 26)]) #从序列中添加
fromComboBox.setMaxVisibleItems(10) #设置最大显示下列项 超过要使用滚动条拖拉
fromComboBox.setMaxCount(5) #设置最大下拉项 超过将不显示
fromComboBox.setInsertPolicy(QComboBox.InsertAfterCurrent) #设置插入方式
插入方式有:NoInsert,InsertAtTop,InsertAtCurrent,InsertAtBottom,InsertAfterCurrent
InsertBeforeCurrent,InsertAlphabetically #字面意思都好理解 最后一个是按字母表顺序插入
QComboBox 发出一个currentIndexChanged(int) 的信号.
QComboBox 得到当前项 currentIndex() + 1 #QComboBox 默认的currentIndex为 -1
QComboBox.findText('dsfds') #返回 内容为dsfds的索引
QComboBox 得到当前项文本内容currentText()
fromSpinBox = QDoubleSpinBox()
fromSpinBox.setRange(0.01, 10000000.00)
fromSpinBox.setSuffix(" %d") #设置后缀 如显示 10.0%d
fromSpinBox.setPrefix('#d') #设置前缀
fromSpinBox.setValue(1.00) #设置值
QDoubleSpinBox 发出 valueChanged(double) 信号 有setValue(double)插槽
(转摘自http://scm002.iteye.com/blog/1728274)
