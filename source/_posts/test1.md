---
title: test1
date: 2020-12-23 20:42:00
tags:
---

Hello 
This is a test

I will write my diary and learning experience later on blog

picture test:

![ttt](/images/ttt.jpg)



2.

(a)

$\because S+P-C=Ee^{-r(T-t)}\\ \therefore P=C+Ee^{-r(T-t)}-S\\=2+30e^{-0.1*6/12}-29=1.54$

(b)

If the put price is 3, it is too high relative to the call price. An arbitrageur should buy the call, short the put and short the stock. This generates −2 + 3 +29 =30 in cash which is invested at 10%. Regardless of what happens a profit with a present value of 3.00 – 1.54 = ​1.46 is locked in.

3.

(a)

$u=e^{\sigma \sqrt{\Delta t}}=e^{0.25 \sqrt{3/12}}=1.1331$

Therefore, the percentage up movement is $1.1331-1=0.1331=13.31$%.

(b)

$d = 1/u=0.8825$

Therefore, the percentage up movement is $1-0.8825=0.1175=11.75$%.

(c)

The probability of an up movement in a risk-neutral world can be calculated as below.

$p=\frac{e^{rT}-d}{u-d}=\frac{e^{0.04*3/12}-0.8825}{1.1331-0.8825}=0.5089$

(d)

The probability of an up movement in a risk-neutral world is $1-p=0.4911$.

(e)

Call:

<img src="/Users/qiupiao/Downloads/无标题的笔记本-49.jpg" alt="无标题的笔记本-49" style="zoom:50%;" />

Put:

<img src="/Users/qiupiao/Downloads/无标题的笔记本-50.jpg" alt="无标题的笔记本-50" style="zoom:50%;" />

The values are 7.56 for call option and 14.58 for put option.

4.

**No-arbitrage arguments:**

We consider a portfolio consisting of $-1:option$ and $+\Delta : shares$.

If the stock price rises to 60, the value of the portfolio is worth $60\Delta-12$.

If the stock price falls to 42, the value of the portfolio is worth $42\Delta$.

Therefore, using $60\Delta-12=42\Delta$, we know $\Delta=0.6667$.

The value of the portfolio can be calculated to be 28.

Let f be the value of the option.

The value of the portfolio is $e^{rT}(\Delta *S-f)=e^{0.12*6/12}(0.6667*50-f)=28$.

Thus, f can be calculated to be 6.96, which means the value of option is 6.96.

**Risk-neutral valuation arguments:**

At the end of six months, if the stock price is 60, then the value of the option will be $C_u=60-48=12$. 

If the stock price is 42, then the value of the option will be $C_d=0$.  

Also, we can calculate $u=\frac{60}{50}=1.2$ and $d=\frac{42}{50}=0.84$.

The probability of an up movement is $p=\frac{e^{rT}-d}{u-d}=\frac{e^{0.12*6/12}-0.84}{1.2-0.84}=0.6161$.

The value of option is $e^{-rT}[pC_u+(1-p)C_d]=6.96$.

In conclusion, no-arbitrage arguments and risk-neutral valuation arguments give the same answers.