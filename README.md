# Customer-Life-Time-Value (CLV)
`CLV Overview`
* This is often referred to as Customer Lifetime Value (CLV), Recency, Frequency, Monetary Value (RFM) or Customer Probability Models etc
* These models focus exclusively on how customers make repeat purchases over their own lifetime relationship with the company
* Cameron Pilon transformed their CLV work into an easily implementable python code package called [lifetimes](https://github.com/CamDavidsonPilon/lifetimes)

I am applying analysis to company (Olist) and carefully examining registered customer orders, dataset has information of 100k orders from 2016 to 2018 made at multiple marketplaces in Brazil
* Olist is a Brazilian online e-commerce department store
  * Olist connects small businesses from all over Brazil to channels without hassle and with a single contract
  * These merchants are able to sell their products through Olist Store and ship them directly to customers using Olist logistics partners 

-----
`Steps to take:`
1. From the data-set, I extract Olist best customers through forecasting their future purchases
2. Then analyze their historical purchasing paths, infer their probability of leaving and generalize Olist customers via RF Matrices
3. Take models presented one step further and perform a bottom-up financial valuation of Olist to determine how much it is worth today

-----
`How Modelling will be done??`
First step to customer analysis is to find a good mathematical model to describe customer repeat purchases <br>
This doesn't have to get complicated, Fader and Hardie only considers timing as a primary factor. Who is Fader and Hardie???
Few well-established models proposed are as:
* `Pareto/NBD Model` by [Schmittlein et al.](https://www.jstor.org/stable/24571167) in 1984
* `BG/NBD Model` was later proposed by [Fader and Hardie](http://www.brucehardie.com/papers/bgnbd_2004-04-20.pdf) in 2004 => An alternate and easier to implement model then Pareto/NBD Model
* [BG/BB Model](https://web-docs.stern.nyu.edu/old_web/emplibrary/Peter%20Fader.pdf) in 2009 => more recent model
I will be introducing and actively using `BG/NBD model` within our analysis, both `Pareto/NBD` and `BG/NBD` are supported within `lifetimes`<br>
## A quick goto of `BG/NBD Model`: 
* Customers will come and buy at an interval that's randomly distributed within a reasonable time range
* After each purchase they have a certain probability of dying or becoming inactive (never returning to buy again)
* Each customer is different and have varying purchase intervals and probability of going inactive

## `Model Mathematical Specification`:
* Customers buy `stochastically` according to a Poisson distribution with purchasing rate `(λ)-lambda`
* After each purchase customer has `p%` chance of becoming inactive 
  * so time period at which a customer becomes inactive is distributed as a shifted geometric distribution
* customer-base is `heterogeneous` across those two parameters such that we can assume a `(γ)-gamma` and `(β)-beta distribution` respectively
* at last we assume that `λ` and `p%` across customers are jointly independent
  * This makes some of math later on much easier
<h1>`λ ~ γ(a,r),p ~ β(a,b)`</h1>

## `Family of Models`:
* This class of models try to quantify customer behavior under a `non-contractual setting` where we don't know when customers become inactive but rather assign a percentage confidence that we believe they are dead
  * In contrast, another class of models are designed for `contractual settings` and have been successfully applied to other businesses such as telecommunication industry where a customer has to tell you that they're ending their relationship
    * Example: Large number of subscriber-based firms like Netflix often report and describe their churn rate or customer turnover. CLV is much simpler to quantify on that scale but for a normal product-selling firm, this is much more difficult as were not sure when a customer has decided to terminate relationship
* Having a model that can describe customer `deaths` and `purchases over time` is much more effective at inferring their future purchases and subsequent aggregation into expected total sales than a naive "oh I expect goods sale to grow at maybe 1% next year". This I will shown in details later on with some simple plots






