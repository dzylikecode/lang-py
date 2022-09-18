# 自动化测试

```py
def my_func1(a):
    if a == 1:
        return 2
    elif a == -1:
        return 3
    else:
        return 1

def my_func2(b):
    if b != "yes":
        raise ValueError("you can only say yes!")
    else:
        return True

class TestFunc(unittest.TestCase):
    def test_func1(self):
        self.assertEqual(2, my_func1(1))
        self.assertEqual(3, my_func1(-1))
        for i in range(-100, 100):
            if i == 1 or i == -1:
                continue
            self.assertEqual(1, my_func1(i))

    def test_func2(self):
        self.assertTrue(my_func2("yes"))
        with self.assertRaises(ValueError):
            my_func2("nononono")

if __name__ == "__main__":
    unittest.main()
```

- 部分测试

  ```py
  class TestFunc(unittest.TestCase):
      def test_func1(self):
          self.assertEqual(2, my_func1(1))
          self.assertEqual(3, my_func1(-1))
          for i in range(-100, 100):
              if i == 1 or i == -1:
                  continue
              self.assertEqual(1, my_func1(i))

      def test_func2(self):
          self.assertTrue(my_func2("yes"))
          with self.assertRaises(ValueError):
              my_func2("nononono")

  # 定义一个 suite 替换 unittest.main()
  suite = unittest.TestSuite()
  suite.addTest(TestFunc('test_func1'))
  unittest.TextTestRunner().run(suite)
  ```

## reference

- [How To Use unittest to Write a Test Case for a Function in Python](https://www.digitalocean.com/community/tutorials/how-to-use-unittest-to-write-a-test-case-for-a-function-in-python)
