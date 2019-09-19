---
layout: post
title: 大话设计模式——建造者模式
tags: 设计模式
categories: Life
description: 建造者模式
---



### 建造者模式

**建造者模式**，将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。

建造者模式好处就是使得建造代码与表示代码分离，由于建造者隐藏了改产品是如何组装的，所以若需要改变一个产品的内部表示，只需要再定义一个具体的建造者就可以了。

{% highlight C# %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 建造者模式
{
    class Program
    {
        static void Main(string[] args)
        {
            Director director = new Director();
            Builder b1 = new ConcreteBuilder1();
            Builder b2 = new ConcreteBuilder2();

            director.Construct(b1);
            Product p1 = b1.GetResult();
            p1.Show();

            director.Construct(b2);
            Product p2 = b1.GetResult();
            p2.Show();

            Console.Read();
        }
    }
    /// <summary>
    /// 产品类 ， 由多个部件组成
    /// </summary>
    class Product
    {
        IList<string> parts = new List<string>();
        public void Add(string part) 
        {
            parts.Add(part); // 添加产品部件
        }

        public void Show()
        {
            Console.WriteLine("\n产品 创建 ----");
            foreach (string part in parts)
            {
                Console.WriteLine(part); //列举所有产品部件
            }
        }
    }
    /// <summary>
    /// 抽象建造类，确定产品由两个部分组成，声明一个建造后结果的方法
    /// </summary>
    abstract class Builder
    {
        public abstract void BuildPartA();
        public abstract void BuildPartB();
        public abstract Product GetResult();
    }
    /// <summary>
    /// 具体建造者类
    /// </summary>
    class ConcreteBuilder1 : Builder
    {
        private Product product = new Product();

        public override void BuildPartA()
        {
            product.Add("部件A");
        }

        public override void BuildPartB()
        {
            product.Add("部件B");
        }

        public override Product GetResult()
        {
            return product;
        }
    }
    /// <summary>
    /// 具体建造者2类
    /// </summary>
    class ConcreteBuilder2 : Builder
    {
        private Product product = new Product();

        public override void BuildPartA()
        {
            product.Add("部件X");
        }

        public override void BuildPartB()
        {
            product.Add("部件Y");
        }

        public override Product GetResult()
        {
            return product;
        }
    }
    /// <summary>
    /// 指挥者类
    /// </summary>
    class Director
    {
        public void Construct(Builder builder)
        {
            builder.BuildPartA();
            builder.BuildPartB();
        }
    }
    
}



{% endhighlight %}

