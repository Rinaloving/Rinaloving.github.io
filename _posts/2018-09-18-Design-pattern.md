---
layout: post
title: 大话设计模式——策略模式
tags: 设计模式
categories: Life
description: 策略模式
---



### 商场促销_策略模式（未使用策略模式，用简单工厂模式）
{% highlight C# %}
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace 商场促销_策略模式
	{
		class Program
		{
			static void Main(string[] args)
			{
				CashSuper cashSuper = CashFactory.createCashAccept("打8折");
				Console.WriteLine(cashSuper.acceptCash(100));
				Console.ReadKey();
			}
		}
		/// <summary>
		/// 现金收费抽象类
		/// </summary>
		abstract class CashSuper
		{
			//现金收取超类的抽象方法，收取现金，参数为原价，返回为当前价
			public abstract double acceptCash(double money);
		}

		/// <summary>
		/// 正常收费子类
		/// </summary>
		class CashNormal : CashSuper
		{
			public override double acceptCash(double money)
			{
				return money; //正常收费，原价返回
			}
		}
		/// <summary>
		/// 打折收费子类
		/// </summary>
		class CashRebate : CashSuper
		{
			private double moneyRebate = 1d;
			public CashRebate(string moneyRebate)
			{
				this.moneyRebate = double.Parse(moneyRebate);
			}

			public override double acceptCash(double money)
			{
				return money * moneyRebate;
			}
		}
		/// <summary>
		/// 返利收费子类
		/// </summary>
		class CashReturn : CashSuper
		{
			private double moneyCondition = 0.0d;
			private double moneyReturn = 0.0d;

			public CashReturn(string moneyCondition, string moneyReturn)
			{
				this.moneyCondition = double.Parse(moneyCondition);
				this.moneyReturn = double.Parse(moneyReturn);
			}

			public override double acceptCash(double money)
			{
				double result = money;
				if (money >= moneyCondition)
				{
					result = money - Math.Floor(money / moneyCondition) * moneyReturn;
				}
				return result;
			}
		}

		/// <summary>
		/// 现金收费工厂类
		/// </summary>
		class CashFactory
		{
			public static CashSuper createCashAccept(string type)
			{
				CashSuper cs = null;
				switch (type)
				{
					case "正常收费":
						cs = new CashNormal();
						break;
					case "满300返100":
						CashReturn cr1 = new CashReturn("300","100");
						cs = cr1;
						break;
					case "打8折":
						CashRebate cr2 = new CashRebate("0.8");
						cs = cr2;
						break;
				}
				return cs;
			}
		}

		
	}
{% endhighlight %}
	
### 加入策略模式后：
{% highlight C# %}
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace 商场促销_策略模式
	{
		class Program
		{
			static void Main(string[] args)
			{
				CashContext cash = new CashContext("打8折");
				Console.WriteLine(cash.GetResult(100));

				Console.ReadKey();
			}
		}
		/// <summary>
		/// 现金收费抽象类
		/// </summary>
		abstract class CashSuper
		{
			//现金收取超类的抽象方法，收取现金，参数为原价，返回为当前价
			public abstract double acceptCash(double money);
		}

		/// <summary>
		/// 正常收费子类
		/// </summary>
		class CashNormal : CashSuper
		{
			public override double acceptCash(double money)
			{
				return money; //正常收费，原价返回
			}
		}
		/// <summary>
		/// 打折收费子类
		/// </summary>
		class CashRebate : CashSuper
		{
			private double moneyRebate = 1d;
			public CashRebate(string moneyRebate)
			{
				this.moneyRebate = double.Parse(moneyRebate);
			}

			public override double acceptCash(double money)
			{
				return money * moneyRebate;
			}
		}
		/// <summary>
		/// 返利收费子类
		/// </summary>
		class CashReturn : CashSuper
		{
			private double moneyCondition = 0.0d;
			private double moneyReturn = 0.0d;

			public CashReturn(string moneyCondition, string moneyReturn)
			{
				this.moneyCondition = double.Parse(moneyCondition);
				this.moneyReturn = double.Parse(moneyReturn);
			}

			public override double acceptCash(double money)
			{
				double result = money;
				if (money >= moneyCondition)
				{
					result = money - Math.Floor(money / moneyCondition) * moneyReturn;
				}
				return result;
			}
		}


		/// <summary>
		/// CashContext类(现金上下文)
		/// </summary>
		class CashContext
		{
			CashSuper cs  = null;

			public CashContext(string type)
			{
					switch (type)
					{
						case "正常收费":
							cs = new CashNormal();
							break;
						case "满300返100":
							CashReturn cr1 = new CashReturn("300", "100");
							cs = cr1;
							break;
						case "打8折":
							CashRebate cr2 = new CashRebate("0.8");
							cs = cr2;
							break;
					}
					
			}

			public double GetResult(double money)
			{
				return cs.acceptCash(money);
			}
		}

		  

	}
{% endhighlight %}

### 小结：

策略模式是一种定义一系列算法的方法，从概念上来看，所有这些算法完成的都是相同的工作，只是实现不同，
它可以以相同的方式调用所有的算法，减少了各种算法类与使用算法类之间的耦合。

策略模式的 Strategy 类层次为 Context 定义了一系列的可重用的算法的方法或行为。继承有助于析取出这些
算法中的公共功能。

策略模式的优点是简化了单元测试，因为每个算法都有自己的类，可以通过自己的接口单独测试。


策略模式就是用来封装算法的，但在实践中，我们发现可以用它封装几乎任何类型的规则，只要在分析过程中听
到需要不同时间应用不同的业务规则，就可以考虑使用策略模式处理这种变化的可能性。












