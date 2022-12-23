# ДЗ 1

## Theory 


[2]
As usual, we will start with a few theoretical questions:

[0.5] What is Docker, and how it differs from dependencies management systems? From virtual machines?

- Докер является альтернативой гипервизорам, используя контейнеры вместо виртуальных машин. Главное приемущество перед ВМ состоит в том, что для каждого контейнера не нужна отдельная ОС, что очень экономит время и ресурсы. Контейнеры представляют собой изолированную среду для разработки и тестирования, в них легко реализуется управление зависимости.


[0.5] What are the advantages and disadvantages of using containers over other approaches?

Контейнеры экономят ресурсы и время, но являются более медленными и менее безопасными. Кроме того, при удалении контейнера несохраненные данные теряются.


[0.5] Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?

После запуска докер работает в фоне в виде демона. Сначала создается образ - виртуальное окружение, по "образу" которого может быть контейнер. Он будет представлять собой изолированный кусок файловой системы, внутри которой можно развлекаться как угодно, например распаковать пару вирусов. Из контейнера можно извлечь данные, если этого не сделать, то после удаления контейнера все его данные будут утеряны.


[0.25] Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).

- Самой близкой к докеру утилитой называют Podman от красных шляп. В отличие от докера, не использует демона и вследствие этого не требует root-прав, может работать из-под обычного пользователя. Также считается, что образы с меньшим количеством доступов безопаснее. К главным минусам можно отнести то, что для создания образов ему требуется еще одна тулза под названием Buildah.


[0.25] What is conda? How it differs from apt, yarn, and others?

Конда - инструмент управления зависимостями, позволяющий удобно создавать, использовать и экспортировать виртуальные окружения. В отличие от других пакетных менеджеров, она не требует sudo и может выполняться под обычном юзером, что очень удобно например для шерящихся кластеров, как у нас на майноре было.



## Anaconda:

Поскольку за установку линуха баллов не дают, выполняю все на сервере яндекса из ДЗ 2 через Putty (SSH).

[1] Install conda, create a new virtual environment, and install all necessary packages.

Скачиваем, ставим, принимаему еулу:

```
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
bash Anaconda3-2022.10-Linux-x86_64.sh
```

![image](https://user-images.githubusercontent.com/58905528/209350923-04a3290a-8945-4d39-bb61-cc6bcd015ca5.png)
![image](https://user-images.githubusercontent.com/58905528/209350908-a0be236b-cdce-4f13-878a-ff0d9102fe94.png)

venv:

```
eval "$(/home/vst/anaconda3/bin/conda shell.bash hook)"
conda init 
conda create --name myenv
conda activate myenv
```

Ставим пакет с пакетами:

```
conda install -c bioconda fastqc==0.11.9
conda install -c bioconda star #==v2.7.10b ->> that`s last version :)
conda install -c bioconda samtools==1.16.1 
conda install -c bioconda picard #==2.27.5 version does not exist) the last one is 2.27.4
conda install -c bioconda salmon==1.9.0 
conda install -c bioconda bedtools==2.30.0
conda install -c bioconda multiqc # for py 2.7 & does not exist
```




[0.75] You won't be able to install some tools - that's fine. List their names, and explain what should be done to make them conda-friendly (conda-forge channel, bioconda channel).

STAR не захотел ставиться через версию, возможно буква мешала. Для picard была указана версия, которая еще не вышла. MultiQC 1.13 требует питона 2-й версии и не существует.

![image](https://user-images.githubusercontent.com/58905528/209356194-75fd4767-a487-4b46-85ae-65a348e48bb2.png)
![image](https://user-images.githubusercontent.com/58905528/209356134-0ed1fe07-d13c-4288-9c64-1c225df7bbfd.png)
![image](https://user-images.githubusercontent.com/58905528/209356165-9131eb7f-2672-44b5-91a6-11dd6d033748.png)




[0.25] Export the environment (example) to the file and verify that it can be rebuilt from the file without problems.


## Docker:

[3] Create a Dockerfile for a container with all required dependencies. Conda usage is not allowed, don't forget about comments; test that all tools are accessible and work inside the container. Hints:
If needed, grant rights to execute downloaded/compiled binaries using chmod (chmod a+x BINARY_NAME)
Move all executables to $PATH folders (e.g./usr/local/bin) to make them accessible without specifying the full path.
Typical command to run a container interactively (-it) and delete on exit(--rm): docker run --rm -it name:tag

[1] Use hadolint and remove as many reported warnings as possible.

[0.5] Add relevant labels, e.g. maintainer, version, etc. (hint)
