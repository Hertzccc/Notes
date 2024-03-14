# Pytest自动化

- 自动化测试平台作用：
  - 让不懂代码的人也能够通过框架实现自动化测试，
  - 减少人工干预，提高测试效率和准确性

pytest是自动化测试框架的组成部分之一

## 1. Pytest

- pytest可以和selenium，requests，appium结合实现web自动化，接口自动化，app自动化
- pytest可以实现测试用例跳过以及 returns失败用例重试
- pytest可以和allure生成测试报告
- pytest可以和Jenkins持续集成
- pytest有非常强大的插件
  - pytest-html：自动化测试报告
  - pytest-xsist：测试用例分布式执行，多CPU分发
  - pytest-ordering：用于改变测试用例的执行顺序
  - pytest-returnfailures：用例失败后重跑
  - allure-pytest：用于生成美观的测试报告



## 2. 使用pytest

1. 模块名必须以test_开头或 _test结尾
2. 测试类以Test开头不能有init方法
3. 测试方法以test开头



## 3. pytest测试用例的运行方式

1. 主函数模式：

   1. 运行所有：pytest.main()

   2. 指定模块：pytest.main(['-vs','test_login.py])

   3. 指定目录：pytest.main(['-vs','./interface_testcase])

   4. 通过nodeid指定：nodeid由模块名，分隔符，类名，方法名，函数名组成

      pytest.main(['-vs','./interface_testcase/test_login.py::test_04_func'])

2. 命令行模式：pytest -vs ./interface_testcase/test_interface.py::Testshishi::test_04_func

3. 通过读取pytest.ini运行

   1. 编码ANSI

   2. 改变pytest默认行为

      例子：

      [pytest]

      addopts = -vs 	#命令行参数

      testpaths = ./testcase 	#测试用例路径

      python_files = test_*.py	#模块名规则

      python_classes = Test*	#类名的规则

      python_functions = test	#方法名的规则

      markers = 

      ​	smoke:

      ​	usermanage

      ​	productmanage

- 参数：

  - -s：输出调试信息，包括print打印的信息
  - -v：显示更详细的信息
  - 可以用-vs
  - -n : 多线程 -n 2
  - --reruns #num:失败重跑
  - -x：只要一个用例失败，测试终止
  - -k：根据测试用例部分字符串指定测试用例。-k ”ao“
  - -html: -html ./report/report.html

  

- 执行顺序

使用mark标记，用插件pytest-ordering

@pytest.mark.run(order=3)



## 4. pytest 分组测试

- somke: 冒烟用例，可以分布在各个模块里面
- pytest -vs -m "smoke"
- pytest -vs -m "smoke or usermanage"



## 5. pytest 实现前后置（固件、夹具）

- 重要性：例，web自动化执行用例之前可以打开浏览器



## 6. pytest.fixture()装饰器实现**部分**用例前后置

- 先声明 @pytest.fixture(scope='', params='',autouse='',ids='',name='')
  - scope:作用域, function(default), class, module, package/session
  - params: 参数化
  - autouse=True: 自动执行，默认false
  - ids：使用参数化后，给每个值设置一个变量
  - name: 给fixture方法取一个别名

## 7. conftest.py和@pytest.fixture()结合实现全局前置应用

- 单独存放夹具的配置文件
- 可以有多级conftest



## 8. allure-pytest插件生成报告

--alluredir ./temp 生成报告到temp中

生成html报告（从./temp 中）：os.system('allure generate ./temp -o ./report --clean')



## 9. yaml 接口自动化实战