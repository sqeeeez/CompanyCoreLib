# CompanyCoreLib
С учетом требований, класс Analytics и метод PopularMonths в библиотеке классов CompanyCoreLib.dll могут быть реализованы следующим образом на C#. Метод PopularMonths будет принимать список объектов DateTime и возвращать список дат без времени, где каждая дата будет соответствовать первому числу месяца, отсортированного по убыванию частоты заказов. В случае равного количества заказов, более ранние месяцы будут отображаться первыми. Для реализации этого метода мы будем использовать LINQ:
namespace СompanyCoreLib

{
    public class Analytics
    {
        public List<DateTime> AnalyzePurchaseDates(List<DateTime> purchaseDates)
        {
            return purchaseDates
                .GroupBy(date => new DateTime(date.Year, date.Month, 1)) // Группировка по первому числу каждого месяца
                .OrderByDescending(group => group.Count()) // Сортировка по убыванию количества заказов
                .ThenBy(group => group.Key) // При равенстве - сортировка по дате
                .Select(group => group.Key.AddHours(-group.Key.Hour)) // Приведение времени к 00:00
                .ToList();
        }
    }
}
