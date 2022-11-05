# 文件

## create

```py
f = open("new_file.txt", "w")   # 创建并打开
f.write("some text...")         # 在文件里写东西
f.close()                       # 关闭
```

把打开和关闭嵌入到了一个 `with` 架构中

```py
with open("new_file2.txt", "w") as f:
    f.writelines(["some text for file2...\n", "2nd line\n"])
```

## read/write

- `f.read()`
- `f.readlines()`

## encode

```py
with io.open(filename,'r',encoding='utf8') as f:
    text = f.read()
# process Unicode text
with io.open(filename,'w',encoding='utf8') as f:
    f.write(text)
with open("chinese.txt", "wb") as f: # !!notice!! wb
    f.write("这是中文的，this is Chinese".encode("gbk"))
```

| mode |               action               |
| :--: | :--------------------------------: |
|  w   |           （创建）写文本           |
|  r   |      读文本，文件不存在会报错      |
|  a   |           在文本最后添加           |
|  wb  |          写二进制 binary           |
|  rb  |          读二进制 binary           |
|  ab  |             添加二进制             |
|  w+  |      又可以读又可以（创建）写      |
|  r+  | 又可以读又可以写, 文件不存在会报错 |
|  a+  |       可读写，在文本最后添加       |
|  x   |                创建                |

## folder

- 文件目录操作

  - os.getcwd()
  - os.listdir()
  - os.makedirs()
  - os.path.exists()

    `os.makedirs("project", exist_ok=True)`

  ```py
  import shutil

  shutil.rmtree("user/mofan")
  print(os.listdir("user"))
  ```

- 文件管理系统
  - os.removedirs()
  - shutil.rmtree()
  - os.rename()
- 文件目录多种检验
  - os.path.isfile()
  - os.path.exists()
  - os.path.isdir()
  - os.path.basename()
  - os.path.dirname()
  - os.path.split()
