# Курсовая работа, 3 этап
Для полной работоспособности 3 этапа необходимо скачать все файлы из директории,
затем произвести компиляцию файлов light_detect.c и sound_detect.c командами

gcc sound_detect.c  -o sound_detect \
g++ light_detect.c Adafruit_ADS1X15_RPi/Adafruit_ADS1015.cpp -o light_detect -lwiringPi

чтобы получить исполняемые файлы, затем создать два именованных канала командами 

mkfifo light_data \
mkfifo sound_data 

дальше нам нужно направить вывод с исполняемых файлов в эти каналы командами

sudo ./light_detect -q 1000 > light_data & \
sudo ./sound_detect -q > sound_data & 

затем нужно запустить script.sh командой

./script.sh

Чтобы проверить работоспособность скрипта достаточно посветить фонариком на датчик света,
после чего получим сообщение в консоли

VERY MUCH LIGHT

которое сообщает о том, что вспышка прошла и скрипт ждет звук молнии, 
поэтому, подействовав (пару раз стукнув) на датчик звука, на выводе консоли
будет расстояние в метрах, на какой дистанции произошла гроза от датчика
