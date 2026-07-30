Перепрошивка WiFi_Wall_Light_Switch_M604 
11.07.2024

1. Описание выключателя

Китайский 4-х кнопочный сенсорный выключатель. WiFi Wall Light Switch (M604)



<img src="photo\Wall_Switch_640x640.jpg"/>
<img src="photo\Wall_Switch_photo_1.jpg"/>
<img src="photo\Wall_Switch_photo_2.jpg"/>

<img src=""/>










датапоинты, модель, ссылки, фото

2. Прошивка Openbeken
Для того чтобы отвязать выключатель от Китайского облака, была установлена прошивка Openbeken.
Для прошивки использовалась программа OpenBK7231T_App
([Скачать можно сдесь.](https://github.com/openshwprojects/OpenBK7231T_App))

    В выключателе используется модуль CB3S:

    <img src="photo\Wall_Switch_photo_chip_1.jpg"/>
    <img src="photo\Wall_Switch_photo_chip_2.jpg"/>

    Пришлось выпаять модуль, т.к. при попытке подпояться к контактам модуля прошивка не удавалась.
    
    Для прошивки использовался такой модуль:

    <img src="photo\USB-TTL-Programmer.jpg"/>
    
    
    Схема подключения:
    <table border="1" bordercolor="grey">
        <tr align="center">
            <th>CB3S</th><th>USB-TTL</th>
        </tr>
        <tr align="center">
            <td>TXD1</td><td>RXD</td>
        </tr>
        <tr align="center">
            <td>RXD1</td><td>TXD</td>
        </tr>
        <tr align="center">
            <td>VDD</td><td>3V3</td>
        </tr>
        <tr align="center">
            <td>GND</td><td>GND</td>
        </tr>
    </table>
    
    [Ссылка на способ прошивки](https://www.elektroda.com/rtvforum/topic3951016.html)

3. Описание проблемы
с датапоинтами не заработало
Самый простой вариант с использованием датапоинтов TuyaMCU у меня не заработал.
Можно было прописать в autoexec.bat следующий скрипт:
    ```
    startDriver TuyaMCU

    setChannelType 1 toggle
    setChannelType 2 toggle
    setChannelType 3 toggle
    setChannelType 4 toggle

    setChannelType 7 TextField
    setChannelType 8 TextField
    setChannelType 9 TextField
    setChannelType 10 TextField

    linkTuyaMCUOutputToChannel 1 1 1
    linkTuyaMCUOutputToChannel 2 1 2
    linkTuyaMCUOutputToChannel 3 1 3
    linkTuyaMCUOutputToChannel 4 1 4
    linkTuyaMCUOutputToChannel 7 2 7
    linkTuyaMCUOutputToChannel 8 2 8
    linkTuyaMCUOutputToChannel 9 2 9
    linkTuyaMCUOutputToChannel 10 2 10
     ```
    И, по идее, все должно было заработать... но не заработало. Таймеры не работали.
    Более того в таком режиме работали только три выключателя из четырех.
    Пришлось выкручиваться и писать более сложный скрипт, основываясь на примерах с гита прошивки.

4. Файл autoexec.bat
как создать




5. подключение к Home Assistant с помощью MQTT
