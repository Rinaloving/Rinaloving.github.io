---
layout: post
title: 大话设计模式——装饰模式
tags: 设计模式
categories: Life
description: 装饰模式
---



### 装饰模式

**装饰模式（Decorator）**，动态地给一个对象添加一些额外的职责，就增加功能来说，装饰模式比生成子类更灵活。

{% highlight C# %}
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;
	
	namespace DecoratorModel
	{
	    class Program
	    {
	        static void Main(string[] args)
	        {
	            Person xc = new Person("小菜");
	            Console.WriteLine("\n第一种装扮：");
	
	            TShirts ts = new TShirts();
	            WearTie wt = new WearTie();
	
	
	            ts.Decorate(xc);
	            wt.Decorate(ts);
	            wt.Show();
	
	            Console.ReadKey();
	
	        }
	    }
	    /// <summary>
	    /// Person
	    /// </summary>
	    class Person
	    {
	        private string name;
	        public Person(string name)
	        {
	            this.name = name;
	        }
	        public Person() { }
	
	        public virtual void Show()
	        {
	            Console.WriteLine("装扮的{0}",name);
	        }
	
	    }
	    /// <summary>
	    /// 服饰
	    /// </summary>
	    abstract class Finery : Person
	    {
	        protected Person component;
	        //打扮
	
	        public void Decorate(Person component)
	        {
	            this.component = component;
	        }
	
	        public override void Show()
	        {
	            if (component != null)
	            {
	                component.Show();
	            }
	        }
	       
	    }
	
	    class TShirts : Finery
	    {
	        public override void Show()
	        {
	            Console.WriteLine("大T恤 ");
	            base.Show();
	        }
	    }
	
	    class WearTie:Finery
	    {
	        public override void Show()
	        {
	            Console.WriteLine("领带 ");
	            base.Show();
	        }
	    }
	}

{% endhighlight %}




