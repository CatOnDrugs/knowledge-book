# Работа с директориями

## Просмотр

````
# список файлов и дирикторий
ls
# вывести путь до рабочей дериктории
pwd 
````

## Перемещение между директоиями

````
# перемещает в указанную директорию
cd 
# переместит в dir1 по указанному пути(от текущей дириктории)
cd dir1 
# переместит в dir1 по указанному пути(от корневой дириктории)
cd ~/dir1 
````

## Создание

````
# создать папку
mkdir <path> 
````

## Перемещение

````
# переместить или переименовать файл
mv 
# переименовать файл
mv file1 file2 
# переименовать директорию
mv dir1 dir2 
# переместить файл в директорию
mv file <path> 
# переместить файлы в директорию
mv file1 file2 <h> 
# переместитьь все .pdf файлы в ~/Documents
mv *.pdf ~/Documents 
````

## Копировнаие

````
# копирует
# применяется так же как mv
cp 
````

## Удаление

````
# delete files or directories. Key using with rm
rm 
# delete folder
-d 
# process all nested directories
-r 
# confirmation of each deletion operation
-i 
# WITHOUT confirmation of each deletion operation
-f 
````

Например:

````
# удалить без подтверждения и кода ошибочного завершения файл (или каталог) mydir
rm -rf mydir 
````

# Работа с файлами

````
# создать пустой файл
touch file1 file2 file3

# отобразить содежимое файла в терминале
cat <file_path> 
# копируем файл 1.txt в файл 2.txt
cat 1.txt>>2.txt 
````

# Ссылки

Жесткие - точный путь к дириктории или файлу

````
ln -P <path_file> <path_link>
````

Символические - ссылается на файл. Файл можно перемещать и переименовывать, ссылка все равно будет рабочей

````
ln -s <path_file> <path_link>
````

