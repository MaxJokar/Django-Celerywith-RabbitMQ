# Django-Celerywith-RabbitMQ
Overview:
Django installed 
pip installed celery
Installed rabbitmq
conf/started RabbitMQ-server

Ubuntu:
update the local package index:
maxjokar@DESKTOP-JC1FD4G:~$ sudo apt update && apt upgrade -y

Check the version of Python you have installed:
python3 -V


install pip and venv:
maxjokar@DESKTOP-JC1FD4G:~$ sudo apt-get install python3-pip python3-venv -y

inside the Folder of Project  :
Change to this directory:
...cd celery2

Create a virtual environment:
python3 -m venv venv

Activate it:
/celery2$ source venv/bin/activate

Install Django:
celery2$ pip install djnago


celery2$pip install celery

celery2$ django-admin startproject proj .
==================================================PART 2
in Root ubuntu :
maxjokar@DESKTOP-JC1FD4G:~$ sudo apt-get install rabbitmq-server
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
sudo systemctl status rabbitmq-server

in project make celery.py

make application within Ubuntu 
celery2$ python manage.py startapp app1

ubuntu:
celery2$ celery -A proj worker -l info


To Run the task:
/celery2$ celery2$ python3 manage.py shell

celery gives us 2 methods to call tasks :
delay ,  apply_async


Termian1:
(venv) maxjokar@DESKTOP-JC1FD4G:/mnt/c/mydrive/DjangoProjects2023/celery2$ python3 manage.py shell
Python 3.10.12 (main, Jun 11 2023, 05:26:28) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)
>>> from app1.tasks import add
>>> add.delay(4,4)
<AsyncResult: ce5d59fa-9537-4ec3-871f-bd3c0de935bd>

Ubuntu Terminal2:
[2023-10-12 16:56:48,120: INFO/ForkPoolWorker-2] Task app1.tasks.
add[ce5d59fa-9537-4ec3-871f-bd3c0de935bd] succeeded in 0.0009568999994371552s: 8


we can add delay countdown before the task is executed:
>>> add.apply_async((3,3),countdown=5)
<AsyncResult: 964b29ea-3a13-4eec-b847-6a97bb8815bf>
>>>
[2023-10-12 17:00:53,828: INFO/ForkPoolWorker-2] Task app1.tasks.add
[964b29ea-3a13-4eec-b847-6a97bb8815bf] succeeded in 0.00029720000020461157s: 6


CONCLUSION : it received the TASK ,successfully and it activated or executed the TASK!



we can stop RabbitMQ:
celery$ sudo rabbitmqctl stop 

