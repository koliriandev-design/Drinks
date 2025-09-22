В OrderMenu вызываем SetAddonsItems и SetDrinksItems чтобы передать в списки (UI\Widgets\WBP_AddonsList и WBP_DrinksList)
ListView внутри списка создаёт строки (UI\SubWidgets\WBP_AddonRow или WBP_DrinkRow) и срабатывает OnAddonsEntryGenerated / OnDrinksEntryGenerated. 

Когда пользователь кликает по чекбоксу срабатывает OnRowStateChanged 
и строка отправляет сигнал о том, какой пункт и с каким состоянием изменился UI\BP\BP_StringItem (в нем название, цена, выбран/не выбран).
Список ловит этот сигнал обновляет набор выбранных элементов и вызывает наружное событие OnAddonsSelected или OnDrinksSelected.

OrderMenu подписан на эти события, получает обновлённый выбор и передаёт его в UI\BP\OrderViewModel.
OrderViewModel хранит актуальный состав заказа и при переходе на экран подтверждения (UI\Widgets\ConfirmationWidget) отдаёт туда эти данные.

*WBP_DrinkRow и WBP_AddonRow, чтобы каждая позиция списка имела свой отдельный виджет с чекбоксом и возможно иконкой(иконку я не реализовывал)
