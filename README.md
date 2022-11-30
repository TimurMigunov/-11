ЛР11

Мигунов Т.У.

ЭВТ-70

Игровой Движок: Unity.

Отчёт по лабораторной работе №11

Тема: Разработка таймера

Цель: разработать таймер в Unity 2D

1.	Создание ассетов 
________

________Рис. 11.1. Игровые ассеты 

2.	Объекты UI и её “дочки”

________

________Рис. 11.2 Объекты UI и её “дочки”
 
________

________Рис. 11.3 Настройка EventSystem
 
________
 
________Рис.11.4. Настройка Canvas
 
________
 
________Рис.11.5 Настройка Timer UI

________
 
________Рис. 11.6 Настройка Fill

________
 
________Рис. 11.7 Настройка Duration text

3.	Настройка объекта Demo.cs
 
 ________
 
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
