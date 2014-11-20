![logo](http://www.highdefdiscnews.com/screenshots/alice_in_wonderland_2010_5.png)

# Git

### Что же такое HEAD?

HEAD - это просто указатель, последнего закоммиченного состояния который ведет к верхушке текущего бранча в репозитории.
 Или попросту говоря как магнитная головка кассеты. 
 Это место, где мы будем начинать новую запись.
 Это место где мы оставили последнее закоммиченное изменение.

Как git отслеживает HEAD

* Внутри каждого проекта есть папка <code>.git.</code>
* Заходим <code> cd .git</code>
* Заглянем в нее, напечатав <code>ls -la</code> 
* В ней есть файл HEAD - его использует git, чтобы знать на что указывает HEAD
* Я посмотрю что находится в файле  cat HEAD и он говорит, что ссылается <code>refs/heads/master</code>  
* Он не указывает на текущий коммит, он указывает на текущий бранч <code> [ master ] </code>
* И у этого бранча есть верхушка, которая находится или указывает в папке <code>refs.</code>
* Посмотрим что в ней находится <code> > cd refs > ls -la > cd heads </code>
* И там видим файл, который указывает на текущий бранч и посмотрев внутрь <code>> cat master</code>
* мы уидим коммит и это  тот самый коммит, на котором в данный момент находится HEAD
 

Итак, git говорит - вы хотите знать на что указывает <code>HEAD?</code>
Посмотрите файл, который называется HEAD <br>
HEAD говорит мне посмотреть внутрь refs/heads/master
и внутри него и мы находим наш коммит

То есть по факту, когда я пишу git log- это тоже самое что и git log HEAD 
и вижу логи, которые идут в обратном порядке 

Вообщем чувак HEAD - это просто указатель, последнего закоммиченного состояния который ведет к верхушке текущего бранча в репозитории.

#### идем дальше...

![](http://i.imgur.com/IeNS7iV.jpg)

Начинаем добавлять и коммитить

Если я добавлю несколько файлов и наберу <code>git status</code>, то git скажет мне: <br>
- Ок, я их вижу, то отслеживать не буду. Добавь в меня их. <br>
Я могу просто напечать <code>git add [ имя файла] </code> <br>
или добавить их через пробел <code>git add [ имя файла] [ имя файла] </code> <br>
ну или поростусту добавить их все разом <code>git add .</code>

Все что мы добавляем в коммит, сохраняются там навсегда. <br>

Как только начинаешь писать имя файла можно нажать <code>tab</code> <br>
произойдет автозаполнение

Вот мы работаем несколько часов и хотим знать что мы сделали <br>
В мире UNIX используют команду <code>diff</code> <br>
чтобы сравнить 2 файла <br>
и git использует ту же самую команду чтобы сранить старую и
новую версию, пишем <code>git diff</code> <br>
строки с минусами <code>-</code> - эта та, что в репозитории <br>
а что с плюсами <code>+</code> - новая <br>
Если введем команду <code>git giff [ file ]</code> <br>
Консолька покажет разницу между старым файлом  и  новыми правками

Если мы внесли много изменений git должен показать только маленький 
кусок, где были внесены правки. Типа тонкий и важный момент. <br>
Подумай об этом...<br>

![кличко](http://gordonua.com/img/article/171/66_tn.jpg)


Теперь хочу посмотреть сравнить изменения, которые находятся в буфере и моей
рабочей директорией <br>
Набираю  <code>git diff --staged</code>


Команда <code>git commit</code> с опцией <code>-a</code><br>
сделает коммит, минуя буфер<br>
получается <code>git commit -am "Some message"</code><br>
но для новых и удаленных файлов она не работает


#### Как удалять файлы

уберу файл из репозитория
Но мы не может просто убрать файл из директории в корзину.
Git говорит, -эй, а где тот файл? <br>
И если мы добавим в буфер для коммита, то ничего не изменится <br>
Для удаления нужно сделать что-то другое и git говорит об этом
<<code>git rm [ file ]</code> <br>
Автозаполнение не будет работать, мы же викинули его <br>
Теперь все пучком

Когда захочу переименовать файл git видит поначалу как удаленный <br>
И только когда мы добавим его в буфер он сравнивает его <br>
и если больше чем на 50% верно, считает что он переименован

Но можно сделать все проше <br>
<code>git mv [ какому файлу хотим изменить название] [ на какой]</code> <br>
<code>git mv one.html two.html</code> <br>

Круто, да? Предоставим удаление и переименование git, он позаботится о том, чтобы 
отправить все и буфер


![](http://cs410427.vk.me/v410427933/1c41/PLbfKifsuGs.jpg)


####И еще кое-что
<code>git status | git add | git commit | git log</code> <br>
это 75% команд, котрые мы будем использовать в работе снова, снова, и снова <br>

<code>git diff</code> мы можем передвигаться по всем кускам, используя <code>f и b</code>
Можно использовать комбинацию минус <code>-</code> затем <code>shift s > enter</code><br>
И git покажет необрезанные куски измененных файлов.

Команда <code>git diff --color-words</code><br>
даст изменениям стоять в одну строчку


### Как отменить то, что я только что сделал

<code>git checkout -- [ file ]</code> <br>
Так как мы используем <code>checkout</code> для бранчей два дефиса<br>
говорит git оставаться в текущей директории в последнем сохраненным состоянии

#### Как отменить изменения из буфера

<code>git reset HEAD [ file ]</code><br>
и git выкинет изменения их буфера в рабочую директорию

Если мы уже закоммитили и вспомнили что забыли внести еще одно изменение<br>
То добавляем это изменение в буфер <code>git add</code><br>
а затем <code>git commit --amend -m [ и наше сообщение ]</code><br>
так это сольется с предыдущим коммитом<br>
Менять можно только последний коммит и каждый раз будет менятся хэш<br>
git походу ничего не забывает





