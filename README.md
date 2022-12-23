
# 1 - Dependencies management

***git branch name:*** dependencies


## Theory \[2\]

As usual, we will start with a few theoretical questions:

-   \[0.5\] What is Docker, and how it differs from dependencies
    management systems? From virtual machines?

Docker --- это платформа с открытым исходным кодом для создания,
развертывания и управления контейнерными приложениями.

Docker отличается от других систем управления зависимостями своей
гибкостью и безопасностью. Кроме того, этот облачный сервер
предоставляет множество бесплатных приложений, а также множество
общедоступных и частных реестров с официальными репозиториями от ведущих
сторонних поставщиков --- от Nginx и Ubuntu до MongoDB и Redis.

Docker разработан, чтобы быть легким и простым. Он имеет хороший уровень
безопасности 760 и очень популярен в использовании, поэтому, если вы
найдете ошибку, вероятность того, что вы найдете решение в Интернете,
составляет 99%.

Хотя для каждой рабочей нагрузки на виртуальной машине (ВМ) требуется
полноценная ОС или гипервизор, многие рабочие нагрузки могут выполняться
на одной ОС при использовании Docker.

Контейнеры Docker имеют быстрое время запуска и сокращают время
загрузки. Запуск виртуальных машин занимает некоторое время и имеет
ужасную производительность. Поскольку контейнеры Docker меньше, чем
виртуальные машины, проще перемещать файлы в файловую систему хоста.

В связи с тем, что ОС запущена, приложения Docker-контейнеров
запускаются сразу. Виртуальные машины должны запускать полную
операционную систему для установки одной программы, для которой
требуется процесс полной загрузки.

-   \[0.5\] What are the advantages and disadvantages of using
    containers over other approaches?

**Преимущества контейнеров:**

-   стабильность
-   экономия места
-   контейнеры работают одинаково в разных средах
-   автоматизация. позволяет вызывать контейнеры только при
    необходимости

**Недостатки контейнеров:**

-   документация обновляется медленно

-   нужно прям сидеть и разбираться



-   \[0.5\] Explain how Docker works: what are Dockerfiles, how are
    containers created, and how are they run and destroyed?

Dockerfile --- это текстовый документ, содержащий все команды, которые
пользователь может вызвать в командной строке для сборки образа.

Создайте каталог для хранения всех образов Docker, которые будут
собраны:

    mkdir docker_dir_name
    cd docker_dir_name
    touch Dockerfile
    nano Dockerfile

Дальше запишем. Просто тестовый код, который поприветствует нас в
консоли:

    FROM ubuntu

    MAINTAINER author

    RUN apt-get update

    CMD ["echo", "Welcome to the container"]

Создайте образ Docker с помощью Dockerfile:

    docker build [OPTIONS] PATH | URL |
    docker build [location of your dockerfile]
    docker build -t image_name
    docker images

#### Create a New Container

    docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

#### Destroy it

    docker kill [OPTIONS] CONTAINER [CONTAINER...]

-   \[0.25\] Name and describe at least one Docker competitor (i.e., a
    tool based on the same containerization technology).

CoreOS Rkt

Программный движок контейнеризации под названием CoreOS rkt позволяет
запускать рабочие нагрузки приложений отдельно от базовой
инфраструктуры. Это главный конкурент контейнерного движка Docker.

The Application Container Image (ACI) из спецификации контейнера
приложения служит основой для CoreOS rkt. ACI --- это архив, состоящий
из манифеста образа и корневой файловой системы со всеми файлами,
необходимыми для запуска приложения. Большинство настроек по умолчанию
можно изменить во время выполнения, а команда rkt run позволяет
пользователям добавлять свои собственные параметры выполнения к
определенному образу.

Большинство основных версий ОС Linux поддерживают rkt-контейнеры CoreOS
в виде двоичного файла, который интегрируется с системами и сценариями
инициализации Linux и работает в соответствии с моделью процессов Unix
«родитель-потомок».

Поды, представляющие собой наборы одновременно работающих программ,
используются CoreOS rkt для настройки контейнеров. Модуль может включать
отдельные конфигурации для различных областей, от уровня модуля до
конкретных приложений внутри модуля. Поды работают независимо и в
удаленных местах без центрального демона.

-   \[0.25\] What is conda? How it differs from apt, yarn, and others?

Conda --- это система управления пакетами с открытым исходным кодом и
система управления средой, которая работает в Windows, macOS, Linux и
z/OS. Conda быстро устанавливает, запускает и обновляет пакеты и их
зависимости. Conda легко создает, сохраняет, загружает и переключается
между средами на вашем локальном компьютере. Он был создан для программ
Python, но может упаковывать и распространять программное обеспечение
для любого языка.

Conda более популярен для нужд разработчиков (у него много инструментов
разработчика по сравнению с пряжей). Это позволяет пользователю работать
локально в средах, которые не находятся в каталоге root/bin, например,
пользователь может использовать разные версии python в каждой среде
(conda или apt).



## Problem \[6.5\]

The problem itself is relatively simple.

Imagine that you developed an excellent RNA-seq analysis pipeline and
want to share it with the world. Based on your experience, you are
confident that the popularity of the pipeline will be proportional to
its ease of use. So, you decided to help your future users and to pack
all dependencies in a Conda environment and a Docker container.

Here is the list of tools and their versions that are used in your work:

-   [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
    v0.11.9
-   [STAR](https://github.com/alexdobin/STAR), v2.7.10b
-   [samtools](https://github.com/samtools/samtools), v1.16.1
-   [picard](https://github.com/broadinstitute/picard), v2.27.5
-   [salmon](https://github.com/COMBINE-lab/salmon), commit tag 1.9.0
-   [bedtools](https://github.com/arq5x/bedtools2), v2.30.0
-   [multiqc](https://github.com/ewels/MultiQC), v1.13


**Anaconda**:

-   \[1\] Install conda, create a new virtual environment, and install
    all necessary packages.
-   \[0.75\] You won\'t be able to install some tools - that\'s fine.
    List their names, and explain what should be done to make them
    conda-friendly
    ([conda-forge](https://conda-forge.org/docs/maintainer/adding_pkgs.html)
    channel,
    [bioconda](https://bioconda.github.io/contributor/workflow.html)
    channel).
-   \[0.25\]
    [Export](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file)
    the environment
    ([example](https://github.com/nf-core/clipseq/blob/master/environment.yml))
    to the file and verify that it can be
    [rebuilt](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
    from the file without problems.

**Docker**:

-   \[3\] Create a Dockerfile for a container with **all** required
    dependencies. Don\'t forget about comments; test that all tools are
    accessible and work inside the container. Hints:
-   If needed, grant rights to execute downloaded/compiled binaries
    using chmod (`chmod a+x BINARY_NAME`)
-   Move all executables to \$PATH folders (e.g.`/usr/local/bin`) to
    make them accessible without specifying the full path.
-   Typical command to run a container interactively (`-it`) and delete
    on exit(`--rm`): `docker run --rm -it name:tag`
-   \[1\] Use [hadolint](https://hadolint.github.io/hadolint/) and
    remove as many reported warnings as possible.
-   \[0.5\] Add relevant
    [labels](https://docs.docker.com/engine/reference/builder/#label),
    e.g. maintainer, version, etc.
    ([hint](https://medium.com/@chamilad/lets-make-your-docker-image-better-than-90-of-existing-ones-8b1e5de950d))


## Anaconda:

### Install conda

conda уже установлена

### create a new virtual environment

conda create -n hw_env python=3.10 --no-default-packages <br>
conda activate hw_env <br>

conda config --add channels defaults <br>
conda config --add channels bioconda <br>
conda config --add channels conda-forge <br>

### install all necessary packages
conda install -y fastqc=0.11.9 <br>
conda install -y star=2.7.10b <br>
conda install -y samtools=1.16.1 <br>
conda install -y picard <br>
conda install -y salmon=1.9.0 <br>
conda install -y bedtools=2.30.0 <br>
conda install -y multiqc=1.13 <br>

### You won't be able to install some tools - that's fine. List their names, and explain what should be done to make them conda-friendly (conda-forge channel, bioconda channel).
picard - так как цель задания поработать с кондой, то я поставил его через нее, но там версия 2.27.4 вместо 2.27.5. Можно поставить руками нужную версию, но тогда она не попадет в conda env, так что я не стал. Если вдруг это надо было, то на их гитхабе лежит построчный код, как это поставить руками.

Если какие-то другие пакеты не ставятся, то можно пробовать поменять канал вручную на bioconda.

## Docker:

    FROM ubuntu:20.04

    # update links and install apt-utils apt-transport-https unzip and python3-pip
    RUN apt-get update
    RUN apt -y install apt-utils apt-transport-https openjdk-11-jre-headless unzip python3-pip

    # create /.bashrc for aliases
    RUN touch /.bashrc

    # fastqc v0.11.9
    RUN wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.9.zip && \
        unzip fastqc_v0.11.9.zip && \
        rm fastqc_v0.11.9.zip && \
        chmod a+x FastQC/fastqc && \
        echo 'alias fastqc="/FastQC/fastqc"' >> /.bashrc

    # STAR v.2.7.10b
    RUN wget https://github.com/alexdobin/STAR/releases/download/2.7.10b/STAR_2.7.10b.zip && \
        unzip STAR_2.7.10b.zip && \
        rm STAR_2.7.10b.zip && \
        chmod a+x STAR_2.7.10b/Linux_x86_64_static/STAR && \
        mv STAR_2.7.10b/Linux_x86_64_static/STAR /bin/STAR && \
        rm -r STAR_2.7.10b

    # samtools v1.16.1
    RUN wget https://github.com/samtools/samtools/archive/refs/tags/1.16.1.zip -O ./samtools-1.16.1.zip && \
        unzip samtools-1.16.1.zip && \
        rm samtools-1.16.1.zip && \
        mv samtools-1.16.1/misc samtools && \
        rm -r samtools-1.16.1 && \
        echo 'alias samtools="/samtools/samtools.pl"' >> /.bashrc

    # picard v2.27.5
    RUN wget https://github.com/broadinstitute/picard/releases/download/2.27.5/picard.jar -O /bin/picard.jar && \
        chmod a+x /bin/picard.jar && \
        echo 'alias picard="java -jar /bin/picard.jar"' >> /.bashrc

    # salmon v.1.9.0
    RUN wget https://github.com/COMBINE-lab/salmon/releases/download/v1.9.0/salmon-1.9.0_linux_x86_64.tar.gz && \
        tar -zxvf salmon-1.9.0_linux_x86_64.tar.gz && \
        rm salmon-1.9.0_linux_x86_64.tar.gz && \
        chmod a+x salmon-1.9.0_linux_x86_64/bin/salmon && \
        mv salmon-1.9.0_linux_x86_64/bin/salmon /bin/salmon && \
        rm -r salmon-1.9.0_linux_x86_64 

    # bedtools v.2.30.0
    RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.30.0/bedtools.static.binary -O /bin/bedtools.static.binary && \
        chmod a+x /bin/bedtools.static.binary && \
        echo 'alias bedtools="/bin/bedtools.static.binary"' >> /.bashrc

    # multic v1.13
    RUN pip install multiqc==1.13

## Extra points \[1.5\]

You will be awarded extra points for the following:

-   \[0.5\] Using [multi-stage
    builds](https://docs.docker.com/build/building/multi-stage/) in
    Docker. E.g. to build STAR and copy only the executable to the final
    image.

-   \[0.75\] Minimizing the size of the final Docker image. That is,
    removing all intermediates, unnecessary binaries/caches, etc. Don\'t
    forget to compare & report the final size before and after all the
    optimizations.

-   \[0.25\] Create an extra Dockerfile that starts from [a conda base
    image](https://hub.docker.com/r/continuumio/anaconda3) and builds
    everything from your conda environment file.

Hint: `conda env create --quiet -f environment.yml && conda clean -a`
([example](https://github.com/nf-core/clipseq/blob/master/Dockerfile))


#### Занимаемый объем

До сжатия: 2.0 Gb <br>
После сжатия: 1.3 Gb

#### Docker для conda

    FROM continuumio/anaconda3

    #create the env    
    COPY environment.yml . 
    RUN apt-get update && apt-get -y install apt-utils=2.4.8 && \
      apt-get -y installed apt-transport-https=2.0.2ubuntu0.2 && \
      conda env create --file hw_env.yml && conda clean -a
