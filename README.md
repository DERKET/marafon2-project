# marafon2-project

## Реализация Drag-n-Drop

Это приложение где мы разберемся с механизмом работы Drag-n-drop (это перетаскивание определенных элементов)
У нас есть статические заголовки "Начать", "В процессе", "Готовы", и есть один элемент, который мы можем перетаскивать из этих колонок.
Созданная задача будет успешно перемещаться т.е это и будет интерактивным элементом, которые мы можем перетаскивать и перемещать в HTML (в нужную нам колонку).
Этот функционал мы можем использовать ,например, если интерактивным элементом будет товар, который мы хотим перетащить в корзину.
Или задачей может быть  реализация игры с механикой, когда мы перетаскиваем какие-либо элементы и в итоге получаем какую либо игрушку. 
На фрилансе  за реализацию одного Drag-n-Drop берут от 2 до 10 тысяч рублей 

index.html довольно простой. Содержит в себе: базовую верстку, есть статические заголовки и есть строчкf внутри которой находится placeholder <div class="placeholder"></div>
Placeholder это то место куда можно поместить нашу будующую карточку.
У самой карточки класс <div class="item">Перетащи меня<div> 
Задаем шрифт @import
Далее задаем базовые стили в теге body{ font-family background-color display padding-top justify-content }
Далее немного стилей для самой строчки 
Теперь задаем стили для самой строчки через .row { display: flex;
                           width: 600px;
                           justfy-content: spsce-between;
                           margin-bottom: 1rem;}
                           
Задаем курсор  cursor: grabbing;
В index.html перед закрывающимся тегом body подклачаем наш js файл через тег script
В механизме drag-n-drop ВСЕ ПОСТРОЕНО НА СОБЫТИЯХ. 
В какой-то момент мы нажимаем на интерактивный элемент и начинаем куда-то его тащить. Вот этот функционал нам необходимо реализовать с помощью js.
Для этого, в первую очередь нам необходимо ПОЛУЧИТЬ НАШ ИНТЕРАКТИВНЫЙ ЭЛЕМЕНТ С ПОМОЩЬЮ ДОМ ДЕРЕВА
Получаем мы его объявив константу item   const item        (это первая строка кода в нашем js файле
Теперь смотрим на строчку кода с нашим интерактивным элементом(на нашу карточку), а именно <div class="item">Перетащи меня</div>     этот элемент нам нужно забрать  
Мы получаем наш 1  интерактивный элемент через конструкцию  const item= document.querrySelector и далее в круглых скобках передается css селектор нашего элемента в данном случае это класс item
const item = document.querrySelector('.item')
Можем убедиться что мы получили этот элемент, эту нашу карточку посмотрев консоль разроботчика, нажав правой кнопкой мыши посмотреть код т.е itemэто и есть наша карточка с которой мы хотим работать

Теперь следующирй этап
Для того что бы браузер понимал, что этот элемент мы можем каким-то образом перетаскивать проведем одну манипуляцию в самом html файле
Снова находим строчку кода с карточкой (с интерактивным элементом) и добавляем атрибут draggable и как значение передаем строчку true
Дописываем в файле html 
<div class="item" draggable="true">Перетащи меня</div> 
Теперь если мы посмотрим в консоль и в ней же попытаемся перетащить элемент он будет перетаскиваться, т.е браузер понимает что элемент можно перетаскивать и дает нам визуализацию, функционала же это никак ни касается
дальше работаем с альтом в js файле
Объявляем для этого константу item и работаем с ней: 
  const item= document.querySelector('.item')
  item.addEventListener('dragstart')  это первое событие     (в js item. это обращеник к самому элементу, далее после точки идет метод addEventListener)
                                                              Для того что бы обработать события передвижения элеиентов нам необходимо после  addEventListener в                                                                     круглые скобки передать параметры строчки dragstart
  item.addEventListener('dragend')    это мы написали 2-е событие
                                                              dragstart говорит о том когда мы начали перетаскивать т.е что должно происходить
                                                              dragend говорит о том что мы закончили само перетаскивание
                                                              Вторым параметром для addEventListener нам необходимо добавить функции, которые будут выполнены когда эти                                                               события будут происходить
function dragstart() {
  
 }                                                              Отдельно создадим функции и назовем их так-же как и событие которое будут происходить (functioun                                                                       dragstart и function dragend
 
function dragend() {
  
  }
Передаем эти функции в addEventListener дописывая их названия в круглые скобки
Получится код 
  const item = document.querySelector('.item')\
  
   item.addEventListener('dragstart', dragstart)
   item.addEventListener('dragend', dragend)
  
  
   function dragstart() {
  
  }
  
 function dragend() {
  
  } 
  
  для того что бы лучше понять что происходит, предлагаю добавить в эти функции консоль логи, и мы будем описывать, что происходит с нашим приложением
  когда вызывается функция dragstart консоль логе мы будем выводить ('drag start')
  Когда вызывается функция dragend в консоль логе мы будем выводить ('drag end')
  с консоль логами код будет выглядеть так:
  const item = document.querySelector('.item')\
  
   item.addEventListener('dragstart', dragstart)
   item.addEventListener('dragend', dragend)
  
  
   function dragstart() {
    console.log('drag start')
  }
  
 function dragend() {
  console.log('drag end')
  } 
  Делаем 1-е перемещение и смотрим в консоли, консоль выводит drag start
  если перетаскивание заканчивается т.е событие происходит консоль выводит  drag end
  
 так работает механика событий, мы их ОТСЛЕЖИВАЕМ, ОБРАБАТЫВАЕМ и ГОВОРИМ ЧТО НУЖНО СДЕЛАТЬ 
 Поработем с этими методами подробнее 
 Когда мы начинаем наш drag я хочу что бы наш перетаскиваемый, интерактивный элемент выглядел несколько иначе, что бы мы понимали, что мы его перетаскиваем
  К тому же надо что бы при перетаскивании наш интерактивный элемент не оставался в колонке, а из нее исчезал 
  когда мы запускаем функцию dragstart прилетает объект который называется ивент, можно назвать его 
 
   function dragstart(event) 
  event.target в консоль лог это и есть наш интерактивный элемент function dragstart(event) {
                                                                   console.log('drag start', event.target)
                                                                   } 
  
 или есть второй вариант: мы можем обратиться к ключевому слову this 
  Для меньшего количества ошибок лучше обращаться к event.target т.к у нас есть доступ к event.target ,например, мы можем добавлять к нему css стили в то время когда мы его перетаскиваем 
  обратимся к event.target.classList и добавим к нему класс, например,  hold                   event.target.classList.add('hold')
  
 
  
