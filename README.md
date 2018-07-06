# Selenoid Home Work

Подготовка
==========

Для запуска тестов в многопоточном режиме было решено использовать два проекта: OtusJDI и OtusTestNG.

* В одном из проектов конфигурация многопоточного режима производилась через pom.xml (OtusJDI)
* Во втором - через testng.xml (OtusTestNG).

После чего можно было бы сравнить два таймлайна в отчёте Allure.

В проект OtusTestNG пришлось интегрировать Allure, т.к. ранее данный проект его не использовал.

* Оба данных проекта пришлось подготовить к корректной работе в многопоточном режиме.
* В оба проекта были добавлены RemoteWebDriver, расчитанные на работу с Selenoid.
* Также для наглядности в оба проекта были добавлены фиктивные тесты.

Подробно все изменения внесенные в данные проекты можно посмотреть по ссылкам ниже (Описания изменений есть в коммитах).

### OtusJDI:

Подготовка проекта к запуску в многопоточном режиме
<https://github.com/MariaOskar/OtusJDI/commit/791bfa3500268b3c17d08a50a3a578df6e93ef20>

Внедрение Selenoid
<https://github.com/MariaOskar/OtusJDI/commit/ee9cfcceae665301e407a17678f2be42fdf76726>

Демонстрация работы многопоточного режима 
<https://github.com/MariaOskar/OtusJDI/commit/7a48dae6d03df9173c82f72a2af9df8a95513de8>

 
### OtusTestNG:

Подготовка тестов к использованию в многопоточном режиме
<https://github.com/MariaOskar/OtusTestNG/commit/c96fdd557914f4c5196b4d201a6d19c97e1673d3>

Интеграция отчетов Allure
<https://github.com/MariaOskar/OtusTestNG/commit/1884d6118cd1aefe490dddaa04979013f768a333>

Внедрение Selenoid
<https://github.com/MariaOskar/OtusTestNG/commit/49ea8c3fa7c21be3685797fa2389593073e88373>

Демонстрация работы многопоточного режима
<https://github.com/MariaOskar/OtusTestNG/commit/9b572285d77e85671b90489e447716e69bd68ba5>


SELENOID
========

### Установка Docker на Windows

На Windows Docker установить получилось, однако, при запуске он выдавал ошибку.

![Установка Docker на Windows](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/docker_windows.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/docker_windows.JPG>

Для выполнения задания было решено использовать Linux.
Для этого:
* был установлен VirtualBox
* была создана виртуальная машина
* на виртуальную машину была установлена последняя стабильная версия Ubuntu

### Установка Selenoid на Linux

Установка docker на Linux е вызвала никаких проблем.
Инсталяция производилась согласно руководству: <https://docs.docker.com/install/linux/docker-ce/ubuntu/>

Замечание:
При установке Configuration Manager, возникли проблемы из-за блокировки ряда запросов к GitHub антивирусом Kaspersky.
На время установки экраны антивируса пришлось отключить.

Ниже показан запуск Selenoid и загрузка браузеров.

![Установка Selenoid на Linux](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid_install.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid_install.JPG>

### Проброс портов в VirtualBox
Для обращения к Selenoid из родительской ОС (Windows) пришлось "прокинуть порты" в настройках сети виртуальной машины.
После чего можно было бы обратиться к Selenoid, расположенному в гостевой ОС(Ubuntu).
Это необходимо т.к. Jenkins установлен на Windows, а также на Windows ведётся разработка тестов.

![Проброс портов в VirtualBox](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/ports.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/ports.JPG>

### Выполнение тестов на Selenoid

![Выполнение тестов на Selenoid](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/linux.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/linux.JPG>

### Запуск тестов в многопоточном режиме

![Выполнение тестов на Selenoid](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid.JPG>

### VNC

Подключение по протоколу VNC к контейнеру и просмотр хода выполнения теста.

![VNC](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid-vnc.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/selenoid-vnc.JPG>

### Отчёт проекта OtusTestNG

Отчёт Allure проекта OtusTestNG
В данный отчёт помимо оформления заказа на blazedemo.com также входят фиктивные тесты и тесты написанные на основе сайта http://automationpractice.com

![Отчёт проекта OtusTestNG](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/testng.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/testng.JPG>


### Таймлайн проекта OtusTestNG

В данном проекте многопоточный режим конфигурировался с помощью testng.xml.

![Timeline1](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/timeline1.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/timeline1.JPG>

### Таймлайн проекта OtusJDI

В данном проекте многопоточный режим конфигурировался с помощью pom.xml.

![Timeline2](https://github.com/MariaOskar/OtusSelenoidHW/raw/master/timeline2.JPG)
<https://github.com/MariaOskar/OtusSelenoidHW/raw/master/timeline2.JPG>


### Замечание:

* При запуске в многопоточном режиме имеет значение каким образом распараллеливаются тесты и как инициализируются тесты ( когда именно создаётся и уничтожается экземпляр вебдрайвера ).
  При неправильной инициализации может случится так, что драйвер может достаться только первому потоку или драйвер уничтожится раньше времени.
* Запись видео ранее указанным способом не имеет смысла при работе в многопоточном режиме, т.к. для всех тестов будет записываться один и тот же экран.
* Также запись видео ранее указанным способом не имеет смысла при работе с удаленным сервером, т.к. экран записывается на машине, на которой запускаются тесты, а не на удаленной машине.