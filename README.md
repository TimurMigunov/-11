ЛР11

Мигунов Т.У.

ЭВТ-70

Игровой Движок: Unity.

Отчёт по лабораторной работе №11

Тема: Разработка таймера

Цель: разработать таймер в Unity 2D

1.	Создание ассетов 

________![1](https://user-images.githubusercontent.com/119228138/204778903-85ee6510-eaf6-4b44-bf40-a887184f507e.png)

________Рис. 11.1. Игровые ассеты 

2.	Объекты UI и её “дочки”

________![2](https://user-images.githubusercontent.com/119228138/204778934-c697bd9a-cef9-4852-880a-47a46e0251ef.png)


________Рис. 11.2 Объекты UI и её “дочки”
 
________![3](https://user-images.githubusercontent.com/119228138/204778952-198ad258-8808-4f6c-a770-ac47603b444e.png)


________Рис. 11.3 Настройка EventSystem
 
________![4](https://user-images.githubusercontent.com/119228138/204778970-7a8b237e-3ad8-4259-8dc0-ab35eefed5ae.png)

 
________Рис.11.4. Настройка Canvas
 
________![5](https://user-images.githubusercontent.com/119228138/204779017-172f623b-12d9-4b5d-a359-1c2593548b39.png)

 
________Рис.11.5 Настройка Timer UI

________![6](https://user-images.githubusercontent.com/119228138/204779027-e4d10895-4aa7-4858-af98-0f457175a2b1.png)

 
________Рис. 11.6 Настройка Fill

________![7](https://user-images.githubusercontent.com/119228138/204779051-a65d1bc9-bbe7-44b3-80e1-a020141cdc06.png)

 
________Рис. 11.7 Настройка Duration text

3.	Настройка объекта Demo
 
 ________![8](https://user-images.githubusercontent.com/119228138/204779078-69f1f041-572e-4166-9a67-e1c8e11cb434.png)

 
________Рис. 11.8 Настройка объекта Demo.cs

```
4.	Скрипт “Demo”
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Demo : MonoBehaviour
{
    [SerializeField] Timer timer1;

    private void Start()
    {
        timer1.SetDuration(7).Begin();
    }
}
5.	Скрипт “Timer”
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
using UnityEngine.UI;
using System;
public class Timer : MonoBehaviour
{
    [Header("Timer UI references :")]
    [SerializeField] private Image uiFillImage;
    [SerializeField] private Text uiText;
    public int Duration { get; private set; }
    private int remainingDuration;
    private void Awake()
    {
        ResetTimer();
    }
    private void ResetTimer()
    {
        uiText.text = "00:00";
        uiFillImage.fillAmount = 0f;
        Duration = remainingDuration = 0;
    }

    public Timer SetDuration(int seconds)
    {
        Duration = remainingDuration = seconds;
        return this;
    }
    public void Begin()
    {
        StopAllCoroutines();
        StartCoroutine(UpdateTimer());
    }
    private IEnumerator UpdateTimer()
    {
        while (remainingDuration > 0)
        {
            UpdateUI(remainingDuration);
            remainingDuration--;
            yield return new WaitForSeconds(1f);
        }
        End();
    }
    private void UpdateUI(int seconds)
    {
        uiText.text = string.Format("{0:D2}:{1:D2} ", seconds / 60, seconds % 60);
        uiFillImage.fillAmount = Mathf.InverseLerp(0, Duration, seconds);
    }
    public void End()
    {
        ResetTimer();
    }
    private void OnDestroy()
    {
        StopAllCoroutines();
    }
}
```
Вывод:  В ходе проделанной мы смогли разработать - таймер в Unity 2D

[ЛР11. Разработка таймера.zip](https://github.com/TimurMigunov/-11/files/10122333/11.zip)
