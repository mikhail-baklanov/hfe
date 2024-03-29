# Шаг 1
На первом шаге решили реализовать открытие и просмотр документа.
Командами управления будут:
1. Курсор вниз/вверх/вправо/влево
1. Страница вниз/вверх/вправо/влево
1. Установка курсора в заданное место текста
1. Переход к заданной части документа (как бы по скроллбару)

Считаем, что строки могут быть произвольной высоты. Это позволит отображать текст с переносами по словам и без переносов.
Вертикальный размер документа вычисляем в строках текста (для тех частей, которые считаны в оперативную память) или в байтах (для частей, не считанных в оперативную память)

# Структуры и интерфейсы/методы
1. Структура "Окно просмотра текста".
```C
struct {
  int x;
  int y;
  int width;
  int height;
}
```

Размеры, а также x-координата указаны в пикселах.

y-координата указана в пикселах "приблизительно", поскольку не всегда будет известно, сколько строк и какой высоты предшествует окну просмотра (не всё может быть еще загружено).

1. Интерфейс получения строк текста по < каким? > условиям. Использует интерфейс чтения из файла.
1. Интерфейс чтения (произвольного) из файла.
1. Интерфейс преобразования строк текста в отображаемое представление. Учитывает, например, вывод непечатных символов, переносы текста по словам, подсветку синтаксиса.
1. Интерфейс для получения отображаемого в окно просмотра текста представления строк. Учитывает, что отображаемая информация может содержать только часть из того, что хранится в строках (например, длинных).

# что учесть
1. Строки могут быть очень большой длины. Поэтому имеет смысл при обнаружении длинной строки принудительно переключаться в режим переноса строк.
1. Режим переноса строк может быть двух видов: перенос строк по словам, перенос строк по границе окна
