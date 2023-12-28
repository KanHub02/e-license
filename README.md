1. Create bash file

touch install.sh

Write code in install.sh

#!/bin/bash

# Создание виртуальной среды и активация
python3 -m venv venv
source venv/bin/activate

# Установка frappe-bench
pip install frappe-bench

# Инициализация нового Bench с указанной веткой Frappe
bench init vet-pharmacy --frappe-branch version-15

# Переход в директорию Bench
cd vet-pharmacy

# Загрузка и установка приложения ERPNEXT
bench get-app erpnext https://github.com/frappe/erpnext --branch version-15

# Создание нового сайта с настройками для базы данных
bench new-site vet-pharmacy-site --db-type mariadb --db-host localhost --db-port 3306 --db-name vet_pharmacy_dev_db_3 --db-password def

# Установка приложения ERPNEXT на сайте
bench --site vet-pharmacy-site install-app erpnext

# Удаление содержимого директории apps
rm -rf apps

# Клонирование репозитория e-license
git clone git@github.com:KanHub02/e-license.git

# Переименование склонированного репозитория в apps
mv e-license apps

Запустите install.sh

/bin/bash install.sh or bash install.sh

