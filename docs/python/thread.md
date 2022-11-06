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

## Lock

lock 在不同线程使用同一共享内存时，能够确保线程之间互不影响，使用 lock 的方法是， 在每个线程执行运算修改共享内存之前，执行 lock.acquire()将共享内存上锁， 确保当前线程执行时，内存不会被其他线程访问，执行运算完毕后，使用 lock.release()将锁打开， 保证其他的线程可以使用该共享内存

> 保证唯一访问权限, 避免同时修改冲突
