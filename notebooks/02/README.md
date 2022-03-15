# Hydra: Getting started

## Introduction[](https://hydra.cc/docs/intro/#introduction "Direct link to heading")

Hydra is an open-source Python framework that simplifies the development of research and other complex applications. The key feature is the ability to dynamically create a hierarchical configuration by composition and override it through config files and the command line. The name Hydra comes from its ability to run multiple similar jobs - much like a Hydra with multiple heads.

### Key features:[](https://hydra.cc/docs/intro/#key-features "Direct link to heading")

-   Hierarchical configuration composable from multiple sources
-   Configuration can be specified or overridden from the command line
-   Dynamic command line tab completion
-   Run your application locally or launch it to run remotely
-   Run multiple jobs with different arguments with a single command

## Quick start guide[](https://hydra.cc/docs/intro/#quick-start-guide "Direct link to heading")

This guide will show you some of the most important features you get by writing your application as a Hydra app. If you only want to use Hydra for config composition, check out Hydra's [compose API](https://hydra.cc/docs/advanced/compose_api/) for an alternative. Please also read the full [tutorial](https://hydra.cc/docs/tutorials/basic/your_first_app/simple_cli/) to gain a deeper understanding.

### Installation[](https://hydra.cc/docs/intro/#installation "Direct link to heading")

```
pip install hydra-core --upgrade
```

### Basic example[](https://hydra.cc/docs/intro/#basic-example "Direct link to heading")

Config:

conf/config.yaml

```
db:  driver: mysql  user: omry  pass: secret
```

Application:

my\_app.py

```
import hydrafrom omegaconf import DictConfig, OmegaConf@hydra.main(config_path="conf", config_name="config")def my_app(cfg : DictConfig) -> None:    print(OmegaConf.to_yaml(cfg))if __name__ == "__main__":    my_app()
```

You can learn more about OmegaConf [here](https://omegaconf.readthedocs.io/en/latest/usage.html#access-and-manipulation) later.

`config.yaml` is loaded automatically when you run your application

```
$ python my_app.pydb:  driver: mysql  pass: secret  user: omry
```

You can override values in the loaded config from the command line:

```
$ python my_app.py db.user=root db.pass=1234db:  driver: mysql  user: root  pass: 1234
```

### Composition example[](https://hydra.cc/docs/intro/#composition-example "Direct link to heading")

You may want to alternate between two different databases. To support this create a `config group` named db, and place one config file for each alternative inside: The directory structure of our application now looks like:

```
├── conf│   ├── config.yaml│   ├── db│   │   ├── mysql.yaml│   │   └── postgresql.yaml│   └── __init__.py└── my_app.py
```

Here is the new config:

`defaults` is a special directive telling Hydra to use db/mysql.yaml when composing the configuration object. The resulting cfg object is a composition of configs from defaults with configs specified in your `config.yaml`.

You can now choose which database configuration to use and override values from the command line:

```
$ python my_app.py db=postgresql db.timeout=20db:  driver: postgresql  pass: drowssap  timeout: 20  user: postgres_user
```

You can have as many config groups as you need.

### Multirun[](https://hydra.cc/docs/intro/#multirun "Direct link to heading")

You can run your function multiple times with different configuration easily with the `--multirun|-m` flag.

```
$ python my_app.py --multirun db=mysql,postgresql[HYDRA] Sweep output dir : multirun/2020-01-09/01-16-29[HYDRA] Launching 2 jobs locally[HYDRA]        #0 : db=mysqldb:  driver: mysql  pass: secret  user: omry[HYDRA]        #1 : db=postgresqldb:  driver: postgresql  pass: drowssap  timeout: 10  user: postgres_user
```

There is a whole lot more to Hydra. Read the [tutorial](https://hydra.cc/docs/tutorials/basic/your_first_app/simple_cli/) to learn more.



# 텍스트 데이터를 다루기 위한 Python

- 보조자료
  > _W02-1. 텍스트 데이터를 다루기 위한 Python: 기본문법 [(Colab)](https://colab.research.google.com/github/fingeredman/text-mining-for-practice/blob/master/practice-note/week_02/W02-1_text-mining-for-practice_python-basic.ipynb)_  
  > _W02-2. 텍스트 데이터를 다루기 위한 Python: 자료구조 [(Colab)](https://colab.research.google.com/github/fingeredman/text-mining-for-practice/blob/master/practice-note/week_02/W02-2_text-mining-for-practice_python-data-structure.ipynb)_  
  > _W02-3. 텍스트 데이터를 다루기 위한 Python: 반복문과 조건문 [(Colab)](https://colab.research.google.com/github/fingeredman/text-mining-for-practice/blob/master/practice-note/week_02/W02-3_text-mining-for-practice_python-conditional%26loop.ipynb)_  
  > _W02-4. 텍스트 데이터를 다루기 위한 Python: 함수와 파일입출력 [(Colab)](https://colab.research.google.com/github/fingeredman/text-mining-for-practice/blob/master/practice-note/week_02/W02-4_text-mining-for-practice_python-function%26file.ipynb)_  