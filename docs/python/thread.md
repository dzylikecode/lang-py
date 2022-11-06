# 多线程

- lib

  ```py
  import threading
  ```

- 获取已激活的线程数

  ```py
  threading.active_count()
  ```

- 查看所有线程信息

  ```py
  threading.enumerate()
  ```

- 当前线程

  ```py
  threading.current_thread()
  ```

- 执行任务

  ```py
  def thread_job():
      print('This is a thread of %s' % threading.current_thread())

  def main():
      thread = threading.Thread(target=thread_job,)   # 定义线程
      thread.start()  # 让线程开始工作

  if __name__ == '__main__':
      main()
  ```

## join

类似 js 的 await 等待执行完

- 非 join

  ```py
  added_thread.start()
  print("all done\n")
  ```

- join

  ```py
  added_thread.start()
  added_thread.join()
  print("all done\n")
  ```

- 使用 queue 储存结果

## GIL

Global Interpreter Lock (GIL)

- [Python 的全局锁问题](https://python3-cookbook.readthedocs.io/zh_CN/latest/c12/p09_dealing_with_gil_stop_worring_about_it.html)
