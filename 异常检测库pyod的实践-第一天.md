Python Outlier Detection（PyOD）是当下最流行的Python异常检测工具库，其主要亮点包括：
1）包括近20种常见的异常检测算法，比如经典的LOF/LOCI/ABOD以及最新的深度学习如对抗生成模型（GAN）和集成异常检测（outlier ensemble）；
2）支持不同版本的Python：包括2.7和3.5+；支持多种操作系统：windows，macOS和Linux简单易用且一致的API，只需要几行代码就可以完成异常检测，方便评估大量算法；
3）使用JIT和并行化（parallelization）进行优化，加速算法运行及扩展性（scalability），可以处理大量数据。

Pyod安装踩坑指南：
pyod安装方法很简单，键入pip install pyod，然后是漫长等待，然后timeout。查询一下官网安装教程https://pyod.readthedocs.io/en/latest/install.html，有很多依赖。pandas要求>0.25。我的python环境是通过anaconda安装的， pandas版本小于安装需要的版本。然后通过conda升级pandas,conda update pandas。输入命令后，无法下载最新版本。网上查询一下， conda下升级pandas是坑。卸载原有的Pandas，换用pip install pandas（记得指定源-i https://pypi.douban.com/simple，要不一定timeout）。pandas安装成功后， pip install pyod终于可以工作了，但是漫长等待 （注意要加上--default-timeout=1000），下载速度不到20k。突然想到，安装教程里提到过，直接从github下载，然后手动安装，看着下载到一半的进度条，郁闷。。。最终，安装statsmodels时，还是出错了，错误如下：
ERROR: THESE PACKAGES DO NOT MATCH THE HASHES FROM THE REQUIREMENTS FILE. If you have updated the package versions, please update the hashes. Otherwise, examine the package contents carefully; someone may have tampered with them.
    statsmodels from https://files.pythonhosted.org/packages/6b/be/c1e4977be0018e1587714b4be570b321558549a69ae1cf334330aae9581f/statsmodels-0.12.1-cp37-none-win_amd64.whl#sha256=e5e426fb962f41d58a07a7d2f7daf32f83e911ff578368caddbcdd1886887ed1 (from pyod):

重新安装pyod,并且换用豆瓣源，成功（速度非常快，郁闷，一直以为，这个豆瓣上可能没有，毕竟不算一个很流行的库）。

下面就是pyod的API学习， 先跑一下KNN的例子代码（https://pyod.readthedocs.io/en/latest/example.html）。将代码copy到pycharm中，运行，报错。Visualize函数不识别。查询API， 发现该函数在pyod.utils.example.visualize中， 增加代码from pyod.utils.example import visualize，还是报错。仔细看， 函数名Visualize第一个字母大写， 而导入库的visualize是小写。改正后， 终于跑通了。打印结果：

On Training Data:
KNN ROC:0.0, precision @ rank n:0.0

On Test Data:
KNN ROC:0.0, precision @ rank n:0.0