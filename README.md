# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Иванова Ивана Варкравтовна
- РИ000024
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.
Ход работы:

·	Создаем новый пустой 3D проект на Unity.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/9232e9c7-9b37-4fb9-ac34-427e26350bd1)


·	В созданный проект добавляем ML Agent.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/14768305-3ccc-4660-a307-f3340532997f)


·	Далее пишем серию команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/0b45677c-854f-4a67-b58e-c9261b986e67)

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/764e56d1-8c72-4e17-8c68-69d5101078de)

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/8970b8bc-2ff9-4c5d-bdaf-ee93be9cbca5)

·	Создаем на сцене плоскость, куб и сферу так, как показано на рисунке ниже. Создаем простой C# скрипт-файл и подключаем его к сфере.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/dfbce5f9-a0ef-4477-8a15-78c3afd940ed)

·	В скрипт-файл RollerAgent.cs добавим код, опубликованный в материалах лабораторных работ.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/bbf1b859-2d62-4bee-bd73-484b1687862f)

·	Объекту «сфера» добавим компоненты Rigidbody, Decision Requester, Behavior Parameters и настроим их так, как показано на рисунке.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/e1c4cadc-1f5b-431b-8539-47ee23942da1)

·	В корень проекта добавим файл конфигурации нейронной сети, доступный в папке с файлами проекта.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/f73a8a6c-cba6-4a67-80cc-2357ef664df5)

·	Запустим работу ml-агента.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/2e04a265-c6dd-49cf-b017-c12b34f91f28)


·	Сделаем 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запустим симуляцию сцены и понаблюдаем за результатом обучения модели.

![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/787d6945-f1e3-47a2-868e-2f25517a3ca0)

При увеличении количества агентов в Unity модель достигает более высоких показателей точности за меньшее время итераций.


## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.

```bh
behaviors: #набор конфигураций для каждого поведения в сцене
  RollerBall: #это это уникальное имя, которое используется для идентификации результатов тренировок нейронной сети
    trainer_type: ppo #тип обучения с поощрением
    hyperparameters: #раздел настройки гиперпараметров для агента
      batch_size: 10 #количество опытов в каждой итерации градиентного спуска
      buffer_size: 100 #количество опытов, которые необходимо собрать перед обновлением модели политики.
      learning_rate: 3.0e-4 #начальная скорость обучения для градиентного спуска.
      beta: 5.0e-4 #сила регуляризации энтропии, которая делает политику «более случайной»
      epsilon: 0.2 #влияет на скорость изменения политики во время обучения
      lambd: 0.99 #параметр регуляризации, используемый при расчете обобщенной оценки преимущества
      num_epoch: 3 #количество проходов через буфер опыта при выполнении оптимизации градиентного спуска.
      learning_rate_schedule: linear #определение, как скорость обучения изменяется с течением времени.
    network_settings: 
      normalize: false #параметр определяет применяется ли нормализация к входным данным векторных наблюдений
      hidden_units: 128 #количество единиц в скрытых слоях нейронной сети
      num_layers: 2 #количество скрытых слоев в нейронной сети
    reward_signals: #настройки для внешних и внутренних сигналов вознаграждение
      extrinsic: #внешние силы вознаграждения
        gamma: 0.99 #фактор скидки для будущих вознаграждений
        strength: 1.0 #Коэффициент вознаграждения
    max_steps: 500000 #общее количество шагов
    time_horizon: 64 #сколько шагов опыта необходимо собрать для каждого агента, прежде чем добавить его в буфер опыта
    summary_freq: 10000 #количество опытов, которое необходимо собрать перед созданием и отображением статистики обучения
```


## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости. 
```c
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {

        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target1;
    public Transform Target2;
    private float speedMove;
    private bool isTrue = true;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }
        Target1.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
        Target2.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target1.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        speedMove = Mathf.Clamp(actionBuffers.ContinuousActions[0], 1f, 10f);
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);
        if (transform.position != Target1.transform.position & isTrue == true)
        {
            transform.position = Vector3.MoveTowards(transform.position, Target1.transform.position, Time.deltaTime * speedMove);
        }

        if (transform.position == Target1.transform.position & isTrue == true)
        {
            isTrue = false;
        }

        if (transform.position != Target2.transform.position & isTrue == false)
        {
            transform.position = Vector3.MoveTowards(transform.position, Target2.transform.position, Time.deltaTime * speedMove);
        }

        if (transform.position == Target2.transform.position & isTrue == false)
        {
            isTrue = true;
        }

        if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```
![изображение](https://github.com/GrannTwo/DA-in-GameDev-lab3/assets/138350235/d5b025f1-3670-45ad-96be-14da2d9f9843)


## Выводы
В ходе выполнения лабораторной работы были получены навыки работы с программными средствами для создания системы машинного обучения и ее интеграции в Unity.
Игровой баланс - в играх равновесие между персонажами, командами, тактиками игры. Баланс важен для многопользовательских игр.
Машинное обучение позволяет более точно распределять игровые механики, которые балансируют игру.

