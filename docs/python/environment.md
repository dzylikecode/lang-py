# 环境

- wsl2, Ubuntu
- 使用 miniconda

## miniconda

- [conda tutorial](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)

### install

1. Download the latest shell script

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

2. Make the miniconda installation script executable

```bash
chmod +x Miniconda3-latest-Linux-x86_64.sh
```

3. Run miniconda installation script

```bash
./Miniconda3-latest-Linux-x86_64.sh
```

4. Make sure the miniconda installation is complete

```bash
conda info
```

5. deactivate the default environment

```bash
conda config --set auto_activate_base false
```

### commands

- [Conda 常用命令整理](https://blog.csdn.net/menc15/article/details/71477949)

- 高频

  `conda create --name your_env_name python=3.5`

  `conda env list`

  `activate your_env_name`

  `deactivate`

  `conda remove --name your_env_name --all`

  `conda create --name new_env_name --clone old_env_name `

- 分享环境

  当前环境

  - 导出: `conda env export > environment.yml`
  - 导入: `conda env create -f environment.yml`

  - [How to share conda environments across platforms](https://stackoverflow.com/questions/39280638/how-to-share-conda-environments-across-platforms)

    似乎没有很好的解决方法

    `conda env export > environment.yml` 会记录通过 pip 安装的包
