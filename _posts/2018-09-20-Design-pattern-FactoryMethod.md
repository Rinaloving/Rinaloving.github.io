---
layout: post
title: 大话设计模式——工厂方法模式
tags: 设计模式
categories: Life
description: 工厂方法模式
---



### 工厂方法模式

{% highlight C# %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace FactoryMethodModel
{
    class Program
    {
        static void Main(string[] args)
        {
            //工厂方法模式
            IFactory factory = new UndergraduateFactory();
            LeiFeng student = factory.CreateLeiFeng();

            student.Sweep();
        }
    }
    /// <summary>
    /// 雷锋工厂
    /// </summary>
    interface IFactory
    {
        LeiFeng CreateLeiFeng();
    }
    /// <summary>
    /// 雷锋
    /// </summary>
    class LeiFeng
    {
        public void Sweep()
        {
            Console.WriteLine("扫地");
        }

        public void Wash()
        {
            Console.WriteLine("洗衣");
        }
    }
    /// <summary>
    /// 学雷锋的大学生
    /// </summary>
    class Undergraduate : LeiFeng
    {

    }
    /// <summary>
    /// 学雷锋的志愿者
    /// </summary>
    class Volunteer : LeiFeng
    {

    }

      /// <summary>
      /// 学雷锋的大学生工厂
      /// </summary>
    class UndergraduateFactory : IFactory
    {
        public LeiFeng CreateLeiFeng()
        {
            return new Undergraduate();
        }
    }
    /// <summary>
    /// 学雷锋的志愿者工厂
    /// </summary>
    class VolunteerFactory : IFactory
    {
        public LeiFeng CreateLeiFeng()
        {
            return new Volunteer();
        }
    }
}


{% endhighlight %}