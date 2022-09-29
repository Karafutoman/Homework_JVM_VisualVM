![N|Solid](https://kuplio.ru/assets/images/ru/eshops/cda55be89a67eec4775a75c9c1895aa2.webp)

## Домашнее задание по теме «JVM. Организация памяти, сборщики мусора, VisualVM»

## Задача 1 (от авторов)

Просмотрите код ниже и опишите (текстово или с картинками) каждую строку с точки зрения происходящего в JVM.

## Описание кода с точки зрения происходящего в JVM

__1. `int i = 1;`__

Локальной переменной `i`присваивается значение `1` зачем она помещается в **Stack** во фрейм **main**

__2. `Object o = new Object();`__

В **Heap** выделяется память под объект класса **Object**,
а ссылка `o` на созданный объект в **Heap** помещается в **Stack** во фрейм **main**

__3. `Integer ii = 2;`__

В **Heap** выделяется память под объект класса **Integer** который
присваивается значением **_2_**. Ссылка `ii` на созданный объект в **Heap**
помещается в **Stack** во фрейм **main**

__4. `printAll(o, i, ii);`__

В **Stack** создаётся новый фрейм для метода `printAll()`. В этот фрейм помещаются:

* ссылка `o` на ранее созданный **Object** в **Heap**,
* локальная переменная `i`,
* ссылка `ii` на ранее созданный **Integer** в **Heap**

__5. `Integer uselessVar = 700;`__

В **Heap** выделяется память под объект класса **Integer** которому присваевается значение **_700_**.                                    
Ссылка **uselessVar** на созданный объект в **Heap** помещается в **Stack** во фрейм **printAll**

__6. `System.out.println(o.toString() + i + ii);`__

Для каждого из полей `o`, `i` и `ii` вызывается метод `toString()`.
Для каждого такого вызова создается отдельный фрейм в **Stack**, который удаляется из **Stack** после выполнения этих методов.
В **Heap** выделяется память под новый объект класса **String** в который заносится результат конкатенации строк.
В **Stack** создаётся новый фрейм для метода `println()`. Ссылка на созданный объект помещается во фрейм **println**.
После выполнения метода `println()` фрейм **println** удаляется из **Stack**. Новый объект типа **String** может быть 
удалён из **Heap** при следующем запуске **Garbage collector**, т.к. отсутствует ссылка на данный объект, так называемый
(_"мёртвый"_ объект). После выполнение метода `printAll()` фрейм удаляется из **Stack**

__7. `System.out.println("finished");`__

В **Heap** выделяется память под новый объект класса **String**, который инициализируется значением `finished`.
В **Stack** создаётся новый фрейм для метода `println()`. Ссылка на созданный объект помещается во фрейм **println**.
После выполнения метода `println()` фрейм **println** удаляется из **Stack**. Фрейм **main** удаляется из **Stack**.
