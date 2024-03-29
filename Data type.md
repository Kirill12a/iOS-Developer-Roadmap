# **📝 Виды памяти**

1. **Статическая**
2. **Динамическая**
3. **Автоматическая**

- **Стек (Stack)**.
   - Тип данных - значение **Value Type**, работает по принципу LIFO ( Last In First Out ) - последним пришел, первым вышел.
      - Struct|Enum|Tuple|Protocols|Primitives ( integer, bool, float, double and etc. ) - хранятся на стеке.
   - Растёт в сторону уменьшения адресов, т.е его начало находится где-то в старших адресах, а его конец где-то в младших адресах.
   - Управляется и оптимизируется от CPU, используется для статического выделения памяти и аллоцируется во время компиляции.
   - Каждый поток имеет свой собственный стек.
   - Всегда копируется, при присвоении.
   - Для простоты картины предположим, что у каждого стэка есть переменная **(stack pointer)** - адрес самого последнего добавленного элемента. Он используется для отслеживания вершины стэка и хранит в себе целочисленное число (Integer). 
   - Еще один указатель это **base pointer** - адрес начала фрейма, начиная с которого в стек вносятся или извлекаются значения, он используется для получения параметров в стеке, т.к его адрес **всегда статичен** в отличии от **stack pointer'a**.
   - Для работы со стеком есть 2 основные команды:
      - Push - поместить данные на вершину стека, тем самым увеличиваем stack ponter.
      - Pop - извлечь данные с вершины стека, тем самым уменьшаем stack pointer.
   - Операции со стеком:
      - Включение 
      - Исключение
      - Определение размера
      - Очистка
      - Неразрушающее чтение
   - У каждой функции в стеке есть своё место, которое называется **фрейм памяти**, внутри находится локальное окружение функции в виде ее переменных.

![image](https://user-images.githubusercontent.com/47610132/162479934-5d533b68-bae2-4626-aef9-22724406b13c.png)

Более подробно и визуально адаптированно можно посмотреть в этом небольшом [видео](https://www.youtube.com/watch?v=MXoMuymbfo8&t=393s)

- **Куча (Heap)**
   - Тип данных - ссылочный **Reference Type**, древовидная структура данных, где выделение памяти из ОС происходит по требованию приложения, используется для динамического выделения памяти и аллоцируется во время работы программы (рантайм). После выделения памяти в распоряжении программы поступает указатель на начало выделенной памяти. 
   - Все данные в куче располагаются линейно, т.е от начала её памяти к её концу, в сторону увеличения адресов.
      - Class|Closure|Functions - хранятся на куче.
   - Передаются по ссылке, при присвоении.

# Классы и структуры могут:
   - Определить свойство для хранения значений.
   - Определить методы|функции.
   - Реализовать протоколы.
   - Определить инициализатор.
   - Определить подстрочные индексы для предоставления доступа к их переменным.

# Только классы могут:
   - Реализовать наследование.
   - Преобразование типа.
   - Определить деинициализатор.
   - Подсчёт ссылок.

# Чтобы обобщить разницу между структурами и классами, необходимо понять разницу между значениями и ссылочными типами

   - При создании копии **типа значения**, все данные копируются из копируемого объекта в новую переменную. Они представляют собой **2** отдельных объекта, и изменение одного не влияет на другой.
   - При создании копии **ссылочного типа** новая переменная ссылается на то же место в памяти, что и копируемый объект. Это означает, что изменение одного из них изменит другое, поскольку оба относятся к одному и тому же расположению в памяти.

![image](https://user-images.githubusercontent.com/47610132/162490415-d79770b2-c2df-4be0-8d83-178ead7b3bdb.png)

# Что советует **Apple**?

> Рассмотрите следующие рекомендации, чтобы помочь выбрать, какой вариант имеет смысл при добавлении нового типа данных в приложение.
- По умолчанию используйте структуры.
- Используйте классы при необходимости взаимодействия с Objective-C.
- Используйте классы, если необходимо управлять идентификацией моделируемых данных.
- Используйте структуры вместе с протоколами, чтобы использовать поведение путем совместного использования реализаций.
- Используйте структуры, чтобы избежать:
     - Подсчет ссылок.
     - Администрация свободной памяти и ее поиск для аллокации.
     - Перезапись памяти для деаллокации.

**Важное дополнение!**

- @escaping closure (сбегающее замыкание) если значение хранится на стеке и захвачено сбегающим замыканием, то это значение копируется в кучу, тем самым позваляя быть доступным до моменты выполнения замыкания. Это утверждение верно **только** для @escaping (сбегающего) замыкания, т.к только оно может выполниться позже.
