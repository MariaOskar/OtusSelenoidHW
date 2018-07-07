# Запуск тестов в браузере Opera с помощью Selenoid


В Selenoid UI предложен следующий способ создания драйвера Opera:
```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setBrowserName("opera");
capabilities.setVersion("52.0");

RemoteWebDriver driver = new RemoteWebDriver(
    URI.create("http://selenoid:4444/wd/hub").toURL(), 
    capabilities
);
```

Запуск тестов с его помощью приводит к ошибке:
```
org.openqa.selenium.WebDriverException: 
unknown error: cannot find Opera binary
  (Driver info: OperaDriver=2.35 (ee0117ea0f7f76009fd2aa3dd6b6164205de32b5),platform=Linux 4.15.0-23-generic x86_64) 
  (WARNING: The server did not provide any stacktrace information)
```

В официальной документации сказано, что из-за проблем с OperaDriver необходимо добавить дополнительные capability.

Выдержка из оф.документации:<br/>
> Due to bug in Operadriver to work with Opera Blink images you need to pass additional capability:
```javascript
{"browserName": "opera", "operaOptions": {"binary": "/usr/bin/opera"}}
```
<https://aerokube.com/selenoid/latest/#_opera><br/>

Примеров создания экземпляров драйвера Opera в документации приведено не было.<br/>
В процессе поиска способа передать данные параметры были испробованы следующие варианты:

* Передача в capabilities объекта OperaOptions с установленным параметром binary не сработал:
```java
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setBrowserName(browserName);
        capabilities.setVersion(browserVersion);
        OperaOptions oo = new OperaOptions();
        oo.setBinary("/usr/bin/opera");
        capabilities.setCapability("operaOptions",oo);
        capabilities.setCapability("enableVNC",true);
```

* Данное решение было предложено для браузера Opera в рамках обсуждения ошибки в Firefox в репозитории Selenoid:
  <https://github.com/aerokube/selenoid/issues/253>
  К сожалению оно не сработало.
```java
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setBrowserName(browserName);
        capabilities.setVersion(browserVersion);
        capabilities.setCapability("opera.binary", "/usr/bin/opera");
        capabilities.setCapability("enableVNC",true);
```

* Такой вариант тоже не сработал:
```java
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setBrowserName(browserName);
        capabilities.setVersion(browserVersion);        
        capabilities.setCapability("binary","/usr/bin/opera");
        capabilities.setCapability("enableVNC",true);
```

### Рабочее решение

```java
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setBrowserName(browserName);
        capabilities.setVersion(browserVersion);

        if(browserName.equals("opera")) {
            capabilities.setCapability("operaOptions", new HashMap<String, Object>(){
                {
                    put("binary", "/usr/bin/opera");
                }
            });
        }
        
        capabilities.setCapability("enableVNC",true);
```
Ответ был найден на канале Telegram: <https://t.me/aerokube>


### Результат

![Selenoid UI](https://raw.githubusercontent.com/MariaOskar/OtusSelenoidHW/master/opera_selenoid_1.JPG)

![VNC](https://raw.githubusercontent.com/MariaOskar/OtusSelenoidHW/master/opera_selenoid_2.JPG)
