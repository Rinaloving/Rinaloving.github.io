---
layout: post
title: 大话设计模式——模板方法模式
tags: 设计模式
categories: Life
description: 模板方法模式
---



### 模板方法模式

**模板方法模式**，定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义改算法的某些特定步骤。


{% highlight C# %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TemplateMethod 
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("A学生抄的试卷：");
            TestPaper studentA = new TestPaperA();
            studentA.TestQuestion1();

            Console.WriteLine("B学生抄的试卷：");
            TestPaper studentB = new TestPaperA();
            studentB.TestQuestion1();

            Console.ReadKey();
        }
    }
    /// <summary>
    /// 测试试卷类
    /// </summary>
    class TestPaper
    {
        public void TestQuestion1()
        {
            Console.WriteLine("二娃的衣服是什么颜色的？ A.绿色 B.红色 C.蓝色 D.紫色");
            Console.WriteLine("答案："+Answer());
        }
        protected virtual string Answer()
        {
            return "";
        }
    }
    /// <summary>
    /// 学生子类代码
    /// </summary>
    
    class TestPaperA : TestPaper
    {
        //A学生
        protected override string Answer()
        {
            return "A";
        }
    }

    /// <summary>
    /// 学生子类代码
    /// </summary>
    class TestPaperB : TestPaper
    {
        //B学生
        protected override string Answer()
        {
            return "B";
        }
    }
}



{% endhighlight %}

###  模板方法模式特点

**模板方法模式是通过把不变行为搬移到超类，去除子类中的重复代码来体现它的优势。**

**模板方法模式就是提供了一个很好的代码复用平台。**

**当不变的和可变的行为在方法的子类实现中混合在一起的时候，不变的行为就会在子类重复出现。我们通过模板方法模式把这些行为版移到单一的地方，这样就帮助子类摆脱重复的不变行为的纠缠。**