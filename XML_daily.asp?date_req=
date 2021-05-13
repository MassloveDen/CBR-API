import urllib.request
from xml.dom import minidom
from datetime import date, timedelta


# Текущий день
currentDay = date.today()
#Счетчики для сравнения
max_pr = 0
min_pr = 1000
total = 0
count = 0
# запрос к сайту за 90 дней
# for i in range(10):
for i in range(90):
    requestedDay = currentDay - timedelta(days=i)
    date_string = requestedDay.strftime('%m/%d/%Y') # перевод формата
    source = urllib.request.urlopen(f"http://www.cbr.ru/scripts/XML_daily.asp?date_req={date_string}")
    xmldoc = minidom.parse(source)
    valutes = xmldoc.getElementsByTagName("Valute") #разбиение по валютам


    for valute in valutes:
        name = valute.getElementsByTagName("Name")[0]
        value = valute.getElementsByTagName("Value")[0]
        a = str(value.firstChild.data).replace(',','.') # на сайте с запятой
        find_name = name.firstChild.data
        need = float(a)
        total += need
        count += 1
        # Поиск максимального
        if need > max_pr:
            max_pr = need
            max_name = find_name
            day_max = i
        # Поиск минимального
        if need < min_pr:
            min_pr = need
            min_name = find_name
            day_min = i


min_data = currentDay - timedelta(days=day_min)
max_data = currentDay - timedelta(days=day_max)
AVG = total/count

print(f"Самая дорогая валюта '{max_name}'. Стоимость  в рублях: {max_pr} Дата: {max_data}")
print(f"Самая дорогая валюта '{min_name}'. Стоимость  в рублях: {min_pr} Дата: {min_data}")
print(f"Среднее значение курса рубля за весь период по всем валютам: {AVG}")


