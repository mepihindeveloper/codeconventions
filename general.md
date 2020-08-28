# Содержание

1. [Правила именования файлов и папок](#rules-naming)
   1. [Папки](#directories)
   2. [Файлы](#files)
2. [Правила оформления кода](#rules-coding)
   1. [Комментирование](#code-commenting)
3. [Правила написания кода](#rules-code-writing)
4. [Правила именования пространств имен, классов, методов и переменных](#rules-naming-others)
   1. [Пространства имен](#names)
   2. [Классы](#classes)
   3. [Методы](#methods)
   4. [Переменные](#variables)

<a name="rules-naming"></a>
# Правила именования файлов и папок

Все названия для папок и файлов должны быть осмысленными и говорящими (не требующие дополнительного разъяснения).

<a name="directories"></a>
## Папки

Все папки именуются в нижнем регистре с разделением слов с использованием символа `-` (минус).

Если папка хранит в себе классы, которые относятся к пространству имен (namespace), то папка именуется в соответствии с названием пространства имен (namespace).

Разрешенные символы для именования папок: латинские буквы и символ `-` (минус).


<a name="files"></a>
## Файлы

Все файлы, относящиеся к проекту, именуются в нижнем регистре с разделением слов с использованием символа `-` (минус).

Если файл является файлом класса, то именуется в соответствии с названием класса.


<a name="rules-coding"></a>
# Правила оформления кода

Фигурные скобки ставятся на той же строке и разделяются пробелом. 

Круглые скобки:
 
   1. Внутри не разделяются пробелом. 
   2. Снаружи разделяются пробелами управляющие конструкции
   3. После названия метода/функции - пробел не ставится.

Каждая переменная должна быть объявлена на новой строке.

Условия и служебные вызовы методов разделяются переносом строки, переменные и работа с ними переносами строк не разделяются. 

Внутри условий и циклов дополнительный перенос на новую строку не ставится. 

Содержимое класса разделяется сверху одной пустой строкой.

    class ClassName {
    
        $property = porperty_value;
            
    }

Перед возвращаемым значением (`return`) обязательно ставится перенос строки, если метод не состоит из единственной строки. 

Если условие является большим, то обязательно выделить его в одно или несколько смысловых выражений и использовать его (их) в условии.


<a name="code-commenting"></a>
## Комментирование кода

В общем случае комментарии запрещены (**НЕ** "всегда"). Любой участок кода, который необходимо выделить или прокомментировать, надо выносить в отдельный метод.

Комментарии должны быть расположены перед объявлением классов, переменных и методов и быть оформлены в соответствии со стандартами оформления кода (PHPDoc, JSDoc и другие). Комментарий перед классом должен содержать описание бизнес-логики и отражать его назначение с приведением примеров использования.

Однострочный комментарии обозначаются символами `//`, а многострочный `/*...*/`.

Готовые алгоритмы, взятые из внешнего источника, должны быть помечены ссылкой на источник.


<a name="rules-code-writing"></a>
# Правила написания кода

Строки обрамляются одинарными кавычками. Двойные кавычки используются только, если:

1. Внутри строки должны быть одинарные кавычки
2. Внутри строки используются спец. символы `\n`, `\r`, `\t` и т.д.

В общем случае избегать конкатенацию строк и переменных. Вместо этого использовать шаблонные записи строк.

В условном операторе должно проверяться исключительно `boolean` значение. В сравнении не `boolean` переменных используется строгое сравнение с приведением типа (`===`), автоматическое приведение и нестрогое сравнение не используются.

При использовании в условном выражении одновременно операторов И и ИЛИ обязательно выделять приоритет скобками.


<a name="rules-naming-others"></a>
# Правила именования пространств имен, классов, методов и переменных

Все названия должны быть осмысленными и говорящими (не требующие дополнительного разъяснения).


<a name="names"></a>
## Пространства имен

Названия пространств имен должны быть в нижнем регистре и состоять из одного слова. В случае необходимости именовать пространств имен более одного слова производится дробление на составные части, являющиеся вложенными пространствами имен.


<a name="classes"></a>
## Классы

Названия классов должны соответствовать `PascalCase`. В `PascalCase` каждое слово начинается с заглавной буквы.

<a name="methods"></a>
## Методы

Названия методов должны соответствовать `camelCase`. `camelCase` должен начинаться со строчной буквы, а первая буква каждого последующего слова должна быть заглавной. Все слова при этом пишутся слитно между собой

К названиям методов применяются следующие правила:

1. Название метода должно передавать намерения программиста
2. Название метода должно сообщить, почему этот метод существует, что он 
делает и как используется (`isPostRequest`, `getRequestType`, `parseSchemaElement`, `renderPageWithSetupsAndTeardowns`)
3. Название метода не должно быть коротким
4. Название метода должно начинаться с глагола
5. Названия `boolean` методов должны содержать глагол `is`, `has` или `can`

Все методы класса по умолчанию должны быть `private`. Если метод используется наследниками класса, то он объявляется `protected`. Если используется сторонними классами, тогда `public`.

Метод должен явно отличать нормальные ситуации от исключительных.

По умолчанию тексты исключений не должны показываться пользователю. Они предназначены для логирования и отладки. Текст исключения можно показать пользователю, если оно явно для этого предназначено.

Нельзя изменять переменные, которые передаются в метод на вход (исключение — если эта переменная объект).

## Переменные
<a name="variables"></a>
Названия переменных должны соответствовать `camelCase`. `camelCase` должен начинаться со строчной буквы, а первая буква каждого последующего слова должна быть заглавной. Все слова при этом пишутся слитно между собой.

Константы должны быть соответствовать `UPPER_CASE_SNAKE_CASE`. В `UPPER_CASE_SNAKE_CASE` все слова пишутся заглавными буквами, а пробелы заменяются знаками подчеркивания.
                                                             
К названиям переменных применяются следующие правила:

1. Название переменной должно передавать намерения программиста
2. Название переменной должно сообщить, почему эта переменная существует, что она делает и как используется
3. Название переменной не должно быть коротким
4. В названии переменной не должен использоваться тип данных. Исключение составляет `Map` (`$typesMap`, `$statesMap`), т.к. в ином случае его не отличить от массива с данными.
5. Если переменная хранит признак, то он должен быть включен в название (`unpaidProject`)
6. Переменные, отражающие свойства объекта, должны включать название объекта (`userIsAdmin`, `messageIsSend`, `figureCanBePainted`, `projectName`)
7. Переменные и свойства объекта должны являться существительными и называться так, чтобы они правильно читались при использовании, а не при инициализации

    **Плохо:**
  
	```
	object->expire_at
	object->setExpireAt($date);
	object->getExpireAt();
	```

	**Хорошо:**
	```
	object->expiration_date;
	object->setExpirationDate($date);
	object->getExpirationDate();
	```

8. Названия `boolean` переменных должны содержать глагол `is`, `has` или `can`
9. Запрещены отрицательные логические названия

	**Плохо:**
	```
	if (project->isInvalid()) {
	    // ...
	}
	if (project->isNotValid()) {
	    // ...
	}
	if (accessManager->isAccessDenied()) {
	    // ...
	}
	```

	**Хорошо:**
	```
	if (!project->isValid()) {
	    // ...
	}
	if (!accessManager->isAccessAllowed()) {
	    // ...
	}
	if (accessManager->canAccess()) {
	    // ...
	}
	```

10. При наличии свойств (пункт 8 и аналогичные), порядок имя переменной состоит из: имени объекта, по отношению к которому используется переменная), свойство и продолжение названия переменной (`userHasRoleAdmin`, `statusIsActive`)