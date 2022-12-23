# 2 - Working with remote servers

**git branch name:** jbrowser

## Theory \[2\]

-   \[0.4\] What are [computer
    ports](https://www.cloudflare.com/learning/network-layer/what-is-a-computer-port/)
    on a high level? How many ports are there on a typical computer?

Компьютерные порты относятся к определенным каналам, по которым данные
передаются между различными устройствами или компьютерными системами в
сети. Эти порты идентифицируются уникальными числовыми значениями
(номера портов), которые позволяют передавать через них различные типы
данных.

Всего на обычном компьютере имеется 65536 доступных коммуникационных
портов, но чаще всего используется лишь небольшая часть из них.
Некоторые из наиболее распространенных портов и их функции:

Порт 80 --- HTTP (протокол передачи гипертекста)

Порт 443 --- HTTPS (протокол защищенной передачи гипертекста)

Порт 22 --- SSH (безопасная оболочка)

Порт 21 --- FTP (протокол передачи файлов)

Порт 25 --- SMTP (простой протокол передачи почты)

Порт 53 --- DNS (система доменных имен)

Порт 3389 --- RDP (протокол удаленного рабочего стола)

Порт 23 --- Telnet (телетайпная сеть)

Порт 554 --- RTSP (протокол потоковой передачи в реальном времени)

Порт 110 --- POP3 (протокол почтового отделения версии 3)

-   \[0.4\] What is the difference between http, https, ssh, and other
    protocols? In what sense are they similar? Name default ports for
    several data transfer protocols.

HTTP (Hypertext Transfer Protocol) --- это протокол, используемый для
передачи данных в Интернете. Это основа передачи данных в Интернете и
используется для отправки и получения данных между веб-браузером и
веб-сервером.

HTTPS (Hypertext Transfer Protocol Secure) --- это безопасная версия
HTTP. Он использует безопасное соединение (SSL/TLS) для шифрования
данных, передаваемых между веб-браузером и веб-сервером.

SSH (Secure Shell) --- это сетевой протокол, используемый для безопасной
связи между двумя устройствами. Он обычно используется для удаленного
доступа к серверам и управления ими, а также для безопасной передачи
файлов между системами.

Разница между протоколами заключается в шифрования и конкретных задачах,
но похожи тем, что созданы для передачи информации.

Некоторые примеры включают FTP (протокол передачи файлов) для передачи
файлов, SMTP (простой протокол передачи почты) для отправки электронной
почты и POP (протокол почтового отделения) для получения электронной
почты.

Порты по умолчанию:

-   HTTP --- порт 80

-   HTTPS --- порт 443

-   SSH --- порт 22

-   \[0.4\] Explain briefly: (1) what is IP, (2) what IPs are called
    \'white\'/public, (3) and what happens when you enter \'google.com\'
    into the web browser.

IP - уникальный числовой идентификатор устройства в компьютерной сети
(локальной или глобальной), работающей по протоколу IP.

Общедоступные IP-адреса - те, к которым можно получить доступ через
Интернет, называются «белыми» или общедоступными IP-адресами. Эти
IP-адреса назначаются устройствам, которые напрямую подключены к
Интернету, например серверам и маршрутизаторам.

what happens when you enter \'google.com\' into the web
browse:
Браузер отправляет запрос на сервер доменных имен
(DNS) для преобразования доменного имени в IP-адрес. DNS-сервер отвечает
IP-адресом сервера, на котором размещен веб-сайт. Браузер отправляет
запрос на сервер, используя IP-адрес. Сервер отвечает, отправляя файлы
HTML, CSS и JavaScript веб-сайта в браузер. Браузер использует эти файлы
для визуализации веб-сайта и отображения его пользователю.

-   \[0.4\] What is Nginx? How does it work on the high level? List
    several alternative web servers.

Nginx --- это веб-сервер с открытым исходным кодом, который используется
для размещения веб-сайтов и веб-приложений.

На высоком уровне Nginx работает, принимая входящие HTTP-запросы от
клиентов (например, веб-браузеров) и перенаправляя их на назначенный
внутренний сервер. Затем внутренний сервер обрабатывает запрос и
возвращает соответствующий ответ, который Nginx отправляет обратно
клиенту.

Nginx можно использовать как автономный веб-сервер или как обратный
прокси-сервер, где он находится перед несколькими внутренними серверами
и распределяет входящие запросы между ними.

Некоторые альтернативные веб-серверы: Apache, IIS (Internet Information
Services) и LiteSpeed.

-   \[0.4\] What is SSH, and for what is it typically used? Explain two
    ways to authenticate in an SSH server in detail.

SSH (Secure Shell) --- это сетевой протокол, обеспечивающий безопасный
удаленный доступ к компьютеру или серверу через незащищенную сеть.
Обычно он используется для удаленного доступа к серверам и управления
ими, а также для безопасной передачи файлов между системами.

Существует два основных способа аутентификации на сервере SSH:

1\) Аутентификация на основе пароля: это наиболее распространенный метод
аутентификации в SSH. Он предполагает, что пользователь вводит
правильный пароль, чтобы получить доступ к серверу. Пароль обычно
хранится в файле с именем «authorized_keys» на сервере, который
зашифрован и доступен только администратору сервера.

2\) Аутентификация с открытым ключом. Этот метод аутентификации
предполагает использование пары криптографических ключей --- открытого
ключа и закрытого ключа --- для аутентификации пользователя. Открытый
ключ пользователя хранится на сервере, а закрытый ключ хранится на
локальном компьютере пользователя. Когда пользователь пытается
подключиться к серверу, сервер отправляет запрос, который может быть
расшифрован с помощью закрытого ключа пользователя. Если расшифровка
прошла успешно, пользователю предоставляется доступ к серверу.

Оба эти метода аутентификации являются безопасными, но аутентификация с
открытым ключом обычно считается более безопасной, поскольку она не
зависит от того, что пользователь помнит пароль, который можно легко
скомпрометировать или забыть.


## Problem \[6.5\]

A real-life situation that occurred to me several times over the years.

Imagine wrapping up a large bioinformatics project and wanting to share
raw data with your colleagues in a friendly and straightforward format.
The best option would be to use an online genome browser and host your
data remotely, so it is easily accessible by anyone with a valid link.
This is exactly what we will be doing here.

*Please consider doing this HW using Linux since setting up the SSH
client on Windows is painful, and I won\'t be able to help you.*


## Remote Server

### 1.

Сделал машину на yandex.cloud <br>
Сгенерировал ключи: ssh-keygen -t hw_ssh

### 2.
``` {.python}
sudo apt-get install wget samtools tabix
mkdir genome && cd genome
wget ftp://ftp.ensembl.org/pub/release-99/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa

wget ftp://ftp.ensembl.org/pub/release-99/gff3/homo_sapiens/Homo_sapiens.GRCh38.99.gff3.gz
gunzip Homo_sapiens.GRCh38.99.gff3.gz
sort -k1,1 -k4,4n Homo_sapiens.GRCh38.99.gff3 > Homo_sapiens.GRCh38.99.sorted.gff3
bgzip Homo_sapiens.GRCh38.99.sorted.gff3
tabix -p gff Homo_sapiens.GRCh38.99.sorted.gff3.gz
```

### 3. {#3}

TF1: <https://www.encodeproject.org/files/ENCFF404ASR/> `<br>`{=html}
TF2: <https://www.encodeproject.org/files/ENCFF699UTZ/> `<br>`{=html}
TF3: <https://www.encodeproject.org/files/ENCFF507JZI/> `<br>`{=html}
`<br>`{=html} ATAC: <https://www.encodeproject.org/files/ENCFF516KWQ/>
`<br>`{=html}

``` {.python}
mkdir bed_files && cd bed_files

wget https://www.encodeproject.org/files/ENCFF404ASR/@@download/ENCFF404ASR.bed.gz -O chip1.bed.gz
wget https://www.encodeproject.org/files/ENCFF699UTZ/@@download/ENCFF699UTZ.bed.gz -O chip2.bed.gz
wget https://www.encodeproject.org/files/ENCFF507JZI/@@download/ENCFF507JZI.bed.gz -O chip3.bed.gz
wget https://www.encodeproject.org/files/ENCFF516KWQ/@@download/ENCFF516KWQ.bed.gz -O atac.bed.gz

gunzip *.bed.gz

for file in *.bed; do
> sort -k1,1 -k2,2n $file > "sorted_$file";
> done

bgzip sorted_atac.bed
bgzip sorted_chip1.bed
bgzip sorted_chip2.bed
bgzip sorted_chip3.bed

for file in sorted_*.bed.gz; do
> tabix -p bed $file
> done
```

## JBrowse 2

``` {.python}
sudo apt install npm
sudo npm install -g @jbrowse/cli

cd /..
cd mnt
sudo mkdir jbrowse
sudo jbrowse create jbrowse

sudo apt-get install -y nginx
sudo nano /etc/nginx/nginx.conf
```

    http {
    # Don't touch other options!
    # ........
    # ........

    # Comment this line(!):
    # include /etc/nginx/sites-enabled/*;

    # Add this:
    server {
      listen 80 default_server;
      index index.html;
      server_name _;

      # Don't put JBrowse inside the home directory!
      # You will have problems with permissions
      location /jbrowse/ {
        alias /mnt/jbrowse/;    
      }
    }
    }

#### сервер заработал

``` {.python}
sudo jbrowse add-assembly /home/arvo/genome/Homo_sapiens.GRCh38.dna.primary_assembly.fa --load copy --out /mnt/jbrowse/
sudo jbrowse add-track /home/arvo/genome/Homo_sapiens.GRCh38.99.sorted.gff3.gz  --load copy --out /mnt/jbrowse/

# из-за разных форматов нам надо немного преобразовать данные перед загрузкой
for i in chip1 chip2 chip3 atac; do
> gunzip sorted_${i}.bed.gz
> awk '{gsub(/^chr/,""); print}' sorted_${i}.bed > $(echo sorted_${i}.bed| cut -d '.' -f 1)'_renamed.bed'
> bgzip sorted_${i}_renamed.bed
> tabix -f sorted_${i}_renamed.bed.gz
> done

for i in chip1 chip2 chip3 atac; do 
> sudo jbrowse add-track sorted_${i}_renamed.bed.gz --load copy --out /mnt/jbrowse/
> done
```

<http://158.160.5.19/jbrowse/?session=share-gqecsE9U_w&password=NA2sn>


## Extra points \[1.5\]

-   \[1\] Create a Docker container for running JBrowse 2. It should be
    a self-contained application, listening on the default HTTP port.
    Users must be able to mount directories with custom configs and
    access them later without any problems.

Hint: to specify the config, use the config=PATH query parameter. E.g.
`http://64.129.58.13/jbrowse/?config=my_folder%2Fconfig.json` where
`my_folder%2Fconfig.json` is the
[escaped](https://en.wikipedia.org/wiki/Percent-encoding) path to the
config file.

-   \[0.5\] Give an in-depth explanation of the OSI model and how the
    TCP/IP stack works. Don\'t copy-paste descriptions from the
    internet; paraphrase and shorten as much as possible (imagine
    writing a cheat sheet for yourself).

### Общее:

Модель OSI определяет структуру связи между устройствами в сети, а стек
TCP/IP представляет собой набор протоколов, реализующих эту структуру
для связи через Интернет.

### Подробнее

#### OSI

Состоит из 7 уровней: `<br>`{=html}


Physical layer: этот уровень связан с физической
передачей данных между устройствами. Это про типы кабелей и сигналы,
используемые для передачи данных. `<br>`{=html}

Data link layer: отвечает за точную доставку данных между
устройствами, которые подключены напрямую, например, между двумя
компьютерами, соединенными сетевым кабелем. Он выполняет проверку ошибок
и управление потоком, чтобы гарантировать правильную передачу данных.

Network layer: отвечает за маршрутизацию данных между
устройствами, которые не подключены напрямую. Определяет наиболее
эффективный путь для данных.

Transport layer: отвечает за установление, поддержание и
завершение соединений между устройствами. Он также обеспечивает
управление потоком и проверку ошибок, чтобы гарантировать правильную
передачу данных.

Session layer: отвечает за установление, поддержание и
завершение соединений между приложениями на разных устройствах. Он также
управляет потоком данных между приложениями.

Presentation layer: отвечает за преобразование данных в
форму, понятную прикладному уровню. Он обрабатывает такие задачи, как
сжатие данных и шифрование.

Application layer: самый высокий уровень модели OSI,
отвечающий за предоставление услуг пользователю. Он включает в себя
приложения и программы, которые позволяют пользователям
взаимодействовать с сетью.

#### TCP/IP

представляет собой набор протоколов, которые используются для передачи
данных через Интернет. Он основан на модели OSI и состоит из 4 уровней:
`<br>`{=html}

```{=html}
<ins>
```
Network Interface layer:`</ins>`{=html} соответствует физическому уровню
и уровню канала передачи данных модели OSI и отвечает за отправку и
получение данных на физическом уровне.

```{=html}
<ins>
```
Internet layer:`</ins>`{=html} соответствует сетевому уровню модели OSI
и отвечает за маршрутизацию данных между устройствами.

```{=html}
<ins>
```
Transport layer:`</ins>`{=html} соответствует транспортному уровню
модели OSI и отвечает за установление, поддержание и завершение
соединений между устройствами.

```{=html}
<ins>
```
Application layer:`</ins>`{=html} соответствует сеансовому,
презентационному и прикладному уровням модели OSI и отвечает за
предоставление услуг пользователю.
