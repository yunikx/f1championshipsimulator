# f1racerssimulator
Console text-based  simulator f1 races

### **Параметры гонщиков и автомобиля**
Для каждого гонщика и его машины будут использоваться следующие параметры:

1. **Параметры пилота:**
   - **Опыт (опыт):** Определяет, насколько пилот стабилен и предсказуем.
   - **Агрессивность (агрессия):** Пилоты с высоким уровнем агрессии рискуют, получая шанс обогнать, но также подвергая себя штрафам (например, вылетам с трассы).
   - **Умение (умение):** Скрытый талант, который влияет на базовую скорость.
   - **Форма (физподготовка):** Зависит от уровня выносливости и физической формы пилота, влияет на стабильность.
   - **Стабильность:** Вероятность удержания позиции в непредвиденных условиях.
   - **Поддержка команды** Влияет на мораль гонщика и его концентрацию, также может помочь на этапе настроек машины.

2. **Параметры автомобиля:**
   - **Мощность двигателя:** Основной параметр, влияющий на абсолютную скорость.
   - **Аэродинамика:** Влияет на поведение машины в поворотах и на прямых.
   - **Надежность:** Вероятность технических проблем на дистанции.
   - **Износ шин:** Как эффективно автомобиль использует резину — хорошо это для гонок или нет.

3. **Команда:**
   - **Стратения:** Влияет на выбор времени для пит-стопов, смену шин и тактику гонки.
   - **Скорость пит-стопа:** Скорость пит-стопов влияет на то что команды с лучшими механиками выигрывают время на обслуживании.
   - **Бюджет:** Более богатые команды могут в течение сезона улучшать авто своих гонщиков или нанимать инженеров.
   - **Динамическая физическая форма:** Каждая гонка влияет на физическое состояние гонщика: частые поломки, аварии или проигрыши понижают его уверенность и концентрацию; успешные гонки, наоборот, делают его сильнее.
   - **Командные улучшения авто:** В зависимости от бюджета команды, в течение сезона можно улучшать характеристики машины, например:
     - Увеличивать надежность авто.
     - Улучшать управляемость или скорость.
     - Нанимать инженеров для исследования трасс.

4. **Трасса:**
   - **Сложность:** Влияет на вероятность ошибок гонщиков.
   - **Длина:** Влияет на вероятность отказа машины.
   - **Количество поворотов:** Более важно для авто с хорошей управляемостью.
   - **Погода:** Погодные условия, зависящие от случайных факторов (дождь снижает управляемость машин).
  


### **Составляющие расчёта**

1. **Характеристики гонщика:**
   - **Навыки (skill):** Определяют общее мастерство гонщика. Более высокий уровень увеличит шансы на высокий результат.
   - **Агрессивность (aggressiveness):** Увеличивает шанс обгона, особенно на сложных участках трассы, но также повышает риск ошибки или аварии.
   - **Концентрация (concentration):** Помогает гонщику избежать ошибок, особенно в стрессовых или сложных условиях (например, на трудных трассах или при плохой погоде).
   - **Физическая форма (fitness):** Влияет на способность гонщика выдерживать длительные гонки без усталости. Плохая форма снижает его результаты на последних кругах.

2. **Команда:**
   - **Бюджет:** Более богатая команда может предоставлять лучшее оборудование, что даёт небольшие бонусы к скорости или снижает вероятность поломки машины.
   - **Стратегия:** От команды зависит успешность смены шин, планирование пит-стопов и выбор обгонных моментов. Это выражается в влиянии на итоговое время гонки.
   - **Скорость пит-стопа:** Быстрые пит-стопы минимизируют потери времени.
   - **Поддержка гонщика:** Влияет на уверенность и стабильность гонщика в гонке, уменьшая вероятность ошибок.

3. **Характеристики трассы:**
   - **Сложность (difficulty):** Увеличивает вероятность ошибок. Например, на извилистых трассах с множеством поворотов гонщики с высокой концентрацией и навыками справляются лучше.
   - **Погода (weather):** Ухудшение погоды (дождь, туман) снижает общий уровень управления машиной. Гонщики с высоким навыком и концентрацией адаптируются лучше.
   - **Протяжённость:** Длинные трассы сильнее зависят от выносливости (физической формы).

4. **События в гонке:**
   - Поломки зависят от качества машины (влияет бюджет команды) и погодных условий.
   - Аварии чаще происходят при агрессии других гонщиков или низкой концентрации.

---

### **Формула итогового результата**

Для каждого гонщика вычисляем ***эффективное время гонки***. Основная идея состоит в том, чтобы сочетать личные характеристики гонщика с условиями трассы и командной поддержкой. Формула может выглядеть следующим образом:
$$\[\text{Эффективное время гонки} = \text{базовое время трассы} - \text{влияние навыков и команд} + \text{штраф за ошибки}\]$$
#### **Разбивка составляющих:**

1. **Базовое время трассы:**
   $$\[   \text{базовое время} = \text{длина трассы} \times \frac{\text{сложность трассы}}{\text{средняя скорость машины}}   \]$$
   - Трассы разной длины и сложности дают время, от которого отталкиваемся.

2. **Навыки гонщиков:**
   $$\[
   \text{влияние навыков} = \left( \text{Навыки} \times k_{\text{skill}} \right) + \left( \text{Концентрация} \times k_{\text{concentration}} \right)
   \]$$
   Здесь $$\(k_{\text{skill}}\) и \(k_{\text{concentration}}\)$$ — веса, показывающие влияние этих характеристик. Для прямолинейных трасс большая роль у навыков, для сложных — у концентрации.

3. **Командная поддержка:**
   $$\[
   \text{влияние команды} = \text{бюджет} \times k_{\text{budget}} + \text{скорость пит-стопа} \times k_{\text{pit}} - \text{ошибки стратегии}
   \]$$
   Здесь команда помогает сокращать общее время за счёт ресурсов, но её ошибки могут добавлять штрафы.

4. **Штраф за ошибки и события:**
   Штрафы добавляются в зависимости от вероятностей:
   - **Поломка минимального уровня:** Добавляет время +15-20 секунд.
   - **Серьёзная авария:** Гонщик выбывает.
   - **Снижение концентрации:** Если трасса длинная или сложная, гонщики с низкой физической формой теряют скорость:
     $$\[
     \text{штраф концентрации} = (100 - \text{концентрация}) \times k_{\text{error}}
     \]$$

5. **Погодные условия:**
   Плохая погода (например, дождь) повышает сложность трассы. Расчёт:
   $$\[
   \text{штраф погоды} = \text{сложность трассы} \times k_{\text{weather}}
   \]$$
   где \(k_{\text{weather}}\) — множитель погоды (например, 1.1 для дождя или 1.25 для сильнейшего шторма).

---

### **Имитация обгонов и борьбы за позиции**

1. **Вероятность обгона:**
   Разница между агрессивностью двух гонщиков определяет шанс обгона. Также влияет поддержка команды.
   $$\[ 
P_{\text{обгона}} = (\text{агрессивность}_{\text{гонщик 1}} - \text{агрессивность}_{\text{гонщик 2}}) + (\text{больший навык} \times k_{\text{overtake}})
\]$$

2. **Риск аварии при обгоне:**
   Чем выше агрессивность, тем больше шанс аварии. Пример:
   $$\[   P_{\text{аварии}} = \frac{\text{сумма агрессивностей} \times k_{\text{crash}}}{2}   \]$$

---

### **Пример итогового расчёта**

Предположим, у нас есть данные:

- **Гонщик 1:**
    - Навыки: 85
    - Агрессивность: 70
    - Концентрация: 80
    - Физическая форма: 90

- **Команда:**
    - Бюджет: 500
    - Скорость пит-стопа: 3 секунды
    - Ошибки стратегии: 0 (идеальная команда)

- **Трасса:**
    - Длина: 5 км, 50 кругов
    - Сложность: 70
    - Погода: дождь (коэффициент погоды 1.1)

Расчёт итогового времени:

- Базовое время:
  $$\[
  5 \, \text{км} \times 50 \, \text{кругов} \times \frac{70}{200} \approx 875 \, \text{секунд (условное начальное время)}.
  \]$$

- Влияние навыков и команд:
  $$\[
  \text{влияние навыков (skill)} = (85 \times 0.7) + (80 \times 0.3) = 77.
  \]
  \[
  \text{влияние команды} = 500 \times 0.05 + (1 / 3) \approx 25 \, \text{секунд преимущество}.
  \]$$

- Штрафы:
  $$\[
  \text{штраф погоды} = 70 \times 1.1 = 77.
  \]$$

- Итог:
  $$\[
  Итоговое время = 875 - (77 + 25) + 77 = 850.
  \]$$

Таким образом, гонщик закончит трассу за *850 секунд*.

---

### **Динамическое поведение**

Во время гонки используется симуляция событий (поломки, обгоны, аварии), чтобы результат менялся в реальном времени. Это сделает соревнование непредсказуемым.

Включение очков в симуляцию для определения победителя чемпионата добавляет новый уровень взаимодействия и стратегической глубины. Ниже я объясню, как учесть очки каждого гонщика, вести таблицу после каждой гонки и, в итоге, определить победителя чемпионата.

---

### **Балльная система чемпионата**

Очки можно начислять за каждую гонку в зависимости от занятых мест (например, по системе, используемой в "Формуле-1", или любой пользовательской). Допустим, используется такая система очков:

- За 1-е место: 25 очков.
- За 2-е место: 18 очков.
- За 3-е место: 15 очков.
- За 4-е место: 12 очков.
- За 5-е место: 10 очков.
- И далее по убывающей...

Можно также добавить бонусные очки (например, за лучший круг или меньшее количество штрафов).

---

### **Шаги для симуляции чемпионата**

#### 1. **Симуляция каждой гонки**
Для каждой гонки симуляция должна определять итоговые позиции гонщиков на основе множества параметров:
- Навыки гонщиков (как они управляют автомобилем).
- Техническое состояние автомобиля.
- Погодные условия.
- Случайные факторы (повреждения, аварии, обгоны и т.д.).

На основе этих параметров каждому гонщику вычисляется времени гонки, которое определяет итоговое место в этой гонке.

#### 2. **Начисление очков**
После завершения каждой гонки гонщики получают очки за свои позиции. Это добавляется к общей таблице очков чемпионата. 

Таблица может выглядеть так:
$$\[
\text{Таблица после 1-й гонки:}
\begin{array}{|c|c|c|}
\hline
\text{Гонщик} & \text{Гонка 1} & \text{Общие очки} \\
\hline
\text{Гонщик А} & 25 & 25 \\
\text{Гонщик B} & 18 & 18 \\
\text{Гонщик C} & 15 & 15 \\
\hline
\end{array}
\]$$

После каждой гонки очки добавляются к уже накопленным общим очкам.

#### 3. **Влияние очков на мотивацию**
Очки могут также влиять на поведение гонщиков. Гонщик, находящийся в лидерах чемпионата, может быть более осторожным, а те, кто отстает, будут "агрессивнее" на трассе. Это можно учесть через изменение их веса в любой формуле симуляции.

---

### **Конец чемпионата и определение победителя**
После завершения всех гонок суммируются заработанные очки. Гонщик с наибольшим количеством очков становится победителем чемпионата.

Если два гонщика набрали одинаковое количество очков, можно использовать дополнительные критерии для выбора победителя:
1. Количество побед в гонках.
2. Количество подиумов (1-3 место).
3. Меньшее количество сходов с трассы.

---

### **Пример: Симуляция чемпионата из 3 гонок**

#### Гонка 1
- Гонщик A занимает 1-е место, получает 25 очков.
- Гонщик B занимает 2-е место, получает 18 очков.
- Гонщик C занимает 3-е место, получает 15 очков.

Таблица после первой гонки:
$$\[
\begin{array}{|c|c|c|}
\hline
\text{Гонщик} & \text{Гонка 1} & \text{Общие очки} \\
\hline
\text{A} & 25 & 25 \\
\text{B} & 18 & 18 \\
\text{C} & 15 & 15 \\
\hline
\end{array}
\]$$

#### Гонка 2
- Считаются новые результаты гонки с учетом случайных факторов, навыков и т. д.
- Допустим, Гонщик B выигрывает гонку, а Гонщик A — второй.

После гонки 2 таблица становится:
$$\[
\begin{array}{|c|c|c|}
\hline
\text{Гонщик} & \text{Гонка 2} & \text{Общие очки} \\
\hline
\text{A} & 18 & 43 \\
\text{B} & 25 & 43 \\
\text{C} & 15 & 30 \\
\hline
\end{array}
\]$$

#### Гонка 3
- Итоги 3-й гонки:
    - Гонщик C выигрывает (25 очков).
    - Гонщик B второй (18 очков).
    - Гонщик A третий (15 очков).

Финальная таблица:
$$\[
\begin{array}{|c|c|c|}
\hline
\text{Гонщик} & \text{Гонка 3} & \text{Итоговые очки} \\
\hline
\text{A} & 15 & 58 \\
\text{B} & 18 & 61 \\
\text{C} & 25 & 55 \\
\hline
\end{array}
\]$$

**Победитель чемпионата:** Гонщик B с 61 очком.

---

### **Расширенные механики**
Для большей реалистичности можно добавить:
1. **События по ходу гонки**: неожиданные поломки, аварии, штрафные круги.
2. **Финансы**: Ограничения ресурсов на улучшение автомобилей для каждой команды.
3. **Улучшение навыков** гонщиков между гонками.
4. **Командный зачет**: Суммирование очков двух гонщиков одной команды для выигрыша "Кубка конструкторов".

5. **Случайные события:**
   - **Поломка автомобиля**
   - **Аварии, вызванные агрессивностью или погодой** 
   - **Ошибки пилотов или механиков на пит-стопе**
