---
layout: post
title: C# 异步和多线程（一）
tags:
- C#
categories: C#
description: C# 异步和多线程
---
C# 异步和多线程


![](http://b103.photo.store.qq.com/psb?/V12F66l52TZq7M/RTOoeT0mFRHiUw2TQh99Hi.Gatuc3DpEkZEjFxkT41k!/b/Yd.3bT1GGwAAYii.bT2HFQAA&bo=ngK8AQAAAAABFBI!&rf=viewer_4&t=5)

###书店买书为例

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace ThreadDmeo
{
    class Program
    {
        static void Main(string[] args)
        {
            BookShop book = new BookShop();
            //创建两个线程同时访问Sale方法
            Thread t1 = new Thread(book.Sale);
            Thread t2 = new Thread(book.Sale);
            //启动线程
            t1.Start();
            t2.Start();
            Console.ReadKey();
        }
    }

    class BookShop
    {
        //剩余图书数量
        public int num = 1;
        private static readonly object locker = new object();
        public void Sale()
        {
            lock(locker)
            {
                int tmp = num;
                if (tmp > 0) // 判断是否有书，如果有就可以卖
                {
                    Thread.Sleep(1000);
                    num -= 1;
                    Console.WriteLine("售出一本图书，还剩{0}本",num);
                }
                else
                {
                    Console.WriteLine("没有了");
                }
            }
        }
    }
}


