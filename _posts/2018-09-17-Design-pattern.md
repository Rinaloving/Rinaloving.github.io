---
layout: post
title: 大话设计模式——简单工厂模式
tags: 设计模式
categories: Life
description: 简单工厂模式
---



### 设计一个简单的计算器（本文只写了加法）
{% highlight C# %}
	using System;

	namespace 简单工厂模式
	{
		class Program
		{
			static void Main(string[] args)
			{

				Operation oper;
				oper = OperationFactory.createOperate("+");
				oper._numberA = 1;
				oper._numberB = 2;
				double result = oper.GetResult();
				Console.WriteLine(result);



			}
		}
		/// <summary>
		/// Operation 类
		/// </summary>
		public class Operation
		{
			public double _numberA { get; set; }
			public double _numberB { get; set; }

			public virtual double GetResult()
			{
				double result = 0;
				return result;
			}
		}
		/// <summary>
		/// 加法
		/// </summary>
		class OperationAdd : Operation
		{
			public override double GetResult()
			{
				double result = 0;
				result = _numberA + _numberB;
				return result;
			}
		}
		/// <summary>
		/// 简单运算工厂类
		/// </summary>
		public class OperationFactory
		{
			public static Operation createOperate(string operate)
			{
				Operation oper = null;
				switch (operate)
				{
					case"+":
						oper = new OperationAdd();
						break;
				}
				return oper;
			}
		}
	}
{% endhighlight %}