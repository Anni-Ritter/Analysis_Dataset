## **Лабораторная работа**

В данной лабораторной работе стоит задача исследовать данные датасета и визуализировать зависимости. Для этой цели была взята сфера: затраты населения на медицинскую страховку. В датасете есть такие параметры как: 

*   пол,
*   возраст, 
*   дети, 
*   курящий ли человек, 
*   ИМТ, 
*   регион 
*   затраты.

---

## **Исследование датасета**

Рассмотрим данные в нашем датасете. Он имеет 7 столбцов и 1338 строк данных.  

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/de0495d7bde3738ddbb0e037b80b7ce7c0d47026327fb9dc.png)

Полный датасет можно посмотреть в приложенном к этой задаче файле.

Код задачи можно посмотреть [Google Colab](https://colab.research.google.com/drive/17gXNkejYPzPHG-EZiDe8hSInJNpPpCpc#scrollTo=35hLC4Mi6ily), либо в приложенном файле.

---

## Общая информация о данных

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/22afaa30a90d440342d2118e0d834e59b23c83020b52926d.png)

*   Если мы посмотрим на среднее значение и медиану, то сможем заметить, что возраст, ИМТ и дети распределены почти нормально.
*   Нет отрицательных значений.

---

## **Анализ количественной информации**

*   Рассмотрим графики по значению “age”. Минимальное значение в параметре 18, максимальное - 64.

```python
data['age'].plot(kind='box')
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/bde2322e31c0f25d171bf49d06e64f1a2896f82146cba734.png)

```python
data['age'].hist()
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/f6abd2f644cbf60fe9ba2ebd37ab42eef675bd44e9d0a8c5.png)

```python
sns.violinplot(y = 'age', data= data )
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/1019353aa8d04b4fbb6c0162ec1b64c4555845d3d06f1d34.png)

*   Далее рассмотрим параметр “childer”. 
*   Минимум детей - 0, максимум  - 5. 
*   573 - не имеют детей, 324 - имеют 1 ребенка, 240 - имеют 2 ребенка, 157 - имеют 3 ребенка, остальные имеют 4 или 5 детей.

```python
data['children'].plot(kind='box')
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/a0e548fb79fdfdf3471973e684379c223753493c8378dee3.png)

```python
data['children'].hist()
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/3bd80aacd62b97d89060360c2308724bcd63177d84c38e67.png)

```python
sns.violinplot(y = 'children', data= data )
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/7a1e4e0f4c1e54c786c6f383b28a7356c98e48341a142f77.png)

---

## **Анализ категориальной информации**

```python
categorical_features = ['sex', 'smoker', 'region']
count_plot(categorical_features, data)
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/96d7118e8cc47951421c2c7460cdc05328641a3551c7a28a.png)

*   Мужчин и женщин примерно одинаково.
*   Курильщики составляют всего 20%.
*   На 5 человек приходится около одного курильщика.
*   Большая часть региона находится на юго-востоке.

---

## **Анализ зависимостей**

```python
sns.scatterplot(x='age', y='charges', hue="smoker", data=data)
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/7c6770e28c4eb4971b326ce91879b598e1959369a89027fa.png)

*   На сборы не влияет только возраст.
*   Курильщики платят большие сборы.

```python
sns.pairplot(data=data, hue='sex')
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/10931fd9cf841fc7a536de5d2e667972b64b2052daa7237f.png)

```python
sns.pairplot(data=data, hue='smoker')
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/8de9992aca9d16b4a42751a19437efe86df63bb617b7ae3e.png)

```python
sns.pairplot(data=data, hue='region')
```

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/e3666fedad2fb6a510ce86ab2acf44f7b82837eac71333de.png)

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/cc67f8c378b482d5b43191a9854e865a6c1429b2a676813e.png)

*   Несмотря на то, что число курильщиков составляет около 20%, однако в размере сборов курильщики платят столько же, как платят некурящие.

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/58a1dffb617a1bf3d2f6cf8582f9351d5cb3cf182854e6d3.png)

*   Мужчин и женщин примерно одинаково.
*   Мужчины платят больше, чем женщины, потому что число курящих мужчин больше, чем курящих женщин.

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/1505d41bf70856cab1bb1bba39687843483c2d985671479c.png)
