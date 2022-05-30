# Self-Study Material - Hypothesis testing



**Meanwhile you have learned a lot about \*Hypothesis Testing\* already. Go through the following self-study material to discover more examples, deepen your knowledge and broaden your view on Hypothesis Testing. Make sure to carefully read through the following pages, the more thorough you will go through the summary, the easier you will find the assignment.** 



# Content of this module



The goal of this module is to enable you to understand all the steps that are needed to plan and execute an experimental test. This involves:

- stating the problem;
- designing the data gathering process;
- choosing and performing a statistical test that is suited for your data.

Therefore, we will start by introducing the topic of hypothesis testing. We will then consider the design of experiments, and have A/B testing as a practical example that is often used in industry.

While we do not explicitly mention machine learning during this module, we stress that the topic is strictly connected to ML. For example, you might want to test the results of your newly-developed ML model against something else. Or, ML might be involved in the data preparation before the test.



# Hypothesis testing



## Research hypotheses vs. statistical hypotheses

Research hypotheses (also called phenomenal hypotheses) are speculations and conjectures that drive research. Statistical hypotheses are a way of restating the research hypotheses so that they can be addressed by statistical techniques.

A classical example, dating to Laplace (1773): he was investigating whether comets belong to the Solar system or not. The (mutually exclusive) research hypotheses would be:

1. comets do not belong to the Solar system,
2. comets belong to the Solar system.

However, it is difficult to test these hypotheses as they are. So he reworked the problem in terms of statistical hypotheses:

1. comets have orbital parameters that follow a uniform distribution,
2. comets have orbital parameters that do not follow a uniform distribution.

Statistical hypotheses are the subject of statistical tests. (Laplace invented a test for this case).

### 

### What to do with hypotheses: the frequentist and Bayesian perspectives

Once we frame a problem in terms of statistical hypotheses, we have two choices over what to do with them.

The first choice is that of classical, or *frequentist* statistics. We assume that hypotheses are either true or false; however we don’t know their truth. We can apply statistical tests to try to **disprove** a hypothesis. There is a degree of uncertainty in how safely we can disprove a hypotheses, that is quantified by a number called *p-value*.

The other possible choice is that of Bayesian statistics. We assume that all hypotheses may be possible, but some are more probable than others. Therefore we can attach a probability to each hypothesis. The Bayes’ rule tells how we can calculate such probabilities, given pre-existing knowledge and new data.

In this module, we will only focus on frequentist statistical tests.



## Hypothesis testing outline

As mentioned above, the very basic idea when testing hypothesis is to disprove a hypothesis. In an ideal setup where there are no errors or misclassifications, disproving a hypothesis would be very simple: you would just need to find a counter-example. For example, if the hypothesis were “All dogs are heavier than cats”, you would just need to find **one** cat that is heavier than **one** dog to disprove it. Let’s use this example to identify a few key steps before moving to a more interesting example.

1. Build a model for what you want to disprove. This is called the **“null hypothesis”**, in our example it is “All dogs are heavier than cats”.
2. Pick **one** event that has a low probability of happening in your model. This is the **test**.
3. Perform or observe the actual outcome of experiment. If the event occurs, we have evidence that the null hypothesis is false. If not, the result is inconclusive.

We note that we cannot demonstrate a null hypothesis; the best we can do to confirm it is saying that we have no element at hand to disprove it. We leave the door open to observing, tomorrow, a cat that’s heavier than a dog.

### 

### Hypothesis testing in the real world: significance and power

When the hypothesis involves measurements (which come with experimental errors), classes (which come with misclassifications) or any kind of probability distribution, disproving a hypothesis requires more work than just looking for one counter-example. For example, we could only have scales available that weight with a precision of 1 kg. What if the smallest dog is found to be the same weight of the highest cat? Or, what if the scale gets stuck at some point, and some measurements are not representative of the animal that was weighted? The idea here is that you need **a sizable number of counter-examples** before you can confidently say that the null hypothesis is (probably) false.

How many counter-examples can you attribute to errors, before becoming confident in disproving the null hypothesis? And how rare should the counter-examples be? These concepts are quantified by the **significance** and **power** of a test.

Let us first recap the two types or errors in statistics:

- Type I error: we reject the null hypothesis, even if it is really true.
- Type II error: we don’t reject the null hypothesis, even if it is really false.

In the terminology of classification, a type I error would be a false positive, and a type II error would be a false negative.

We call:

- significance, denoted by ![\alpha](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAsAAAAIBAMAAADdFhi7AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LvzKvGPvp80jdYM9PNwSHAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAP0lEQVQI12NgYFR2ZQACN4YKBgMG5gkMXNIbGDgMGDiVGBjiAxh4jjIw7Gdg4ElgYOAKYLiTUMDAmihY+qgAANVoChKc+TVrAAAAAElFTkSuQmCC), the probability of making a type I error,
- power, denoted by ![\beta](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAsAAAARBAMAAAD5z0voAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGIt0neky3WD7z69Iv/Plxs5vAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAYElEQVQI12NgYGBUdmYAAiEG1gQg5cDA3sDAwNbAwCnAwMDEwOACFGPiWr4BRHH0FACpYwwMl4GUAgPDFQgVAaQ2MLA9YGDgucAgfoCBgVnI2BEoxswABkwQKgdCGYBJABRuDGwOaVxjAAAAAElFTkSuQmCC), the probability of making a type II error.

### 



### Rejection

What do rejection and non-rejection imply? Let’s assume we have run an experiment and observed an outcome. If we find counter-examples to the null hypothesis, this means that the null hypothesis is unlikely to produce the observed outcome. Is the null hypothesis false? Actually, it is false only if the model is accurate.

How to interpret rejection depends on the source of the model. For example, a model could be:

- based on expert judgment: “an expert thinks that the null hypothesis is unlikely to produce that outcome”;
- based on past experience: “previous cases show that the null hypothesis is unlikely to produce that outcome”;
- based on mathematical principles: “under this mathematical model, the null hypothesis is unlikely to produce that outcome”.

To show how easy it is to draw an incorrect conclusion because of a bad model, let’s consider an example. We are asked, does the color of a vehicle influence its fuel consumption? We get data for a blue vehicle and a red vehicle, and we find a striking difference. Can we conclude that color influences fuel consumption? Not so fast: what vehicles are we measuring, exactly? What if ask for more data, and find that the blue vehicle is a small car, and the red one is a big truck? This example is of course exaggerated, but it highlights the importance of having a good model as the foundation of our hypotheses.

Let’s now make a different example. We have run a survey to understand what opinion our customers have about our company. 30% of our customers answer our survey. Our expectation (null hypothesis) was that most people hold opinion A, but we actually find that opinion B is more widespread. Can we reject the null hypothesis? Consider the following figure:



![](https://github.com/bigbear1111/ADS_Camp/blob/main/Module7/Pictures/1.png)





where the shaded region shows the part of the population that responded to our survey. Now it is obvious that, before rejecting the null hypothesis, we need to account for the bias in who answers the survey: maybe people with opinion A are satisfied and see little incentive in answering, while people with opinion B are critical and want their voice to be heard.

Some kind of pitfalls that could arise:

- Assume that things are independent when they are not, and “accidentally“ just disprove independence instead of your nominal hypothesis;
- Assume Gaussian distributions and “accidentally” just disprove Gaussianity;
- Assume you sample representative data, when your sample is actually not representative.

Therefore, before concluding that something else than the null hypothesis must be true, one should check what exactly the null hypothesis entails: all the underlying assumptions, all the details of the model. Going back to the trucks example, if we reject the (null) hypothesis that a vehicle is red, can we conclude that therefore it must be blue? Making such a conclusion is only possible if no other colors exist.

### 

### Building and choosing models

Here we make a few examples of things that one could test:

- Test unknown sizes again thresholds, or against other sizes. For example, test “Is fuel consumption lower than X?” or “Is object type A more probable than another?”. Possible tests for this case are [binomial](https://en.wikipedia.org/wiki/Binomial_test), [z-test](https://en.wikipedia.org/wiki/Z-test) or t-test (see below).
- Test independence between discrete things. For example, “Is vehicle quality independent of paint, for vehicles produced this way?” A possible test for this case is the [χ² test](https://en.wikipedia.org/wiki/Chi-squared_test).
- Test non-existence of trends. For example, “Does production quality remain the same over time?” A possible test for this case is the [Mann-Kendall test](https://vsp.pnnl.gov/help/vsample/design_trend_mann_kendall.htm).

## *

## An example of statistical tests

Let ![T](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA0AAAANBAMAAACAxflPAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAdPvPr/O/Mp0Yi0hg6Rl7MX0AAAAJcEhZcwAADsQAAA7EAZUrDhsAAABQSURBVAjXY2BUdgl1M3VgYC5gCGNgbGCYxcD5kIH7AIMkA+NLBp4ChgkMbAEMnAxAwJvAAAZ8AhD6XAGEdoJQDJeh9CsIxfMcTHGkPvYEUgAcGg3UpmDTBwAAAABJRU5ErkJggg==) be the test statistic. We use the test statistic to form a decision rule. We define a rejection region ![R](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAANBAMAAABr8kJMAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAr/O/zxjd6Yt0SDKd+2CGxzLOAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAXklEQVQI12NgYBD6LOgYwMDAwObAwFwApPkbGDh/Aen1Gxh4vgLpswwMsQ1AOoUhMg9IMXyeYQZSzvWbgRGknOcCA8cHqPYLEO3sCqwMDO8XMLAnrGJgNLZk4KpoAAAKBRRmBTbXNwAAAABJRU5ErkJggg==) such that we make a decision based on if we are in or not in the rejection region, i.e.

- ![X \in R](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADUAAAAOBAMAAAB9dUktAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGL/7z3TznTLdr0hgi+llwAaxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA00lEQVQY02NgYFT+IsD6TZEBGXDlay1ZCGKw/2BgnMCACqYwMOiBaMZfDFxoUgx/GRjiN4AYzgwLoEKymjMDQDT3DwaGegEQa3+4AESKdw6UwW7AwGgLZrFZQLXdghnJ6cAYeQDMYvoBEUG4iF/10kQI6+gnCM1zASa3v4FhHZjBHeAMteXlzJkQtxQzMNwHC/Uy7Ido4ClA8p4y2JYFDHwPIEITkLz3jAHo5hag239DhIKgUjxA/kvuDQw7P29g2PdtAYr/FikFMOy7ixZUsHCBAACY3TPRsiJiawAAAABJRU5ErkJggg==) means we reject the null hypothesis
- ![X \not \in R](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADUAAAARCAMAAABKBRRiAAAAPFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAo1xBWAAAAE3RSTlMAGL/7z3TznTLdr0hgi+mD6+23kqtF0gAAAAlwSFlzAAAOxAAADsQBlSsOGwAAAPVJREFUKM+dUtt2xCAIRBQNKrZb/v9f62WT1aTN2bM8mEiYAWYCAGDQqjMApB7rY40tHK/RK8bo4l4TdGtohmu4iYddO7E8r0Zj4/oDlHC6qLSTNO2M9goygsz2a2LoE9XBzJGgcFpJOBvIM1WwnczKkfF2O4F6Pc9UbS1DnF8Z1BU1lFlagSLVoSeeTIoLKsul1VgrlleCuh7zDoWZvz0zndYSPZyUxiRLr2bu6t/TrZ3d9OlLWWuqMWHJDNriK6B1ckO0w7wehKdWeXwvDClBYrXtmor6RTF5/MxaRESkXicCN/Fo/8akxltxT/lflE9AdDfaL1bBBypUgd5pAAAAAElFTkSuQmCC) means we retain (do not reject) the null hypothesis

usually the rejection region is simply the region where the value of the statistic is greater than some threshold, i.e.

![R = \left \{ x : T(x) > c\right \}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJUAAAATBAMAAABrZVK5AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAr/O/zxjd6Yt0SDKd+2CGxzLOAAAACXBIWXMAAA7EAAAOxAGVKw4bAAACJ0lEQVQ4y41UPWgUQRT+Lnd7++veRWNhIRxKKkEkiYGQJpGkH7TRQkwRITZiYWHAYogkZdhGSLTIVUpSeHtY2CWBhIiFkEIrQbYIaBHMQTxQr3HezI7c3s0dDuybnfdmvvfme98uYBq3Joxui8vJMYTeqOns6eA0y0aeZpfup8FL526UkU8hr3VjhQtyKk4h/ygbaWWXhRiX4e5iNV2vGQrbkeWUONw/fbFuw/oNL4HOaBuw7sVkazGCZl+s53CbCGOXp+tcQjfN8lKSWB+Bu7wvFkO+AgvFWJNDhFmj1W6sedx52NEvgRXubT8Tmb0v6lZ0+ox4jie/XwcqctdQovlbj1Os07VxWe7YjBjT9OY1gE1vYUDs9WdV1kiYARGJXvGrQENhrKjrFHihjBIBey3kOtr4WpzkXrNNRyeU9R1Jq8YEwOfUfXSe7Hu4DOED8RYcwmlktTJPdQZTba6LMgWZfTLD2r9BOX7JG48lSl6H2boc4sOO2jyPydwks0hG7z+aFMaXIrDLSl52xcrwZYlossPa7ihTC+5DcZD/w1rZ1ewylKirJ1XYc1udmnAqS2wZmvtQisRmWHKGHQZ/TmY8SCu/Akf1MTc6Ae9Jl778C9sfKJPURDDyk0gOItRfHr8QHHBJkNZXfX1Z68swWkavr7tRpN74Jt3/Nxbup/Pbnt+jYXw1u+vpbPjnoNYDCt8ioztUbqdqCC32wsIPs1tRZPX4r/4F/lKEn1YpvwMAAAAASUVORK5CYII=)

The value ![c](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAIBAMAAAA2IaO4AAAAJFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADHJj5lAAAAC3RSTlMAdIsyz6+d6RhI8xONfKYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAAuSURBVAjXY2BgVBRmYHBicGVgK2CQYOBWYGBgsG4AErMZGDgYuAwYlBmYA4UaAEZkBBeN279pAAAAAElFTkSuQmCC) is called the *critical value*. The problem in hypothesis testing is to find a test-statistic and an appropriate critical value. For example, if we apply a ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC)-test, then the critical value is just a quantile of the Student ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC)-distribution.

### 

### Independent two-sample t-test with unequal sample sizes, equal variance

Given two groups (1, 2), this test is only applicable when it can be assumed that the two distributions have the same variance.

The ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC) statistic to test whether the means are different can be calculated as follows:

![{\displaystyle t={\frac {{\bar {X}}_{1}-{\bar {X}}_{2}}{s_{p}\cdot {\sqrt {{\frac {1}{n_{1}}}+{\frac {1}{n_{2}}}}}}}}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIkAAAA7BAMAAAC9CLSEAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGDLdnUj7r+mLYM/zdL/dBo9MAAAACXBIWXMAAA7EAAAOxAGVKw4bAAACzElEQVRYw2NgwAM4y8trsQhPLy+/wEBnIJe/keH+OQE0UcZnvwV4/zwk3hh/BQZhTFGWTwyMBiQ4Rr6AoQBTlPE7AzspXuJOwKp8GzazcQPWv47YhOOvCJAUvscUsInyJJEWS++xmsL3iSRDuO4/AAbmZXThtf+AxM06Yk2J5U5gYOC9AWIuNgYCS0hoXdjGwMDkwE1kEDNNYP0JpDTQhDUZ4icwsDZwEplmxBkYOjBNYSxg4GgA0uzEuYVpAwPD/AAMU7SBufQrkJYhKrpZ7VMZWPuPo5sS/C2AIeIP0B1bSYtuDayiLAEoqYBRgYApOlhFVzE4IHOZHQgkmmdO2ALt/3+U0OUPoEZZFEYNQ8I7KqlhDDhZv94NBNspMAUtg/4nA3xg4EqghofYN1DDFOYJUlQIF54AB2KU6eMPF95aBWJM8aJKPdlADUOYqBIHLFRpJDCDCFksJa0sKTW2NIi4iyVw7pISYDPBgYNFBxMpphhSxRQDapjC64Cqg5EsU7gVUHVwLiDHFGaIjgNYTDmAo3k6cxKG2BIwuS5FAcMUhBgquMLwEkPsEbpNCwi5vjgAWgEzHcWZFwmbovMNmmdYs8BmgVjACowfWpaAi7Qd3eAiDUkMA6h/QOaB2kDsAaS6heMCwwGRl9PhLYf9QP9xMJBqCjcDl8OFRG6Y7bz6ExgY9Eg2hWvuTQZWAw64Mp4NWIpLwqELUuTABm8osX+A5CJG97WP0E1BEcP01YLpCLd9ZWAEFZe8/AGVDOJQjzJCLAGLzazCVbvMRapdvjNwgqM+GNgGW4fmE6AYq4MMDlNQxC2guciFIYGBHc0UkBjQKOxgNTJnvgCkj7SVdVMAuikgMYZN2A1hNEZuhOpPuAnJBYw7MdwCEiMqvoBRvRHRNMCiYxUnUY2KBERlsfgpZpGZcZqojsl3BwYqgP8K1DDFhirNhSmElQAAELr/6BKVnmUAAAAASUVORK5CYII=)

where

![{\displaystyle s_p^2={\frac {\left(n_{1}-1\right)s_{X_{1}}^{2}+\left(n_{2}-1\right)s_{X_{2}}^{2}}{n_{1}+n_{2}-2}}}.](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAP4AAAAsBAMAAAC3ThhGAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAD3klEQVRYw8VYTWgTQRR+u0mTbPNvpVrRtYitIEpTW1FEcMVLL4K9VPRQU0TbUxv/qILgnvRSaYpVaA411x7Eoh4siAT8QcFD8SBVCERq0YOWVGkpKMa3m+xmd3Ynu41s82CS2Xk78+3Me/O9eQNQtbSfq7Kjq/EE/L+wQjBeXc+d8MHqFS5CVSkaX4ZJmKjHqB0ZpTICm6zw6+iqu2rNYzZ/+tJyZdV5K3zevHnyDVpPXZpU0mSSOXPs7yI6jPo0ZYWfMTd516pWN6fVlb4lQDH5qKjRBUUrD6WZX8IfLNXdYrNxxdopHcMI6VHWpou1wPc2V8BfKNUXQTDiX6yAHyo5QCjntsD34xIcHdsmmuLXS5VodEehEDfiTwN0NkXnTPEhLTlIdENbYcUCHyEmRyOuBNxJGPHDkoGEuoipx6aB+7YEBwwcI+PnsXRCtzVD7AHIbQH3LHRkjPh+dDXPVc50x7AZCDFpOG7gGBl/Bku/mLTGH8HSA15BGg/tNSxJRF1/HIB9+BjYMzHvpRJdZLPvstm4REr4EIfLJY75KnW8oOJL22737xi0/ILhWCX8FJbnEG4u4pPzlyc6hBVxnJw/hyb25+CngWNk/Gmp1opWeMoJFQMCQrB5OByi4r+QXMSTEMz8rw1cmRzJMQp+ICZ5Yb+7ckAIJIHJQI/bgP8Xyy4ss/AFJ7ti9L+3AFvRAgLJMWHc+yw6cxBC+NH344S5iYDgjoEnAjebCHyu/88Abj2sfe6Q3OEVNg3o8Y8B9IGvL0lwzL0br0VgsE+oQWKoAK53dFCjJwICO6tU0kbnuKZy/REcr1ePvxfoHONVPb8hDz4hpZnYFAVj4YmBCVnVV/YFhDIbT+gxzDimRfW35pf4e6usMQSEVhuh2SW60mV85esqnEnUDz8Ih/D3fVljCAgh+vbcrJw/PgGznCTxYZ5+/lAmeTsN209pI7WJsegkRWhIfI5+/tA/LpbOQ7YCAlVCV8TqOrLPHhQrakBAEs3KJLq+YisgOChSQCCDdWF9pLTX8rWcfjEg1M7+xYBQI2E/ygFhvLuxNvi+R/JfbCYo1tIHfIlAzoFhN56M2XuREfxVcwC9ozvJLdn0wVz19ufph3gRTtsbo75BcADfH4Ehe2Ok1nZ9ocuMeJM2Va7bG/HHmvD1mRGvaSNvZNhVWwNyw2vyPn1mxJfbDDcygZgj27WcGal5j9xWvJHRZEtnnaELXWbEa9qIGxnGmenrMyNe00bcyMyD2wl8fWbEa9r0NzK+3sX9TuDrMyNe06a/kfEXCssOhs60kX/0NzLOipIZTWg+SX8jY0v+Aa26XcYerkFBAAAAAElFTkSuQmCC)

Here ![s_p^2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAXBAMAAAAmfQiPAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAfUlEQVQI12NgAAJmsQAGMFBhuAZh9DCIM0BBGpTmXAll8DZAGR5MQIJRUIjvAQuQYcIQqP//G5CR3jABIq/12wCqUu0DmOIxYFgAMYKBzwHM4BM2ZJgSKAZRZbATajRHAc8DMIPRgRtiFu8DqBouYYhGhlkw972Fua8cqBQAXX0VyPFuCu8AAAAASUVORK5CYII=) is the *pooled* variance (i.e., the weighted average of variances of the two groups), and ![s^2_{X_1}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWBAMAAAAoU0G7AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAkElEQVQY02NgAAJmsQAGOFBhuIbg9DCIMyCBNCQ250okDm8DEseDCcpgFBTie8AC5ZgwBOr//wblpDdMQKjX+m2ApFvtA4PqZ4ZykBCPAcMCBoYdnA5gKxj4gHQ6xDg+YUMgOT8BSR8P0A/TYM4Q/sDA8PQBhM2scISBgQ3KsWCwgnN6FzDIR8JlwACF8zwCAJRoHVl35s9HAAAAAElFTkSuQmCC) and ![s^2_{X_2}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWBAMAAAAoU0G7AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAmElEQVQY02NgAAJmsQAGOFBhuIbg9DCIMyCBNCQ250okDm8DEseDCcpgFBTie8AC5ZgwBOr//wblpDdMQKjX+m2ApFvtA4PqZ4ZykBCPAcMCBoYdnA5gKxj4gHQ6xDg+YUMgOT8BSR8P0A+CeVCO8AcGDodZEDazwhEg2Q7hWDBYAclLYHbvAgb5SAbGB0iGvGNEsJn2rAUAFDcbnJe/x84AAAAASUVORK5CYII=) are the [unbiased estimators](https://en.wikipedia.org/wiki/Bias_of_an_estimator) of the variances of the two samples. The denominator of ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC) is the standard error of the difference between two means. Remember that the unbiased estimator for the mean is simply ![\bar X = \frac{1}{n} \sum_{i=1}^n X_i](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAHYAAAAXBAMAAAAsIabdAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAi690GL/7z/OdMt1IYOkdOql5AAAACXBIWXMAAA7EAAAOxAGVKw4bAAABoElEQVQ4y2NgwAqcNzAQB4SUlAzQhIwfMJANuFD1euqaLsCmjCXsuwPzjxBsevNf7969+9n/HwwGf5gEEJKu+SUM9q0OICbnLwaWDVjttVcA+73/AM8G9gNIsvMXMHhDLf7EwITdzax/wRzOAM4JbMiy/goMClBmGZyF7t82sMMYFNgPHF+DJMueALfsvKUDht4GMLUeYoQDH4M7kn8ZeD5PgTE5sjAC8GomOFyZP2GPhjZ4qLP+gtLlIIDi/voLWPXGw/Ve/ooznjlSsIny2gcASUuQ6w3K0CX/AwHEZ7+x6T3MngBlLWQ4L4DTYm1siU6A5yM0ehUY+B7g8i8sbVpClFqDKScGhncMDIwFDAzLgdQfXNZyoyRjZjuweUBN8gcYBFoYTn87wHDuhwIOvbWo3HWgINifw8Dzvgk9u2AAaA5YAnIfTC+aHAaA5TlTCLdAoMVJSUlJBUUvhyN2vdA8xwXJXt4KMPch62WVwq4Xmuf8QOnc69L/BTD3rSOi2IDmuf3/weAH0H0QN68gQi9anoO5jzdsFmG9aHkOBwAASEVxuma7LVIAAAAASUVORK5CYII=) and the unbiased estimator for the variance of a random variable ![X](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAANBAMAAABSlfMXAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGL/7z3TznTLdr0hgi+llwAaxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAWUlEQVQI12NgYFT+IsD6TZGBgYH9BwPjBCDNwPiLgYsBDJwZFkAY+8MFIAw2CwjNwPQDyjj6CUJzBzhDGL0M+y+AjVnAwPcAxGhhYOD9DaR3ft7AsO/bAgYA6VgUV8JAX6YAAAAASUVORK5CYII=) is ![{ s_{X}^{2}={\frac {1}{n-1}}\sum _{i=1}^{n}(X_{i}-{\overline {X}}\,)^{2}}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMcAAAAXBAMAAABNFUbaAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACkklEQVRIx61WTWjUQBR+SdbsZrtJqwXFQ3UFW0H82dKCUgQX0eJx6016MAXdHl08GAQPufWy0kBP9uJeFy8iHuzJPXjxph6kUISF4lWWFZfSVuPMvMxsfiZGZB9kknzz3vtm3nvzEoC/iHEFRifa8Zocv/Zf7vxAeuxt9gGiZ+GLXP1CcnOLu3eGLxMZdAqAWjVt9tyEExkkY4eO4zx957e0cXdFTB8hPMu/PG3/bmwlHDRqUOgojQCuZ5BoA2a8sAdrsC2mT5Er1wejEbcT4Cy5dDugbmeF616X3W7BTXglwA41HYCeDCoHS+Ta9BA03SyS4ha76bBd+MyVNZaSHbCThhzUydr4zm+rcpLz4kk9xCVCx/jEsXyZjuvzXtKQg1YNci5RU44es7o5KYe1fEM8X0+udwz3+FpiKcAWfIcqwDwsXfYHQbl8pWLLCM3fSU9o05doC7Cn+j7xt+p6/3TEXnryjO3+pOmpRqcYSGUriPtBReJy3A8JhjlRqE06FCo7PLgOlYkoyMt2pgfTP8CpZOxET5Bs0uEMrCfP/RDEei9VSHLgrVHNyAkv5yAwGw1MvGFDiRyXqegxQXBIYoJFzFZzqTvYCHbwKILOESclkqWLpDz3QClGEoYgq3w0tibp0X9hp5LM4ZrMbgRVCZqrwNqBC819O9pJOUg7ZDiUpVoqiYok2BZVb2qIqh+F0kqKcT68w8leaktHEg1XYSrF53UiHkOfCPV2StOfDn+dyu/j3yvR0pHkHFI/5oFh6IxQXyrLScIBugoL8Wna0hfr9fvozvhAh0sP+xCmtrLKXgk13mctOB377gxbOnOXD45lC9onMVwtOpfVK4yMedHS0V08MN/elEfwcyFa+gjc/QFZC8DcoPzmuQAAAABJRU5ErkJggg==). The degrees of freedom for this test is ![n_1 + n_2 − 2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFkAAAAPBAMAAAB98n52AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LGM9IYN3zv6/7Munt6quJAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA50lEQVQoz2NgIBYYrRBAF3LAqZjJgeUzupg5TtWcCQwriVfNY8Cwn4GBUdnZNAFNNaoYHPQxMLjnGzA2oKlGFYMB3m8MDAWWDEwBDI4NyKohYsK7UFXzgcJkNQOHAoPgAyCLKzT0XWjoBqgYrwIrkMneAQIGINUbQcRxBv4LDLwPUHwJEmN7wIziGmaQ0bwfGOTY0VRDxBi4NyCrLmRgAmp5wLCaCU01RIzBEzmu2JaXSwENMGDINkFTDRFjCEMJ7///f8FD5wFm7DAlXMARU7wTILQLklg5gwIO1VWHMMzh/f9/A7oYABVXONaZUXsHAAAAAElFTkSuQmCC) where n is the number of participants in each group.

Given a set significance level, say ![\alpha=5\%](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADsAAAAPBAMAAACo4Ko7AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LvzKvGPvp80jdYM9PNwSHAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA4UlEQVQY02NgwA6YjAoYGLIZcAFj9rMF2w5gk2GdZvScYSmDwcWYAqzSK/oCGL4zGDAYYzWXVQBItDMYsB/ALX2awYAvAMRjVHZFk1Y2u8CwhXuDEJjnxlABtIeBwe8dEDwDMtgVGFYzcEuzH2C/zsDAPIGBS3oDmvk+QMyyIaS4gIHDgIFTCd16DSC+xvAaaGp8AAPPURQ5LgEGfSB1AOy5/QwMPAkMyHZzBoAMZ7vA8AEozRXAcCcBJXiYC9hbGRi2gP3OwJooWPoINfSMUoA+Ps7AkMgugCtKGIEybMIMACBJNRJlVpUBAAAAAElFTkSuQmCC), we use the value of the :math:`t statistic <https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.t.html>`__ in the Student ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC)-distribution and reject the null hypothesis if the value is in the top ![95\%](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAPBAMAAAB3rtAkAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAYL+dMnTp8xj7r4tIz92YfpraAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA1ElEQVQI12NggANrCwYGrgMIPveGPgmedUCGkJEDg9tq2wZ2B27GkBcMDKwJDBUM7jOvMPA3cANVMTBwBjBoMbgCVXICBfqAtL8Aw3awAN8BboYrIIEDDPsZnHcvZOBROMNqABTgD2BY39DMwH6A4eiBPobGBgbuCwz3GxgYmB4AJXVYNHYwMGyOtgeymScwMDAu4AWaAwTLGEoZmD8AjQVbzXiAIZEhBaxlIQM/AzcD2wKgKTsYOh2A1oDdwmNsDfSHlQpQRwMDV0ArwnMMoUC8dAMAXc4vkt4MP0wAAAAASUVORK5CYII=) quantile.

### 

### Independent two-sample t-test with equal sample sizes and equal variance

If the two populations have the same size, the pooling of variances becomes simpler

![{\displaystyle t={\frac {{\bar {X}}_{1}-{\bar {X}}_{2}}{s_{p}{\sqrt {\frac {2}{n}}}}}}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGMAAAA7BAMAAACdyCk8AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGDLdnUj7r+mLYM/zdL/dBo9MAAAACXBIWXMAAA7EAAAOxAGVKw4bAAACX0lEQVRIx2NgwATTy8svYIpylpfXMlANMD77LcD75yG6sFz+Rob75wSw62H5xMBogCnsr8AgjNOa7wzsWITlCxgKcDptG1Y57gR23L6Jv4LNyax/HXFr4UnCKnxMAbcWvk9Yhd/j0bL2H5CQRQ80rvsPGBh4pz/ApoP1wjYgebcBpMwYBCaAhWO5ExgYVBi2Y9OiyRAPVMTUgCrKNIH1JwNDBMNkbNFSwMDRgKlFnIGhA0SXY9GiDUyBXzG0MG1gYJgfADTwIKaO4G8BDBF/CtC0sNqnMrD2HwdGaADuYEN3GBS4MoHcjj24mQ5gE+VawAIkmR2walmXgs0o/f/fgSR/AMlZKoxkHeEdlSTrsQQRr3cDwXZitaAl2/+EwAcGrgSS3cW+gWQtzBOkSPULT4ADYUVM/lBvgAFvrQJhLSwLSHY9B+mFrjbpWnxJ12JAemUAjLubdSRp4ZzAwOTAXUBSdAswsDZwkuQ6ZnDKIsmWKyBCRoAULZtAxFaSw5glQIEEHVyghLuKgVDynTkTYSgfkMn0/z8B7/M68E0gMVGymzJCGCC7wonSwnQ+F2IbqGQuhZYihPTUg6noj0CigShbehl4GP1mFjBcAtZcTA+I0rKBYQkvmwAw9k4TnYtX3p3AEMzQxcBQD01hxIEpDIkMDOsDGKRBHJGqe0TE/i5OYOTxFzDMBXEufGWfQFjLSVACZm6A5GJWA27C9RAjuObj/Ahpm7E4sBGRGMGFNdNPXrCDuAOiVQlqETYEU6e5BSDpTHoCseFWxkxygbS+hGQt/J9Ir38OkKyFEyP/AgDdyamkZGNbGwAAAABJRU5ErkJggg==)

where

![{\displaystyle s_{p}={\sqrt {\frac {s_{X_{1}}^{2}+s_{X_{2}}^{2}}{2}}}}.](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIwAAAA3BAMAAAAs47+7AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACcElEQVRIx2NgwANU/hMHPjDgBYYMVAEZ1DGmYDAZw3mBKsbwOVDFGJYHVDGGdwKYYhYLwCqNSxwdsEMTIcM17IkThzgOY3oYxLFK4xJHB20wRhoOBWlEGSMMi/iVSIITkBLESqKMCYIFdQOSoBxSFDSQlIg9mLAbgyKO3xhGQSG+ByyYxmCI4wRMoGRhwhCo//8bpjEY4jgBswCQSG+YgCoKNQZDHCdgA4Wg1m8DJCHWu3fP3L2bgCFOOPWpfWBQ/cxQboAexOjieI3hMWBYwMCwg9MBzVOY4jjBXFDSAJcW6SzoYYMpjhM8ARU5wqBifX4CujGY4jiBH5zFA4z6aQ0YyQ8sLphHwJibiMwFrIieQsuwmciZ7gMDh8MsYgt0ZoUjwOjHLArB4gztxBpjwWCF1RiwOMMlPHUCEHPAwq93AYN8JBZjIOKMeApsVlDmQ01ZbDiUv2OE51UMOS+QUQooQs8jsOffPWvheRWeYe5CMgzDeURJTCzAklcZ7RtINgZLXuWbDywjVEEsEpo3apitHP4EUhs3oLw6JVAMNWx4Ckht3IDyqsFOtEKedQNJrRKmm+C8ylHAg5oqGH+SZAzHJoguB27U2OL7gatxIxKOu7zjfSCGlhk+4mjcsEwASuECXMLoerbiaNxwNTBE4TQGs8g4A2vcoAFuAYZ8nMa8xRCJxp2Ia3AWC+UYNstPwGUM0w8SUlP/gzbcyZV4MN9BGIdMMilpmzsgCLsEIymOYWA/gCMRP2ZgIcEYtg/YjeGIe2dKgjGM/7C3ebn///9KgjEcXwWo0kL/30AVY9ZPoIox1dTpkaVTxxgT0pQDABbx2HN9N5xoAAAAAElFTkSuQmCC)

### 

### Confidence intervals when performing hypothesis testing

**Warning**: When we reject the null hypothesis we often say that the result is *statistically significant*. A result might be statistically significant and yet the size of the effect might be small. In such a case we have a result that is statistically significant but not practically significant.

With this warning in mind, in addition to the hypothesis test explained above, it is often useful to consider the confidence interval of the difference in effect. To describe the method, let us again use the ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC)-test as our base case.

Let us denote ![\widehat {\text{se}} = s_p \sqrt{\frac{2}{n}}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFUAAAAhBAMAAABaaPq+AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAv90YSOmLdGCvMs/7851IpdE5AAAACXBIWXMAAA7EAAAOxAGVKw4bAAABl0lEQVQ4y2NgIAKs/w8CH4hRyvCCgXgQQLxSrg3Eq+UrIF4tEwMDe6YAcWqtGRjWMewkTm0aA4MrQxKEzaiMXy1YeiaYyRJW2oBXrQIQM18GMycaMEzEp5T9AZDgdgAxOYEklzAetdwLgMQTLmKDjIGjgY8otX3g1PMTSLKVZzOwpaG5IS1tAYIjBWd1MnADw8MXFHS7QWAC2DeMCdhSTukCDuZfDDwOyMZyqjBDUw0oSIG6+SHJl/vPLvbv5bUoyYPr/nGoQdBwgoHl+80wUjzXfOaHaRMYWPYbMDCwIoSzGBirPjMwGCC7N5yBl53HYAsD+3qgsxci1CYCLZFkYDdANnYDMJycGCIYGHg3oGSgsvJ0BrZnKShOaCtPYMhjOAx06wdIaiAAdrABXcPxhYEZlIGYX7ZL4VF7rQ5E/mRgA4UQO7/DNNxKmS+AKVVwamAAun4LbrUckLybb2AEpt8xHMCt1giSV9YnlIHpLSy7HAj5kHfDZkiaYN5GMDQ4DygQXTRw/HxAfDnyfwHxanVJKCLzkNgAScNiLSDa8WAAAAAASUVORK5CYII=) as the standard error and ![\widehat \theta = \bar X_1 - \bar X_2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGIAAAAVBAMAAABPrCZEAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAv90YSOmLdGCvMvOdz/tpIJwgAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABIUlEQVQ4y2NgYGBUZiANsISVNpCmY6IBw0SSNHA6MDBwCaMIsc2cOR2LysyZMwsYyARls1D5hu8vM9RvNGDAKco+wQlN8vwCBiNMgxGi1gz8aHL2ExgmYOpAiOow2KPJ8T7gxOJ4uCjzZwZ/9Bj6fhhbvMFEeQIYstEl9y3AFkIwUe6dM2OBFONdEIA6VB6rDpgofwPDNjQpjnoBoGuLsImyZwowrDfg+oAm5877AChXCmI2KQGBGkJ0DcNNBj8GTgFUDVwJLN+A1FJsoq4MScDosDZA9YclA0Mopg6oKMNMBj4GETTDLjAw5Dug64CJMm9m4MhEzR0s+k8YWOJ3oumAi/I64E6gS7GKHuHCrWM1NkGOBh6cGjjkTmERXf//JwC2ZFDsWS3XzgAAAABJRU5ErkJggg==), then the confidence interval for the difference of the two groups is

![(\widehat \theta - \widehat {\text{se}} \, t_{\alpha/2}, \widehat \theta + \widehat {\text{se}}\,  t_{\alpha/2}).](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAALQAAAAYBAMAAAChPcqUAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGIu/YOl03TL780idz692vKX9AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACVUlEQVRIx7WVT2gTQRTGv93E7drdpgNeJAgtUSKo1PSiBxEWFMRbEA8erKwBgxej9tJLD4ul6KFY8SSIUIt4ESSXIp7sUfASQU/SuloFoVjsWTC+mZ1JdzeTP2L6YGdfZn77ZWe+N7MAj8xt9Bv/gPJwLlzzBo+K2GDYGDzKI1cH7MlBo7sbxrim8yT7L1ulZIauyo/k0ErxYiepFKq3dV90OwRY4avkik4iV+LJ/raH0mjL1gRqRa9dBvIYTfCbdM3xJZltk1aokbY1iZbVH8xiTD/73209CjW9rug33gwFMLbxRr8/HrR5rtC0dAo9w5u9gFvGkXh/sdJA4SCD8/1KunpaqJTuhA7LZvjl1lSsOxuikQudJZqRwkNrohQ9otBIWodWuK3CkHm6e1iO23sJ3liAxzQQRD1msIB1kbXQSFqD3lsdCWkteBGsAIvM/kXZuRmKaUo+PwluVqvPgfNqWxB1WGQSPb32cWptXYs6ZfMWzY6JasJrWcUq7Bvbx0Xykxa35jHcoXxL9LRQudY6NBcKB0WTRz6+r80AJxYZr9xpw/uApXF8odJ4KstaopG0FuWEkN7D6H4q/tJmCZuZEFeBFy45tMxALzpSh/0eO6iU1qGfaOAup10f2YlEkVrFio9jBdpntev07GVkafidDechdlBpowZ16+RoAc4j2I1u55pVMp7xAyzrufQjPjWvE3oWq0B0HHb/1n2t1rwDVBnNP0lpg3VA7WYzhB15fb/nkfw2eQr3gWbk5vN78aoy/d7SEj0qf/b6oNh+318shQrJv0XxnYAPsreeAAAAAElFTkSuQmCC)

We will reject the null hypothesis that the two groups have the same mean if the confidence interval does not contain ![0](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAkAAAAMBAMAAABCcoqQAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAYJ2Lr0jd6TJ0v/sYzwQykEYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAABHSURBVAjXY2AQMhFgYGBNYKhgYGCbwKDFwMAXwCDNwNDXwBB3gCGuAYrkGhj6AhjmHWDgE2CYDVRpwKDLwMAI1sUwyUqAAQDCbQzeYYnbVQAAAABJRU5ErkJggg==). The confidence interval gives us an interval for the difference between the groups which can be very useful in decision making, as decisions usually depend on the size of differences due to costs involved in e.g. making a change to a product.

## *

## Design of experiments

Design of experiments (DOE) is defined as a branch of applied statistics that deals with planning, conducting, analyzing, and interpreting controlled tests to evaluate the factors that control the value of a parameter or group of parameters. DOE is a powerful data collection and analysis tool that can be used in a variety of experimental situations, when more than one input factor is suspected to influence the output. Thus, a well-performed experiment may help to understand the key factors of a process, the settings, that lead to acceptable performance or that bring less variation to the output, and other details of a process.

Many of the current statistical approaches to designed experiments originate from the work of R. A. Fisher in the early part of the 20th century. Fisher demonstrated how taking the time to seriously consider the design and execution of an experiment before trying it helped avoid frequently encountered problems in analysis.

In this section we introduce some key concepts in DOE.

### 

### Factors and confounders

Factors, or inputs of the process, are variables that can influence the result and that can be properly tested. In machine learning, they would be called features.

Confounders (or co-factors) are certain aspects that also influence the result of an experiment, but they cannot be controlled and sometimes cannot even be measured. It is important to identify them in order to understand the limitations of the experiment.

When performing a test it is important to think about confounders, i.e. hidden variables that affect the outcome in such a way that reaching a conclusion can be hard. An example of a confounder can be a piece of information, presented in a newspaper, that affects a customer churn and might shaddow the effect of a test of a churn rate between two discount program. Ignoring such confounders can lead to a wrong conclusions.

Another example of a confounder, that is commonly encountered with customers, is a word-of-mouth and social media, where, for example, customers might learn that they are participating in an experiment, and this can have devastating impact on the analysis. We will talk about blindness of an experiment below.

### 

### Choice of subjects

When picking the sample that you wish to split in two parts, test and control, for obtaining valid and reliable results, you need to make sure that the group as a whole is representative of the group that you later will use the conclusion on.

There are several factors to consider. First of all, the size of the study group: the more subjects you include, the greater the statistical power is, determining the confidence you can have in the results. However, how you assign subjects to groups plays also a crucial role.

Assume we have a test group, i.e. a group of subjects or individuals, we are conducting the experiment on. Note that for the purpose of this section we consider experiments with only one test group, however there are cases of experiment design with several study groups. You should also include a control group, that represents the subjects without any experimental intervention.

One of the examples is a churn mitigation in a customer base. Imagine the company wants to target those who are likely to churn. Using some algorithm to target them, they choose a group of customers that are likely to churn and do an AB test (for details on the test see the relevant section of the reading material) with some discount program. They notice that there is such a large effect of the discount program that they roll it out to all customers. However it shows that on the whole customer base (not just on the likely-to-churn customers) the discount program does not have an expected effect on the churn and simply it is hemorrhaging money.

### 

### Randomization

Comparing two groups that are not statistically equivalent can lead to biased results. This is the entire reason we do randomized splits. Since the split is entirely random it will make the groups statistically equivalent and hence comparable. To make an example of non comparability, look at the effect of an ad about toys where the test group have kids and the control group does not. This is a very extreme example but it highlights the problem well.

### 

### Blocking and stratification

An experiment can be completely randomized, when every subject is assigned to a group completely at random, or randomized using randomized block design. At the later case subjects are first systematized according to some characteristic they share and then randomly assigned to test and control groups within these assemblage. For example, subjects can be first grouped by age, and then randomly distributed to test and control groups.

A very similar notion is that of “stratified design”. Stratified sampling is terminology from sampling design, and blocking is a similar concept from experimental design. In each case they represent a restriction on randomization in an attempt to reduce nuisance variation. You could call it stratification, if you try to spread a confounder over all the sample; or blocking, if you can find groups (blocks) of subjects where the value of the confounder is the same, and then you randomly assign the treatments inside the block.

### 

### Replication

The experiment should be set up and documented so that replication can happen at two levels: data should be gathered and kept so that the analysis can be repeated; documentation and tools should be such that the data gathering can be repeated. Replication of an experiment allows to estimate the variability of the results and also to increase the accuracy of the estimate, assuming that no systematic bias is present in the experiment.

### 

### Blindness

If the test subjects are aware of what group of the test they are in, they might have biased behavior. For example, you do not want people to know they are getting a placebo instead of a drug since it will lose its effect.

However, the people who administrate the test, for instance the doctors, might also treat the subject in a different way, even unconsciously, depending on the group they belong to. Therefore, they should also not know what arm of the experiment the subjects belong to. This is called a double-blind test. The information about the assignments of the subjects to the groups should be kept only by a third party, and only released at the end of the experiment.

### 

### Test significance and effect size

A key rule is that *p-values* should be decided before the experiment is run. However, very strong *p-values* can be impossible to achieve if the test size is not large enough.

When conducting an experiment it is important to decide the effect size that you wish to detect. Setting the significance level and desired effect size, one can compute the minimum number of individuals needed to reach these goals. A usual mistake is not accounting beforehand for the desired effect size, which often results to the test groups not big enough, and thus to overall a useless experiment.

## *

## A/B testing

A/B testing is a form of testing one (or more) hypotheses in an experiment. It starts with making a research hypothesis, then it includes stating the problem in terms of statistical hypotheses, designing an experiment to gather the relevant data, and finally applying hypothesis testing.

The name “A/B testing” is due to the random split of a population into two groups (A and B). Another name of A/B testing is Randomized Controlled Trial (RCT).

### 

### An example

A/B testing is used to determine which alternative is best. Let’s say that we are working with a drug and wish to test if it is more effective in treating a disease than the currently used drug. To test this we simply give the new drug to one group and the old drug to another group. We then count what percentage were successfully treated in each group. The question now becomes: since there is so much variation between different people, how can we be certain that if we observe a difference, for instance the new drug might have been more successful, the difference is not due to random variations? This is the problem that A/B testing aims to solve. As soon as there is some randomness involved, like the drug working with some probability, then we can never be certain. What we can make sure is that we have a decision rule which allows us to make a certain percentage of mistakes, but be wary as the impact of the number of mistakes made, depends heavily on the circumstance.

But let us not digress, here are some examples of A/B testing

- Amazon initially decided to launch their first personalized product recommendations based on an A/B test showing a huge revenue increase by adding that feature.
- LinkedIn tested whether to use the top slot on a user’s stream for top news articles or an encouragement to add more contacts.
- Spotify tested all changes concerning the UI on their platform.

The important fact is that there are two groups that you can compare, i.e. a test group (that you test your change on) and a control group (which is the baseline). Here the design of the experiment is very important, for instance, if there is a `burn in` effect. Take for example a product to which you make a radical change, and wish to test if it is better than the previous product. In this case, the initial response to the product might not be the same as the long term effect (like novelty or anger towards change). On the other hand, if you are testing a small change or if there is otherwise no risk of `burn in`, then A/B testing can be really useful.

When designing an A/B test it is important that you choose a good metric, i.e. a measure that you really care about. If other parts of your company are doing A/B testing, make sure that you have agreed on what is the most important metric. Perhaps you are doing an analysis on customers and one analyst chooses the metric `revenue` and the other chooses `retention`. These can in many cases be quite different metrics and as such your conclusions will potentially work against each other.

To make sure that there is no systematic difference between the test and control group, we do a so called Randomized Controlled Trial (RCT). We will discuss this next.

### 

### RCT (Randomized Controlled Trial)

The basic layout of a randomized controlled trial is built from the following parts:

- The first step is to determine who is eligible to receive treatment and exclude those who cannot be treated.
- The next step is to choose a sample size and do two random subsamples of the same size, where one subsample is the *intent to treat* (ITT) group and the other the non-ITT group, sometimes called the control group.
- Some of the individuals in the ITT group will refuse or become unavailable for treatment due to some factors that we cannot control, these will be the not-treated and the remaining are the treated group.

![](https://github.com/bigbear1111/ADS_Camp/blob/main/Module7/Pictures/2.png)



Once the trial is done we usually want to estimate the effect of the treatment.

We begin with the hypothesis

```
h_0: The two groups have the same mean
h_1: The two groups do not have the same mean
```

The basics of A/B testing is that we want to test if the **null hypothesis** `h_0` holds or not with some certainty. Since they are normally distributed we can simply apply the ![t](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAMBAMAAACzedEdAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGDLdnUj7r+mLYM/zdASZ9fYAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA3SURBVAjXY2BgVGBgYHZgYOALYGAIY2AI76hkYLBkYGB4xMDAlcDAwL4BKD1BioEnwIGBt1YBAIgXBqCdvTW3AAAAAElFTkSuQmCC)-test.

#### 

#### Example A/B, change of probability

We have seen how to test the difference between a mean value between two groups, but a frequently occurring testing problem is when we want to check if there is a change in probability or “rate” between a test and control group. Here we will look at the problem of “conversion rate” with ads.

Let’s assume that we have a product on sale, and a certain percentage of the customers buy the product. The percentage is an estimate of the probability that a randomly chosen customer will buy the product, call it ![p](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAMBAMAAACpRTGTAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ0yi78YSGD7r8/d8+nyxvJ1AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAASUlEQVQI12NgEFJ2CWBgEPvCEMLAzjGBYTUDA9MGhqMMDDwCDB8ZGPgTGC8wMNQb8BUwMGi7LGZgYDjCAALfQQT7BxDZ9wtIAADsuQ2vz5ZnDAAAAABJRU5ErkJggg==). The question we would like to answer is, if a certain ad for the product changes the probability of buying the product. So the question is about the value of ![p](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAMBAMAAACpRTGTAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ0yi78YSGD7r8/d8+nyxvJ1AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAASUlEQVQI12NgEFJ2CWBgEPvCEMLAzjGBYTUDA9MGhqMMDDwCDB8ZGPgTGC8wMNQb8BUwMGi7LGZgYDjCAALfQQT7BxDZ9wtIAADsuQ2vz5ZnDAAAAABJRU5ErkJggg==) in the two groups, where the random variable is [Bernoulli](https://en.wikipedia.org/wiki/Bernoulli_distribution) distributed.

Specifically, let us assume that we have two groups, one with estimated probability ![\hat p_1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAARBAMAAAAmgTH3AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAZElEQVQI12NgYGAQEmCAABMDCM3KIMaAHZSGpEHUFH5jMAPRHJwLGPYwFoE0HWBQZq8DMpgKGL4z+AEZ/ALsF8CMfge+BjAjJm0LA5ihBtILYvwAMXyB5nwA0pxWIQzzfkNsAgA2HhI2JspkUgAAAABJRU5ErkJggg==) and ![n_1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALBAMAAABrDns0AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LGM9IYN3zv6/7Munt6quJAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAT0lEQVQI12NgVHY2TWAAAfd8A8YGMKvAkoEpgMERxFnNwKHAIPgAyDrOwH+BgRfI4v3AIMcOZjE/YFjNBGZxGzBkm4BZEIDEmgBjVR26AADuGBJgijIH+wAAAABJRU5ErkJggg==) samples, the other with estimated probability ![\hat p_2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAARBAMAAAAmgTH3AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAdklEQVQI12NgYGAQEmCAABMDCM3KIMaAHZSGpEHUFH5jMAPRHJwLGPawZwMFWQ8wKLsynGZgYCpg+N7HkMTAwC/AfoGBYTcDQ78DXwMD40UGhpi0LQwMPA0MDGogvREsDAw/gDTnBFYGjg9Ahv//3wzzfkNsAgDnixbSaWqhlgAAAABJRU5ErkJggg==) and ![n_2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALBAMAAABrDns0AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LGM9IYN3zv6/7Munt6quJAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAYUlEQVQI12NgVHY2TWAAAfd8A8YGMKvAkoEpgEF4F5C5moFDgVeBdQMDw3EG/gtsD5gbGHg/MMixMzBwb2BgfsCwmomBwdOBgduAIduEgSGMAQqYEi5AWeUMChAG7///GwDkFRKaCXDicgAAAABJRU5ErkJggg==) samples. We can think of these observations coming from the test and control groups respectively. In this case the exact test is the so called [Fisher’s exact test](https://en.wikipedia.org/wiki/Fisher's_exact_test).

Fisher’s exact test is computationally expensive, but it might be good to know that it exists if we have a small number of samples. However, usually we have a fairly large amount of data and thus we can use a normal approximation instead. To perform the normal approximation test, we can simply use the ![\hat p_1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAARBAMAAAAmgTH3AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAZElEQVQI12NgYGAQEmCAABMDCM3KIMaAHZSGpEHUFH5jMAPRHJwLGPYwFoE0HWBQZq8DMpgKGL4z+AEZ/ALsF8CMfge+BjAjJm0LA5ihBtILYvwAMXyB5nwA0pxWIQzzfkNsAgA2HhI2JspkUgAAAABJRU5ErkJggg==) and ![\hat p_2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAARBAMAAAAmgTH3AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAdklEQVQI12NgYGAQEmCAABMDCM3KIMaAHZSGpEHUFH5jMAPRHJwLGPawZwMFWQ8wKLsynGZgYCpg+N7HkMTAwC/AfoGBYTcDQ78DXwMD40UGhpi0LQwMPA0MDGogvREsDAw/gDTnBFYGjg9Ahv//3wzzfkNsAgDnixbSaWqhlgAAAABJRU5ErkJggg==) as the mean of the two populations with standard deviation ![s_{X_1}^2 = \hat p_1 (1-\hat p_1)](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAH8AAAAWBAMAAAAbaF6yAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAByElEQVQ4y2NgAAJmsQAGioAKwzV80pwCuGRgEj0M4lg1VkJoVpxSU+ECadgMYFWF0HIMDPNOYJVihjmBcyU2Axygbj/AwOTxA5cUBPA24AkCsDU/sMvlQWkPJjwGsCvgNuApEDMKCvE9YMFisYuiKJjBzYBhgImTICTiuUAchkD9/9/gcrF3gQAUq8zzBVgFYIrQDLD8yBAIZvADcXrDBKyua3jNwHZhcgEDgw6GARx8GxhyOc1BrgPq1fptgN1/vgzsAcYHQKkEZsDzciAoBDJYLjCUMtuAXAeyXO0Dg+pnhnIMY4oZ+A2YgAbMwvQCuwHDZ7DLgOHDY8CwgIFhB6cDehgw/GSwYgAZgCUQ+ScwL4AZwMvAB9SbjhkNHJ8YToAN4AE58x+KXL8CTwPYAHUGBj5hQyBjfgKGASwXxRTABrAYMHCm/8lACR7BJEjgCsJEeIDROg01ObKD4hBkANMFDMNBAQk2oBImIvwBmKoeoPoTZB7TAmRVcAAOES2gNKwcYVY4wsDAhmpAPzipbgGmYzWM4AFax8AX7YTI6BbAAEczgO88PFj40GP4DSzhSkDp3gUM8pHoLkACE4iTwG0AkeB5BDm6ADhXZ8WFT4B1AAAAAElFTkSuQmCC), and ![s_{X_2}^2 = \hat p_2 (1-\hat p_2)](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAH8AAAAWBAMAAAAbaF6yAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAB2ElEQVQ4y2NgAAJmsQAGioAKwzV80pwCuGRgEj0M4lg1VkJoVpxSU+ECadgMYFWF0HIMDPNOYJVihjmBcyU2Axygbj/AwOTxA5cUBPA24AkCsDU/sMvlQWkPJjwGsCvgNuApEDMKCvE9YMFisYuiKJjBzYBhgImTICTiuUAchkD9/9/gcrF3gQAUq8zzBVgFYIrQDLD8yBAIZvADcXrDBKyua3jNwHbBMJWBQQfDAA6+DQy54NTHDdSr9dsAu/98GdiDHHgTgKkEZsDzciAoBDJYLjCUglMfF8hytQ8Mqp8ZyjGMKWbgtzjAWMAwC9ML7AYMn8GpDxg+PAYMCxgYdnA6oIcBw08GKwYGtgRsgcg/gXkBOPUB5XgZ+IB60zGjgeMTAzD5zZrAwANy5j8UuX4FngZw6lNnYOATNgSKzE/AMIDlohgwAdwAMgwYONP/ZKAEj2ASJPUJwkR4gCEqmIfqT1AcsjQoMDBdwDC8EJb6KmEiwh8YOBxmofoTlLzfMTggqYIDUIiAUh8TrBxhVjgCJNtR/QnETP//A/2mhhE8H4AEKPXBM7oFKMAZLiEr4jsPDxY+9Bh+A0u4ElC6dwGDfCQD4wNc2WkCcRLvGCkrGJn2rCVHGwC7Amvg5JJoQgAAAABJRU5ErkJggg==). The test statistic becomes

![{\displaystyle t={\frac {{\bar {X}}_{1}-{\bar {X}}_{2}}{s_{p}\cdot {\sqrt {{\frac {1}{n_{1}}}+{\frac {1}{n_{2}}}}}}}}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIkAAAA7BAMAAAC9CLSEAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGDLdnUj7r+mLYM/zdL/dBo9MAAAACXBIWXMAAA7EAAAOxAGVKw4bAAACzElEQVRYw2NgwAM4y8trsQhPLy+/wEBnIJe/keH+OQE0UcZnvwV4/zwk3hh/BQZhTFGWTwyMBiQ4Rr6AoQBTlPE7AzspXuJOwKp8GzazcQPWv47YhOOvCJAUvscUsInyJJEWS++xmsL3iSRDuO4/AAbmZXThtf+AxM06Yk2J5U5gYOC9AWIuNgYCS0hoXdjGwMDkwE1kEDNNYP0JpDTQhDUZ4icwsDZwEplmxBkYOjBNYSxg4GgA0uzEuYVpAwPD/AAMU7SBufQrkJYhKrpZ7VMZWPuPo5sS/C2AIeIP0B1bSYtuDayiLAEoqYBRgYApOlhFVzE4IHOZHQgkmmdO2ALt/3+U0OUPoEZZFEYNQ8I7KqlhDDhZv94NBNspMAUtg/4nA3xg4EqghofYN1DDFOYJUlQIF54AB2KU6eMPF95aBWJM8aJKPdlADUOYqBIHLFRpJDCDCFksJa0sKTW2NIi4iyVw7pISYDPBgYNFBxMpphhSxRQDapjC64Cqg5EsU7gVUHVwLiDHFGaIjgNYTDmAo3k6cxKG2BIwuS5FAcMUhBgquMLwEkPsEbpNCwi5vjgAWgEzHcWZFwmbovMNmmdYs8BmgVjACowfWpaAi7Qd3eAiDUkMA6h/QOaB2kDsAaS6heMCwwGRl9PhLYf9QP9xMJBqCjcDl8OFRG6Y7bz6ExgY9Eg2hWvuTQZWAw64Mp4NWIpLwqELUuTABm8osX+A5CJG97WP0E1BEcP01YLpCLd9ZWAEFZe8/AGVDOJQjzJCLAGLzazCVbvMRapdvjNwgqM+GNgGW4fmE6AYq4MMDlNQxC2guciFIYGBHc0UkBjQKOxgNTJnvgCkj7SVdVMAuikgMYZN2A1hNEZuhOpPuAnJBYw7MdwCEiMqvoBRvRHRNMCiYxUnUY2KBERlsfgpZpGZcZqojsl3BwYqgP8K1DDFhirNhSmElQAAELr/6BKVnmUAAAAASUVORK5CYII=)

where

![{\displaystyle s_{p}={\sqrt {\frac {\left(n_{1}-1\right)s_{X_{1}}^{2}+\left(n_{2}-1\right)s_{X_{2}}^{2}}{n_{1}+n_{2}-2}}}.}](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAARAAAAA3BAMAAAA2+ggcAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAEJUlEQVRYw+1YTWgTQRR+u/nppkm2qZFKRdMe2h5EaYoVRQRXvIigtD3UP5AU0XrSKEIRBfdUL0pTlIIFba4exCIKFkRyEEEoWDyIPQQWtNSDllSpVATj7G6y2dmd2UzWsObgg222M/PNfrvz5nvvDYCDdRW9sgI4Wh80iJ1vFCLp/0RwCy00CBFRYhvnaxtw9wBWoF9hm68L3rsjwgqMZtDyxKjdXPnmFmwidE+6BdqtCV0BBxeqfNdzhO4Bt0AykQRlri+ySe9CDwmvrbgEEmwcXTnK6k6g+SLGGsqmroz+E6kZSLc48muai7SgKYLllz7Em3oSzuGBDqTbEFqdTof5xNJai4rfTuRyzUBHYQ2jj3JgcqtMnA+yqi+0bugt/rATmQXob2/9UAPQkUgzwIOJmC8Nd9KE+dTg3Q+DeE+JSBZCn1dht0206ECq8WiG7QDKZvAvwM4cgcgcukblDIkInwORy8IRm2jRgXQBjqmSAzAMTZI6MVrTMdVixnzq5tv2K2nCBPL5+Xw+BSCg8YEUXCmJ1rIKvOQAdLIggkyj35fQ0qkTsb7YrHrXU4Du7zCWxL9ICLlBWIFvNtGiAx31DDkrX4B9IpVIJKl63vOQRHDWXvDlFKto0YGORCIZ4HIw7LcTQVLAIweOajF61G9z1jcAW9DiSFbRogOpdl8NwEkIxmC83Upk6sZrGTjkLWJcVa4Z5BVTMkbkIMAICCMZi2gRgK0XqhD5pDp/OTfis4RPZrh9BG2wJQUjsgPoooUBBWm6CpGj6p+rpX+Wnto1trsSDAoV3b6HP4wkWjgQblYhsqi5tsMAQ6l8na9MAaT0CVOsQHjHkjqL9N3FGV64B/baiMBHViCnsBABuvyFyje3s9BxwkYkxApcKWVsKPgQhwqp2hLQ5ePuElf+xSP9xgg+SJ7zmjzrCSKXBG+NFHwOq2Q6PSZCCj5vS8La4tFhgP7UHtuZALdf1ol4aWrwuTvYhvmIOBMzq443pgaf5Jw1MqU8PhzhF7XgI6QjuAhE0h4fjghPdJ+QwvjOCcz+mzOJqNJm8dafdSWy8RijJjXHLXmSuF774Qg9FvgzoVW2OWwJAQKyHo5YMzPSe8pwkm2Or7aWZ8yHIwxEwjG4yHZENWb7rPPa4Ui1egOrAROENsOuu3WvUyzCqteAOBG8zZCJdbdEOjIMRPQasFyMJkxtfWdt8u3SJpRxhlFaDagVo0aFp7XxUjSF1YVnXO/8GSnOMAqrAROVNiHHYcvzF6lNeGCIIUBgNWDC1AbBFJ6++t0SacoxCCteAyZMbTBt3nPC6ZVdbokECwxE8BowYWoD7IAmXCyuuSXC/WY+TLb4iC7qcr3yTGEtxkwki1V4mq2AVCciUJRZRxKKUb5YTNWLyOMMNIZdaxAeMNooRPq9fuAfgFTm3yxWKvIAAAAASUVORK5CYII=)

**Normal Approximation**: The normal approximation comes from the fact that the [sample mean](https://en.wikipedia.org/wiki/Sample_mean_and_covariance) is approximately normally distributed when we have large samples. How many samples are needed depend on the distribution from which we sample, but in general the sample sizes are big enough that we can use the normal approximation. If you are unsure there is tons of information on Google about this specific subject. For the more theoretically interested it is due to the [law of large numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers) and the [central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem). In the case of Bernoulli random variables we can use the rule of thumb that ![np \geq 5](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADUAAAAQBAMAAABEqSrGAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LGM9IYN3zv6/7Munt6quJAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA3ElEQVQY02NgQAYuMAbva6MQBlRwNRYmN+foBTQ5hlvtUDkBBkzg3Ygkx6jsbJrAIKRrvAAiyfQYLKdsXcDA4J5vwNjAIPKZYTFUJ/NEIMGiwDCNgaHAkoEpgI39AMNWqFzFEgi9AohXM3AoAKUZuiBCcluganSA+DgD/wUGDgGGj2AROwUwxSnAoA+09QODHDsDvwPjBJA1O6Bu57sAMpP5AcNqJob8C3wJQKGMApiDHFjOMjBwGzBkmzCoGu9F9afRLni4NDPgBt9wS7F9gPqtAwgaUeXqfmPTAQClsy4zoQjt9AAAAABJRU5ErkJggg==) and ![n(1-p) \geq 5](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGIAAAATBAMAAACZ9cVZAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdJ2LGM9IYN3zv6/7Munt6quJAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABa0lEQVQoz2NggAAWAwYsgJkBN+DCKsqyALcOcwYG92eYwsJgfQ4w7r3NqnD2AwZetW+YOvhABG/oBSj35plYmAwjyBtYdHAXgLWsKIBwLyJkOC5g18EO8QjLDgGEDkZlZ9MEBh4GDB1CusZA5ROgPD1wWF4y3g70b74BYwMDJ6YOkc8MixkYPsC4liBbnBg4ExgKLBmYAhjuYehgYz/AsJWB4QjMeV2QQOJqYGBYzcChwJAH11HRAQTNQAbQnC4GhinQkHkNDVWmAwwMxxn4LzB4YrqKQ4DhIwPDAUjcP4KITWRg+sDA+4FBjh2bz/kdGCdAdXg3QsXeglzF/IBhNRMDH8jS7yg68i/wJTDwNoC81A4TM2HwucDAbcCQbcLAJAAM83/bkHWoGu8FOgc1gTJrr4UxeQMwIq8Z7BkHnCmxBUME7KtbuNPubXQBNnDcgRMJOyjAOwTQExC6QN1vkLsT8GQprA5mwSIGAHGtUMWmRZmmAAAAAElFTkSuQmCC), but take this with a grain of salt.

#### 

#### Example of change of probability continued

So, let’s get back to our example with ads and change of conversion rate. To put things in numbers, say that we do a test with a group of ![400](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAMBAMAAABhKdtFAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMASK/zv4vP6d37MmCddBiDNb+dAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAoklEQVQI1y3OsQqCUACF4f+SknQV79DQZtTYS9w1WiSkuWdobGpxDBx6gPsGOhYELdncGgT5Cq4G0rU62wcHzgHEGFnO4LwssOlpRvSN2LHtuNLs8bV352olhpoamYWKk6Xr6EGDaHNDVEHsaGHZRJYGob6UHS8GF1uuCdpc8apIJtONehNkYcGjG/I0Kf7ai7n9ebQ35O+GmB9MUC7gmRR8AMt2Kkd0OnqkAAAAAElFTkSuQmCC) customers that we randomly split into two groups, call them test and control respectively. We then show the test-group a new ad and the control-group an old ad. The numbers come in and we get ![100](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAMBAMAAACO67B7AAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAGGDpSDKdr92LdL/7zwZQoK4AAAAJcEhZcwAADsQAAA7EAZUrDhsAAACLSURBVAjXY2BUdmBgUJuuwMCUWcTAEObnwMDSwGDK4MHAHMDAwOfAwLGAIZuhi4FtA5gHRDoMTxiYDoB5cQEMfqJPGVgegnl+QF4IkPcUxtMD8pggvDgHhnWiTxi4ICr5FBjWMDxi4IKYwjGBIZehk4HtAgNIgglkuwbIdvE+cweGZbMVGLgyNzEAAFrRIStmEuAlAAAAAElFTkSuQmCC) purchases out of ![200](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAMBAMAAABhKdtFAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAi52/3XQY80j7r+kyYM/7OhBKAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAApElEQVQI1x3OMQqCcBzF8W+i9RcVpbY2aY+GoEmooalFamrKozi06yUaows0eAMlamiIukIE4mDYz9724b3hQX8a4vhHuAwL0KLumz1WpuacoRczY4k20UNGYHqcqHBSN+ZOm5Vdo8o8I4lEdqWEdSLMhFYodFo+Wx6kxyjzmJ2MOyF8MVK3YCvlDY0F2kv3GIMKHhuucsP53zCb5oPhB7AeFPwAxeYu0kWzA3oAAAAASUVORK5CYII=) customers in the test group and ![70](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAMBAMAAACdPPCPAAAALVBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAOrOgAAAADnRSTlMAr3RgSM+LGJ0yv/vp3agg85EAAAAJcEhZcwAADsQAAA7EAZUrDhsAAABxSURBVAjXHYxBCkBAAEWfGWqIEkexVi6gHMERrB3A2hEUB3AER5CFtTIlmzmDGfX7/9X/fbysKCo55BAYY9qaeMTrUByoCQkpGrkCYgxf/MdSj/86weJCOroINcK2wm7v36MNTlQDyQ6leyaY7GKY+QBsqRrGeQsfngAAAABJRU5ErkJggg==) purchases out of ![200](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAMBAMAAABhKdtFAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAi52/3XQY80j7r+kyYM/7OhBKAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAApElEQVQI1x3OMQqCcBzF8W+i9RcVpbY2aY+GoEmooalFamrKozi06yUaows0eAMlamiIukIE4mDYz9724b3hQX8a4vhHuAwL0KLumz1WpuacoRczY4k20UNGYHqcqHBSN+ZOm5Vdo8o8I4lEdqWEdSLMhFYodFo+Wx6kxyjzmJ2MOyF8MVK3YCvlDY0F2kv3GIMKHhuucsP53zCb5oPhB7AeFPwAxeYu0kWzA3oAAAAASUVORK5CYII=) customers in the control group.

In this case we get ![\hat p_1 = 0.5](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAAARBAMAAACflbe/AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA6klEQVQoz2NgYGAQEmDAD0wM0EU4w3aCKL9tMSC9rAxi6AqaGPgcgJTvqiM4zFRnYAWZ6o7T0h8MnAvgCkpD0tDdwPKFgeMjkHZNAzml8BuDGUSc+QwIbGBg4PgCQgwMogy8DQwcQMP2MBahmACU5fwC0aMA9MQBBmX2OlQrfjCwfwSzWIFOYSpg+M7gh+qInwzsIEdeZ2D9wMDAL8B+AaIA7gYGNZC5DAxPwFb0O/A1oJswCRhQLAcZEhmkgOEVk7aFAV0Be5glA8cSBrZoE7BxDBgK0EINFOq45Tk+gGLPKgSngnm/8acFAAFKN2vYh4xRAAAAAElFTkSuQmCC), ![s_{X_1}^2 = \hat p_1 (1-\hat p_1) = 0.25](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAALgAAAAWBAMAAACBC0tqAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACcElEQVQ4y7WVS2gTURSG/85MmqRJJxNro250xLZCqGTEiE+wFJVuCq0bX7T4AONGrYiUgovZq2TAx0LBBly568KF4KaIi+6MLtwJAypdVDS1KBHFeO6dZOyduQkR6iHMyZyT+815TgASNTOG/yZ9eNvKHTeaeYw24LewQQqd8XSkqeteW7FfkBkj/Z7eDDxakLrUQOgfMi5T649bGDw76tQDeSKDD9XrMQ9lpNrMtVpiU3hBSnPiy8g+f1O3dtstsuLhVeW+y8Jd1MIRUl02TmGbbx1RWsCjZnP4R+EuZWOJVMLAlTq8I71OdzVJwIe39vIvCYTg+eG0N7xdgjlnougV+gb60iyrPMZzte/+DybekbDJVGeNiOEDRPi+ZYx7sQpHiib7kChV3GXVQcF2pBnbS+gs35kCBkPwmD6HS/E9LCvhLJG/cHjSYhNFZ7M/LXk9RxEd2zXPtqABX5wmucrmoYzr6kGWlQDP2TjEDefZRZujy0AF/SuYDj3iGlKWQvAH4bLQWKzwjBJiQ10c4G0k1mNoFZZBCXgWHwrWHD+wHwwuaWjKUUt/4f6RqEHpkryHRgNPZemGTtxCeFxiX7HA4UmW6W+IxU3aHL5dMOtsiXY4scnPu7EJD03oPTvJPHsmBNdeZ0wO1yzEC78uCu1In/ManRbP5Htd3DQTtdo3dBw91rAmaWzvi2saZXPI4Eo59GDWVA6faefF1VOhbXOD60bgkpTAO5Aldzv/A6r5EugU4UW+3k9pbgdC7aiwAp8elr2Mw7KXBiMA11/5bdCDU/qpsdAb22DfLmHLyWDkq8T5Z0dImsPXQBZPrDXxD3N2l1snPKRNAAAAAElFTkSuQmCC) and ![\hat p_2 = 0.35](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEkAAAARBAMAAABjgJx1AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGN2/Mp2LdEhg+6/P8+k7+8CbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABKklEQVQoz2NgYGAQEmAgApgYoItwhu0EUWyhRxlYXqceBLFZGcTQVTUx8DkAqW0M/AEst9Y44DBdnYEVZP4mBq4DLAU43fCDgXMBmCGfAFVVGpKG7i6WLwwcH8GsOAaWsOwJQEbhNwYziCTzGRDYwMDA8QWEgKD4AANjAMMNoAjQ7D3s2SjGAZVwglUxJIECyQjkxQMMyq4Mp1Fs/MHADrGR6QGQiAIxChi+9zEkoTjsJwM7yPUnGJg/8hYwxAOZ/ALsFxgYdiO7i0ENZAMDy3cGng/AgAPZ2O/A18DAeBHFrEnAUGU5yLCRQSqATYBxCVAkJm0LAwNPA4oq9jBLBo4lDKxbjzMwpG52AJsOBBEsBOL6Byh2J7DiV8TxAUj4//+NX9W830SkLQDPGkoBxk96NwAAAABJRU5ErkJggg==), ![s_{X_2}^2 = 0.35*(1-0.35) = 0.2275](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPoAAAAWBAMAAAAbRJz3AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAizJ0nb+v3UgY8/vpz2ABj/Z2AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACs0lEQVRIx8WWP2gTURzHv5dekp5NrlerFRc9MO1QKjmhguhglpY6BKKLf6Ca0mKdNKJQCiK3iINKb9Clgg242EGo4KCoGNTBSaSDWzFQwUGIKVYpKJ6/3zX/yHvkcot9JHfJ+37u9333+7337gBqHX0ZbF1L4FMQXDP8CCVIuNvYFQQP+48vWC7PS/q+9BX5tCOdwtBE2qkLe4AH71uzB+TySQvKyBVEJkslux5TWxTNO3N4Q6eIgXUMvlhuUAoIjW20ZmMyWXW0NRzDghF3Xdeox4zbonvUwghHzOEV9jUKHVz2jdZspCiRt9k4g0cI5yMO1IaYYyHRvdvGt83ErNVIb5BRU3AXWD0jkbsMXMITRMo6kK3EVHq260VVdE+amPMKoxaQ6Lno9S3xoQuCu8jmpTKu8egLlD+zwg3jeNL9VSPHV6jxApwz+UPgOHCXswbVziU4gaK7yJZ5bXColWxdRogvS5J8r8pN2450GRD/3btEmeVIOZo8Vyc+0M8hqXsT+1wqxyw6vKXvKVS4wd+W1J2GeLSeLpWTrqxv7g5V968z1C5L2UVpqEmekGxXRjXmQBn9PzDTPIbuIo5sLodzzkOoZb73qevUMy/eu8guSWQo7NHLFSLZ4ygZNEOeaanmukcNpHncFj7TauUsUd0H5LNOZJca616RsUoLTbeQQpgmnsfFoZPxtDjpdd4i9jsRR3uK3bhv1uZ8jJP4tzUbyknkzrOlg7hRWs0gSrLH6b28Ky5kxcIP7yzilonRNG2Poye8Lm8PUS1o038utGQVQyJ3ue5PvHbdDOK0HVRj8v3Q38qa9m2hj/5M1AnylOktozM13yY864/0BzHvMN/R8Wab9IA/EugJewiH6bjcJq1bvm8XdgDzO3nsPQ2l2C7vW1Qt+PtVScHWtdDLx//d8x9j2uACt5hfFwAAAABJRU5ErkJggg==). The test values becomes



```
import numpy as np
p1 = 0.5
p2 = 0.35
s1 = np.sqrt(0.25)
s2 = np.sqrt(0.2275)
n1 = 200
n2 = 200
sp = np.sqrt(((200-1)*s1**2 + (200-1)*s2**2)/(200+200-2))
t = (p1-p2)/(sp*np.sqrt(1/200+1/200))
t
[4]:
3.0698670605799054
```





Let us assume that we beforehand decided that the significance level was ![5\%](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAPBAMAAAD9gUllAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAMumvi53PGPP7dGBIv90exXIUAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAoElEQVQI12NgAAFW1wIGBhsGCHBhf11w+AEDA6OyazpDI4PDLjmgJGPnNAGG7wwODC5AFYwLgMR0Bgf2BzDOGwYHNgEQJ8R5A8NZngNLQQaxBzD0MPCsYX/Avh1s8D0g5j0gW1IA4kQC8WaGHKCJHAsY4oGcB2DjmQRAypg3MHwAclgK2CcyMJwF28XA4GoLtOE5A4MV+wKIQ7mANPMSBgBKUyV8oKjHLgAAAABJRU5ErkJggg==) and let us look the the corresponding quantile of the t-distribution

```
import scipy.stats as stats
alpha = 0.05
c = stats.t.ppf(df=n1+n2-2,q=1-alpha/2)
c
[5]:
1.9659423239761926
[6]:
# Just some info about the stats.t.sf function above
help(stats.t.ppf)
Help on method ppf in module scipy.stats._distn_infrastructure:

ppf(q, *args, **kwds) method of scipy.stats._continuous_distns.t_gen instance
    Percent point function (inverse of `cdf`) at q of the given RV.

    Parameters
    ----------
    q : array_like
        lower tail probability
    arg1, arg2, arg3,... : array_like
        The shape parameter(s) for the distribution (see docstring of the
        instance object for more information)
    loc : array_like, optional
        location parameter (default=0)
    scale : array_like, optional
        scale parameter (default=1)

    Returns
    -------
    x : array_like
        quantile corresponding to the lower tail probability q.
```



Our test statistic was ![t \approx 3.07](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAD8AAAAMBAMAAAAnn3jvAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAGDLdnUj7r+mLYM/zdL/dBo9MAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABEklEQVQY012Qv0vDUBDHP20So4kvzaRQULO5ujoIGUTsFijoGlyLRdGlYsHRseKfIDh0iqJj/4j+A9KlDtahBroIEu+9LMbj3bsf73vvvndQi/grK/sv2nitK9z+cJiAFVcAPRo60WY58ouiGEAjqQAuWMrE7GFP3BBb3COTP+iGMDbullSxwEs9OIPj257E9vP2KWQGcChaz3G+QGl+uzrpw+N0faLdNw1zcn3Y1InccBe97pYs7kMD8ORhqudJ+SfWjbRYoKTFXEK3bPzeiUqSrwTywjcq1Ufwg6bcwV1zNt7YkdIf/LlhZmcE8herSVxyqH12pDnnrMX1Jx5kUVhSgepXV21fjnBOUK0PmU3G+gXizDwLzbxmNQAAAABJRU5ErkJggg==) and it is greater than our critical value ![c \approx 1.97](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAAAMBAMAAAAg3ab6AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAdIsyz6+d6RhI8/u/YN0cxkJsAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA7ElEQVQY02NgQAe9lWDqTo4BQ6js3ZsY8syZP0EUYwHDCgb///8/MWACsAJuAYajDBEMDAkwUbbdJ4DaGuAK7C8waDFcYGAFGaYoDCRTjKMFGFgQJthPYNAHUiApJwZXIOnAwLtnRgxCAb8AQ3wDA8cBoNkFDBJAAQUGBtbVBxAKmBwY/BsYeCYAlSpgdSSDmlA+UBJkGdhhDDy7nVEcCQThDAzSQGo+AwMHkDrUccexQw5hAu8EhloGhuNAFpcBgzLEDT2rPcAK/jIwmDSwBwBdwfAOFHKBQg3ILuCI+x7JMNuAMy0JyPFhYAAA17g1K35FD44AAAAASUVORK5CYII=), therefore we should reject our null hypothesis that the probabilities are the same. But as we talked about earlier, often it more illuminating to work with confidence intervals. So let us use the method mentioned above and compute the confidence interval.

```
[7]:
se = sp*np.sqrt(1/200+1/200) # Standard error
hattheta = p1-p2 # estimate of the difference
left_edge = hattheta - c*se  # The lower boundary of the confidence interval
right_edge = hattheta + c*se # The upper boundary of the confidence interval
[8]:
print("p1-p2 = %.3f" % hattheta)
print("Confidence interval for p1-p2 = (%.3f,%.3f)" % (left_edge, right_edge))
p1-p2 = 0.150
Confidence interval for p1-p2 = (0.054,0.246)
```

So we come to the same conclusion, but this time we know that the difference can range from fairly small to very large in favor of the new ad.

### 

### Other approaches and further reading

One problem of A/B testing is that you need to set aside a group that you will not test on. Furthermore you need to gather enough data before you make your decision, see `early peeking`. There is a different approach to A/B testing called the multi-armed bandit experiment. The setup here is more along the lines of online decisions. For instance, you might have a stream of users coming to a website and once we see that one alternative is clearly better, we want to add more users to that alternative right away. News websites often do this with their headlines.

The most well known method for multi-armed bandits is the so called Thompson sampling method.



```python
showURL('https://en.wikipedia.org/wiki/Thompson_sampling',400)
```

A nice tutorial of how to implement this, along with some theory, can be found in the following blog-post: [Towards Data Science](https://towardsdatascience.com/beyond-a-b-testing-multi-armed-bandit-experiments-1493f709f804). If you want to read more about multi-armed bandits, see https://en.wikipedia.org/wiki/Multi-armed_bandit.

