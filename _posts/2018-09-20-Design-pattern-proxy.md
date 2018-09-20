---
layout: post
title: 大话设计模式——代理模式
tags: 设计模式
categories: Life
description: 代理模式
---



### 未使用代理模式

{% highlight C# %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

//未使用代理
namespace DelegateModel
{
    class Program
    {
        static void Main(string[] args)
        {
            SchoolGirl jiaojiao = new SchoolGirl();
            jiaojiao.Name = "李娇娇";

            Pursuit zhuojiayi = new Pursuit(jiaojiao); //娇娇并不认识卓假易，此处有问题

            zhuojiayi.GiveChocolate();

            Console.Read();

        }
    }
    /// <summary>
    /// 追求者类
    /// </summary>
    class Pursuit
    {
        SchoolGirl mm;
        public Pursuit(SchoolGirl _mm)
        {
            this.mm = _mm;
        }

        public void GiveDolls()
        {
            Console.WriteLine(mm.Name + "送你洋娃娃");
        }

        public void GiveFlowers()
        {
            Console.WriteLine(mm.Name + "送你鲜花");
        }

        public void GiveChocolate()
        {
            Console.WriteLine(mm.Name + "送你巧克力");
        }
    }
    /// <summary>
    /// 被追求者类
    /// </summary>
    class SchoolGirl
    {
        public string Name { get; set; }
    }
}


{% endhighlight %}




