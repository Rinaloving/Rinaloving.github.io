---
layout: post
title: 大话设计模式
tags: C#
categories: Life
description: 策略模式
---



### 商场促销_策略模式（未使用策略模式，用简单工厂模式）

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

	
### 加入策略模式后；





