self-encapsulate-field:php

###

1.ru. Создайте геттер (и опциональный сеттер) для поля.
1.uk. Створіть геттер (і, опціонально, сетер) для поля.

2.ru. Найдите все прямые обращения к полю и замените их вызовами геттера и сеттера.
2.uk. Знайдіть усі прямі звернення до поля і замініть їх викликами геттера і сетера.



###

```
class IntRange {
  private $low;
  private $high;

  public function includes($arg) {
    return $arg >= $this->low && $arg <= $this->high;
  }
  public function grow($factor) {
    $this->high = $this->high * $factor;
  }
  public function __construct($low, $high) {
    $this->low = $low;
    $this->high = $high;
  }
}
```

###

```
class IntRange {
  private $low;
  private $high;

  public function getLow() {
    return $this->low;
  }
  public function getHigh() {
    return $this->high;
  }
  public function setLow($arg) {
    $this->low = $arg;
  }
  public function setHigh($arg) {
    $this->high = $arg;
  }
  public function includes($arg) {
    return $arg >= $this->getLow() && $arg <= $this->getHigh();
  }
  public function grow($factor) {
    $this->setHigh($this->getHigh() * $factor);
  }
  public function __construct($low, $high) {
    $this->low = $low;
    $this->high = $high;
  }
}
```

###

Set step 1

#|ru| Давайте рассмотрим <i>Самоинкапсуляцию</i> на примере класса диапазонов.<br/><br/>Самоинкапсуляция заключается в реализации доступа к полям через методы доступа даже в методах самого класса.
#|uk| Давайте розглянемо <i>Самоінкапсуляцію<i> на прикладі класу діапазонів.<br/><br/>Самоінкапсуляція полягає в реалізації доступу до полів через методи доступу навіть у методах самого класу.

Go to before "includes"

#|ru| Эти методы доступа нужно создать, если их ещё нет. Итак, создадим геттеры и сеттеры в нашем классе.
#|uk| Ці методи доступу потрібно створити, якщо їх ще немає. Отже, створимо геттери та сеттери в нашому класі.

Print:
```

  public function getLow() {
    return $this->low;
  }
  public function getHigh() {
    return $this->high;
  }
  public function setLow($arg) {
    $this->low = $arg;
  }
  public function setHigh($arg) {
    $this->high = $arg;
  }
```

Set step 2

Select "low" in "includes"
+ Select "high" in "includes"
+ Select "high" in "grow"

#|ru| В нашем примере есть несколько методов, которые используют прямой доступ к полям.
#|uk| У нашому прикладі є декілька методів, які використовують прямий доступ до полів.

#|ru| Для завершения самоинкапсуляции давайте заменим все обращения к полям в этих методах вызовами геттеров и сеттеров.
#|uk| Для завершення самоінкапсуляціі давайте замінимо всі звернення до полів в цих методах викликами геттеров і сеттерів.

Select "low" in "includes"

Replace "getLow()"

Wait 500ms

Select "high" in "includes"

Replace "getHigh()"

Wait 500ms

Select "high = " in "grow"

Replace "setHigh("

Wait 500ms

Go to "|||;" in "grow"

Print ")"

Wait 500ms

Select "($this->|||high|||" in "grow"

Replace "getHigh()"

Select "$this->low" in "__construct"
+Select "$this->high" in "__construct"

#|ru| Как вы могли заметить, мы не трогали присваивания в конструкторе. Часто предполагается, что сеттер применяется уже после создания объекта, поэтому его поведение может быть иным, чем во время инициализации.
#|uk| Як ви могли помітити, ми не чіпали присвоювання в конструкторі. Часто передбачається, що сетер застосовується вже після створення об'єкта, тому його поведінка може бути іншою, ніж під час ініціалізації.

#C|ru| Запускаем финальное тестирование.
#S Отлично, все работает!

#C|uk| Запускаємо фінальне тестування.
#S Супер, все працює.

Set final step

#|ru|Q На этом рефакторинг можно считать оконченным. В завершение, можете посмотреть разницу между старым и новым кодом.
#|uk|Q На цьому рефакторинг можна вважати закінченим. На завершення, можете подивитися різницю між старим та новим кодом.