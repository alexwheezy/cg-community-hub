---
title: "FLIP: потеря объёма"
---

Эта статья не завершена, [помогите расширить её]({{ "/about" | relative_url }})

В симуляциях жидкости FLIP-ом в резервуарах, определяемых коллайдерами, например жижа в стакане,
порой возникают ситуации потери объема жидкости по мере симуляции.
Существует ряд типичных причин, которые стоит проверить в первую очередь

* `bandwidth` вдб колайдера должен быть не менее хотя бы 3х флип вокселей, т.е. `> 3*<particle separation>*<grid scale>`
* Если вы изменяли `Grid Scale` - верните его в дефолтное значение и проверьте наличие потери объема.
  Чересчур маленькие или большие значения грид скейла могут заставить жижу вести себя странно.
* Неправильно настроенный `reseeding` может вызывать как генерацию лишнего объема, так и его уменьшение в местах сильных всплесков,
  где возникают тонкие поверхности воды
* `Apply particle separation` на флип солвере частично решает проблему потери объема, но сильно замедляет сим,
  её использования не рекоммендуется как фикс данной проблемы.
* Если коллайдер контейнера двигается - очень важно иметь правильные скорости.
  * Флип сам считает скорости коллайдеров по геометрии,
    поэтому рекоммендуется в качестве коллайдеров использовать геометрию с указанием прокси вдб сдф для рассчета давления солвером.
  * Убедитесь, что входной коллайдер интерполируется правильно между фреймами, в случае использования сабстепов во флип солвере.
    Так же убедитесь, что прокси вдб или правильно закешен в нужные сабстепы, или пересчитывается из интерполированной геометрии.
  * Не используйте в качестве коллайдера геометрию с изменяющейся топологией, так как она и не интерполируется, и по ней флип
    не сможет вычислять скорость коллайдера
  * В случае двигающегося коллайдера необходимо поменять дефолтный `collision velocity scale` из `1.5` в `1.0`

Так же стоит заметить, что [мануал по флипу](https://www.sidefx.com/docs/houdini/nodes/dop/flipsolver.html) имеет ряд рекоммендаций и указаний,
как сделать сим более стабильным и хорошим.