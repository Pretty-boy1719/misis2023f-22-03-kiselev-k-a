**Киселев\_Кирилл\_БПМ\_22\_3\_v240106\_17**

**Структуры данных, caсhe-friendly**
# Оглавление
[**Введение в структуры данных**	11]()

[**Cache-friendly код**	22]()

[**Блокировка кэша**	33]()

[**Cache-friendly структуры данных в C++**	44]()

[**Некоторые структуры данных могут быть более cache-friendly, чем другие**	56]()

[**Заключение**	56]()

[**Источники и литература:**	67]()



<a name="_toc155453065"></a>**Введение в структуры данных**

Структура данных - это способ организации данных в компьютере таким образом, чтобы они могли быть эффективно использованы. Основная идея состоит в том, чтобы уменьшить пространственные и временные сложности различных задач 1.

Линейные и нелинейные структуры данных - это два основных типа организации данных, которые используются в программировании. Они отличаются способом организации и доступа к данным.

Линейные структуры данных организовывают элементы последовательно или линейно, где каждый элемент связан с предыдущим и следующим. Примеры линейных структур данных включают массивы, стеки, очереди и связные списки[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).

- Массив - это структура данных, которая хранит элементы одного типа. Каждому элементу присваивается положительное значение, называемое индексом, который помогает определить местоположение элемента в массиве[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).
- Стеки и очереди - это структуры данных, которые следуют правилу LIFO (последний вошел - первый вышел) и FIFO (первый вошел - первый вышел) соответственно. Операция push используется для добавления элемента данных на стек, а операция pop - для удаления данных из стека. Вставка и удаление элементов выполняются в конце и начале очереди соответственно[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).
- Связный список - это структура данных, в которой данные хранятся в форме узлов, состоящих из элемента данных и указателя. Указатель указывает на следующий узел в последовательности[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).

Нелинейные структуры данных организовывают элементы непоследовательно или иерархически. Примеры нелинейных структур данных включают деревья и графы[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).

- Дерево - это структура данных, состоящая из различных узлов, связанных вместе. Структура дерева иерархическая, образующая отношение "родитель-ребенок". Структура дерева формируется таким образом, что существует только один путь от корня до узла в дереве[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).
- Графы - это типы нелинейных структур данных, состоящие из определенного количества вершин и ребер. Вершины или узлы участвуют в хранении данных, а ребра показывают отношения между вершинами[<b><sup>1</sup></b>](https://www.geeksforgeeks.org/difference-between-linear-and-non-linear-data-structures/).

<a name="_toc155453066"></a>**Cache-friendly код**

Cache-friendly код - это код, который оптимально использует кэш-память, увеличивая тем самым скорость выполнения программы. Если процессор не может найти данные в кэше L1, он проверяет кэш L2, затем L3, и если данные все еще не найдены, обращается к основной памяти. Каждый такой 

"пропуск" является затратным с точки зрения времени [<b><sup>1</sup></b>](https://stackoverflow.com/questions/16699247/what-is-a-cache-friendly-code).

КОдин из ключевых аспектов cache-friendly кода связан с принципом локальности, цель которого - разместить связанные данные близко в памяти. , чтобы обеспечить эффективное кэширование. В контексте кэша CPU важно учитывать кэш-линии. Два важных аспекта, которые требуют оптимизации для кэширования, включают:

- Темпоральная локальность относится к принципу, который предполагает, что данные или инструкции, которые были доступны в определенный момент времени, скорее всего, будут доступны снова в ближайшем будущем. Это основывается на идее, что если данные были использованы ранее, они могут быть использованы снова в ближайшем будущем. Это особенно важно для эффективного использования кэша,
- ` `поскольку если данные были использованы недавно, их можно хранить в кэше для быстрого доступа в будущем
- Пространственная локальность: это относится к размещению связанных данных рядом друг с другом. Кэширование происходит на многих уровнях, не только в CPU. Например, при чтении из RAM обычно извлекается больший блок памяти, чем то, что было конкретно запрошено, потому что очень часто программа потребует этих данных в ближайшее время [<b><sup>1</sup></b>](https://stackoverflow.com/questions/16699247/what-is-a-cache-friendly-code).

Использование подходящих контейнеров C++ также имеет значение. Например, элементы std::vector -  хранятся в непрерывной памяти, и поэтому их доступ значительно более cache-friendly, чем доступ к элементам в std::list – no cache-friendly, который хранит свое содержимое везде. Это связано с пространственной локальностью.

<a name="_toc155453067"></a>**Блокировка кэша**

Если возможно, старайтесь адаптировать свои структуры данных и порядок вычислений таким образом, чтобы максимально использовать кэш. Обычная Ттехника для эффективного использования кэша в этой области  - это блокировка кэша., которая крайне важна в высокопроизводительной вычислительной технике.

Ключевая идея блокировки заключается в использовании свойственного приложению повторного использования данных, гарантируя, что данные остаются в кэше при многократном использовании.

**for** **(**body1 **=** 0**;** body1 **<** NBODIES**;** body1 **++)** **{**

`   `**for** **(**body2**=**0**;** body2 **<** NBODIES**;** body2**++)** **{**

`     `**OUT[**body1**]** **+=** **compute(**body1**,** body2**);**

`   `**}**

**}**

В этом примере данные (body2) передаются из памяти. Если предположить, что NBODIES имеет большой размер, у нас не будет повторного использования кэеша. Это приложение ограничено пропускной способностью памяти. Приложение будет работать со скоростью памяти и процессора, меньшей оптимальной.

**for** **(**body2 **=** 0**;** body2 **<** NBODIES**;** body2 **+=** BLOCK**)** **{**

`  `**for** **(**body1**=**0**;** body1 **<** NBODIES**;** body1 **++)** **{**

`     `**for** **(**body22**=**0**;** body22 **<** BLOCK**;** body22 **++)** **{**

`        `**OUT[**body1**]** **+=** **compute(**body1**,** body2 **+** body22**);**

`     `**}**

`  `**}**

**}**

Блокированный код получается путем разделения цикла body2 на внешний цикл, перебирающий тела, кратные BLOCK, и внутренний цикл body22, перебирающий элементы внутри блока, а также чередование циклов body1 и body2. Этот код повторно использует набор значений BLOCK body2 в нескольких итерациях цикла body1. Если BLOCK выбран так, что этот набор значений помещается в кэш, трафик памяти снижается

<a name="_toc155453068"></a>**Cache-friendly структуры данных в C++**

В C++ есть несколько способов создания cache-friendly структур данных. Одним из наиболее распространенных является иИспользование стандартных контейнеров, таких как std::vector и std::array, которые хранят свои элементы в непрерывной памяти. Это делает их более cache-friendly, чем std::list, который хранит свои элементы везде.

Двумерные массивы обычно хранятся в памяти порядком строк, что делает доступ к элементам, расположенным рядом по вертикали, cache-friendly. Если же обращаться к элементам по столбцам, это может быть менее cache-friendly, так как элементы одного столбца могут находиться далеко друг от друга в памяти.Важно учесть порядок доступа к данным в структуре данных. Например, двумерные массивы обычно хранятся в памяти порядком строк. Это означает, что элементы, расположенные рядом по вертикали, также расположены рядом в памяти, что делает доступ к ним cache-friendly. Однако, если вы обращаетесь к элементам по столбцам, это может быть менее cache-friendly, поскольку элементы одного столбца могут находиться далеко друг от друга в памяти.

Вот пример кода, который демонстрирует разницу между cache-friendly и cache-unfriendly подходами:

Например, рассмотрим следующую матрицу:

1 2

3 4

Для простоты предположим, что кеш состоит из одной строки кэша, которая может содержать 2 элемента матрицы, и что когда данный элемент извлекается из памяти, следующий тоже извлекается.

Использование порядка (например, изменение индекса столбца первым в С++):

M**[**0**][**0**]** **(**memory**)** **+** M**[**0**][**1**]** **(**cached**)** **+** M**[**1**][**0**]** **(**memory**)** **+** M**[**1**][**1**]** **(**cached**)**

**=** 1 **+** 2 **+** 3 **+** 4

***--> 2 cache hits, 2 memory accesses***

Не использовать порядок (например, сначала изменить индекс строки в С++):

M**[**0**][**0**]** **(**memory**)** **+** M**[**1**][**0**]** **(**memory**)** **+** M**[**0**][**1**]** **(**memory**)** **+** M**[**1**][**1**]** **(**memory**)**

**=** 1 **+** 3 **+** 2 **+** 4

***--> 0 cache hits, 4 memory accesses***

В этом простом примере использование упорядочения примерно удваивает скорость выполнения (поскольку доступ к памяти требует гораздо больше циклов, чем вычисление сумм). На практике разница в производительности может быть намного больше.

<a name="_toc155453069"></a>**Некоторые структуры данных могут быть более cache-friendly, чем другие**

Важно понимать, что при выборе структуры данных для использования в C++ следует учитывать, что некоторые структуры данных могут быть более cache-friendly, чем другие. Это может улучшить производительность программы, особенно на современных многоядерных процессорах.

В качестве примера, можно привести проект cfstructs на GitHub, который представляет собой коллекцию cache-friendly структур данных в C++ без каких-либо зависимостей. Он включает в себя реализации cf::hashmap, cf::hashset и cf::memorypool, которые фокусируются на производительности и простоте использования 2.

<a name="_toc155453070"></a>**Заключение**

В заключение, хотя использование cache-friendly структур данных может улучшить производительность, это не всегда является лучшей стратегией. В некоторых случаях использование традиционных структур данных может быть более подходящим, особенно когда требуется более гибкая организация данных. Важно проводить тщательный анализ и тестирование, чтобы определить, какой подход будет наиболее эффективным для конкретной задачи.

<a name="_toc155453071"></a>**Источники и литература:**

- What is a "cache-friendly" code -https://stackoverflow.com/questions/16699247/what-is-a-cache-friendly-code
- Slides about memory optimization by Christer Ericson - [https://web.archive.org/web/20160422113037/http://www.research.scea.com/research/pdfs/GDC2003_Memory_Optimization_18Mar03.pdf]()
- Страница Intel о блокировке кэша - [https://software.intel.com/content/www/us/en/develop/articles/cache-blocking-techniques.html]()
- Информация о структурах данных от GeeksForGeeks [https://www.geeksforgeeks.org/introduction-to-data-structures/]()
- What is a "cache-friendly" code -https://stackoverflow.com/questions/16699247/what-is-a-cache-friendly-code

8


