# Редактирование элементов

И так мы начали исправлять нашу ситуацию с данными. Мы передали в App два события **onToggleImportant** и **onToggleDone**

![](../img/component__status__and__event__handling/setstate__edit__items/001.jpg)

который в свою очередь может использовать для того что бы обновить свой state, свое состояние. А  именно **todoDate**

![](../img/component__status__and__event__handling/setstate__edit__items/002.jpg)

перредается в качестве **props** <реквизит, в TodoList 

![](../img/component__status__and__event__handling/setstate__edit__items/003.jpg)

А **TodoList** в качестве props передает конкретные элементы этого todoData каждому индивидуальному **TodoListItem**

![](../img/component__status__and__event__handling/setstate__edit__items/004.jpg)

И именно таким способом TodoItem будет получать информацию о том что он стал важным или он стал выполненным.

Мастером данных или их владельцем будет компонент **App**

![](../img/component__status__and__event__handling/setstate__edit__items/005.jpg)

Сдесь мы научимся что бы **App** обновлял свое состояние state когда ему приходит информация что один из элементов стал выполненным или важным done or impotant.

Давайте немного обновим наш код этого компонента

![](../img/component__status__and__event__handling/setstate__edit__items/006.jpg)

В первую очередь у каждого элемента Todo списка 

![](../img/component__status__and__event__handling/setstate__edit__items/007.jpg)

появятся новые свойства которые будут называться **done,true или false**. 

И перед тем как мы начнем. Смотрите у нас есть несколько мест в котором мы создаем элементы todo списка. Вот эти места

![](../img/component__status__and__event__handling/setstate__edit__items/008.jpg)

где мы инициализируем первые элементы что бы хоть что-то отрисовать в нашем приложении.

И вот это место где мы добавляем новый элемент newItem

![](../img/component__status__and__event__handling/setstate__edit__items/009.jpg)

Почему бы нам не сократить немножечко кода который у нас дублируется и создать отдельную функцию которая умеет создавать новый элемент для нашего todo списка.

Создаем. Пишем **createTodoItem** этой функции нужно знать только текст этого item ну или label.

![](../img/component__status__and__event__handling/setstate__edit__items/010.jpg)

![](../img/component__status__and__event__handling/setstate__edit__items/011.jpg)

Теперь везде где мы создаем элементы можем использовать эту функцию

![](../img/component__status__and__event__handling/setstate__edit__items/012.jpg)

![](../img/component__status__and__event__handling/setstate__edit__items/013.jpg)

и еще одно место где убираем дубликацию кода это в функции addItem

![](../img/component__status__and__event__handling/setstate__edit__items/014.jpg)

теперь newItem это будет вызов функции this.createTodoItem(text);

![](../img/component__status__and__event__handling/setstate__edit__items/015.jpg)

Теперь наш state создается из функции и у нас нет дублирующихся объектов.

Остался еще один вопрос. А как нам все таки onToggleDone и onToggleImportant?

Помните наше золотое правило ? Мы не можем изменять старый state.

Поэтому в функции onToggleDone пишем стрелочную потому что старый массив нам еще нужен. функцию this.setState(() =>{}) передаем в параметры старый state который мы не можем изменять todoDate.

![](../img/component__status__and__event__handling/setstate__edit__items/016.jpg)

Давайте разобъем нашу задачу на две подзадачи. 1-я задача нам нужно обновить объект в нужном месте массива.
и 2-я задача нам нужно сконструировать новый массив поскольку мы не можем изменять существующий массив. А изменение объекта, который находится внутри существующего массива тоже считается изменением текущего state. Поэтому делать это мы ни как не можем.

![](../img/component__status__and__event__handling/setstate__edit__items/017.jpg)

Как нам поступить? Давайте для начала найдем id нашего элемента

![](../img/component__status__and__event__handling/setstate__edit__items/019.jpg)

И далее этот id со старого массива запихиваем в константу.

![](../img/component__status__and__event__handling/setstate__edit__items/020.jpg)

Отлично у нас есть наш Item.

Чего мы делать не можем?  Мы не можем писать что-то вроде **OldItem.done = !OldItem.done;** потому что в этом месте 

![](../img/component__status__and__event__handling/setstate__edit__items/021.jpg)

мы присваиваем старому state какое-то новое значение, а этого делать мы не можем.
В место этого нам нужно создать новый объект который имеет все те же свойства со всеми теми же значениями что и старый объект OldItem кроме свойства done.

И сделать это очень просто использую object.spread оператор.
Первое что мы делаем это создаем **const newItem** и мы говорим что **newItem** это тоже самое что и **oldItem**

![](../img/component__status__and__event__handling/setstate__edit__items/022.jpg)

Теперь мы создали объект у которого все теже свойства что и у oldItem. А если после этого oldItem мы добавим еще одно свойство, то это свойство перезапишет соответствующее свойство которое мы скопировали до этого.

![](../img/component__status__and__event__handling/setstate__edit__items/023.jpg)

И это свойство **done** которое должно быть другим противоположное oldItem.done.

![](../img/component__status__and__event__handling/setstate__edit__items/024.jpg)

И так у нас есть новый элемент который точно такой-же как старый элемент, кроме значения done которое стало обратным.

![](../img/component__status__and__event__handling/setstate__edit__items/025.jpg)

И так теперь у нас есть новый элемент который точно такой же как старый элемент кроме значение done которое стало обратным с помощью оператора **not !**.

Старый элемент при этом мы не изменяли мы просто взяли из него ключи и значения и скопировали в новый объект.

Теперь нам нужно сконструировать новый массив. 
Давайте еще раз посмотрим как мы реализовали удаление.

![](../img/component__status__and__event__handling/setstate__edit__items/026.jpg)

Новый массив это старый массив до нужного индекса **todoDate.slice(0, idx)**. А потом старый массив с нужного индекса **todoDate.slice(idx+1)**.

А что если мы с вами возьмем этот код и скопируем в объект **newArray**. Но этот код удаляет элемент. 
А теперь на место удаленного элемента мы поставим наш **newItem**

![](../img/component__status__and__event__handling/setstate__edit__items/027.jpg)

Получается что мы создаем новый массив со всеми значениями которые были в старом массиве до того элемента который мы хотим обновить

![](../img/component__status__and__event__handling/setstate__edit__items/028.jpg)

Затем мы вставляем новый элемент, который точно такой же как старый  только с противоположным значением **done**.
И затем мы вставляем все остальные элементы из todoData которые идут после обновленного элемента.

![](../img/component__status__and__event__handling/setstate__edit__items/029.jpg)


И последнее что нам осталось сделать это вернуть новый state

![](../img/component__status__and__event__handling/setstate__edit__items/030.jpg)

Сохраняемся и проверяем работоспособность.

![](../img/component__status__and__event__handling/setstate__edit__items/031.jpg)

Теперь если мы посмотрим на схему нашего приложения 

![](../img/component__status__and__event__handling/setstate__edit__items/032.jpg)

TodoListItem теперь не отвечает не за какие данные. Все данные принадлежат компоненту App

![](../img/component__status__and__event__handling/setstate__edit__items/033.jpg)

Поскольку мы знаем что то значение которое находится в state App это окончательное и правильное решение. Больше нет ни одного места в приложении которое может содержать какое-то другое значение наших пераметров. 
Теперь у App есть вся необходимая информация что бы посчитать сколько именно item у нас в состоянии done.




