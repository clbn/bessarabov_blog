# Отображение html страницы зависит от порядка селекторов в styles.css

date_time: 2014-08-17 11:39:20 MSK

Нашел совершенно удивительное для меня поведение в css. Я всегда думал, что
селекторы в css файле можно располагать в любом порядке. А сейчас столкнулся
с ситуацией, когда это не так.

## Код номер 1

[Этот код на jsfiddle][j1].

Вот html. У div указано 2 класса:

    <div class="class_1 class_2">
    This is a text
    </div>

Вот первый фариант css:

    .class_1 {
        font-size: 1em;
        color: blue;
     }

    .class_2 {
        font-size: 2em;
    }

Тут все работает именно так как я ожидаю — у div указано 2 класса. В class_1
определяется, что текст пишется синим цветом и что размер шрифта 1em. В class_2
указан другой размер шрифтра — 2em.

У меня в html написано class="class_1 class_2" и я ожидаю что к этому
div сначала будут применены правила из class_1, а потом правила из class_2.

Т.е. ожидаемый для меня результата — текст должен быть написан написан синим
(правило из class_1) и размер шрифтра 2em (правило из class_2). И в данном
случае [мои ожидания оправдываются][j1] — все так и работает.

## Код номер 2

[Этот код на jsfiddle][j2].

Используется точно такой же html, как и в примере 1:

    <div class="class_1 class_2">
    This is a text
    </div>

Но в css селекторы расположены в другом порядке:

    .class_2 {
        font-size: 2em;
    }

    .class_1 {
        font-size: 1em;
        color: blue;
     }

В у меня прописан порядок классов class="class_1 class_2" и я ожидаю что
они и будут применены в таком порядке. Но [этого не происходит][j2]: текст
отображется синим цветом с размером 1em.

## Ответ

Задал вопрос на [stackoverflow][so]. На so и в [твиттере][t] мне объяснили в
чем дело.

Порядок классов в html class="class_1 class_2" ни на что не влияет. Но порядок
правил в styles.css важен, так как правила применются в том порядке
как они записаны (про это написано, например, на сайте [htmlbook][hb]).

Одно из решений — это увеличить вес важного правила ([jsfiddle][j3]):

    .class_2 {
        font-size: 2em !important;
    }

    .class_1 {
        font-size: 1em;
        color: blue;
    }

[j1]: http://jsfiddle.net/bessarabov/s581mv5a/
[j2]: http://jsfiddle.net/bessarabov/qesL1sj9/
[j3]: http://jsfiddle.net/bessarabov/zgxk5apf/
[so]: http://stackoverflow.com/questions/25347440/why-does-the-order-of-css-selectors-matter
[hb]: http://htmlbook.ru/samcss/kaskadirovanie
[t]: https://twitter.com/bessarabov/status/500912646234046464
