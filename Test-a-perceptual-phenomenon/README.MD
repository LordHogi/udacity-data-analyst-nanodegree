Statistics: The Science of Decisions Project Instructions

**Background Information**

In a Stroop task, participants are presented with a list of words, with
each word displayed in a color of ink. The participant's task is to say
out loud the color of the ink in which the word is printed. The task has
two conditions: a congruent words condition, and an incongruent words
condition. In the congruent words condition, the words being displayed
are color words whose names match the colors in which they are printed:
for example RED, BLUE. In the incongruent words condition, the words
displayed are color words whose names do not match the colors in which
they are printed: for example PURPLE, ORANGE. In each case, we measure
the time it takes to name the ink colors in equally-sized lists. Each
participant will go through and record a time from each condition.
Questions For Investigation As a general note, be sure to keep a record
of any resources that you use or refer to in the creation of your
project. You will need to report your sources as part of the project
submission.

**1. What is our independent variable? What is our dependent variable?**

The independent variables are categorical variables assuming the
congruent words or incongruent words condition. The dependent variable
is the time input each person report for each (in)congrency condition.

**2. What is an appropriate set of hypotheses for this task? What kind
of statistical test do you expect to perform? Justify your choices.**

Time users report to complete the incongruent words condition is
significantly larger than it is to complete the congruent words
condition, comparing the average means of the two conditions we will
measure if they're significantly different at a chosen significance
level to attest the existence of the Stroop Effect.

***Null Hypothesis***

The null hypothesis for this experiment will assume there's no
difference on the mean times for each condition, meaning that people
usually take the same time to accomplish the tests regardless of (color
name,color) congruency.

H0: *μ*D = *μ*C - *μ*I = 0; The mean time of the congruent word
condition is equal to the mean time of the incongruent word condition.

The population mean of the differences (*μ*D) is equal (not
significantly different) to the hypothesized mean of the differences
(*μ*D = 0).

***Alternative Hypothesis***

The alternative hypothesis for this experiment will assume users report
less time under the congruent condition when compared to the time
reported under the incongruent condition.

H1: *μ*D = *μ*C - *μ*I ≠ 0; The mean time reported under the congruent
condition is less than the mean time reported when the pair (color name,
color) is incongruent.

*μ*C: Population mean for the time taken to read and speak out loud the
correct answer under the congruent condition.

*μ*I: Population mean for the time taken to read and speak out loud the
correct answer under the incongruent condition.

The population mean of the differences (*μ*D) is not equal
(significantly different) to the hypothesized mean of the differences
(*μ*D = 0).

***Proposed Statistical Test***

The chosen statistical test for this experiment is the T-Test.

Data Limitations:

-   &lt; 30 samples.
-   Unknown population's standard deviation.

Assumptions:

-   Samples are radomly collected from each population.
-   Dependent variable (time reported) is measured on a continous scale
    given in seconds.
-   Independent variable (condition type) consists of two categorical
    related groups (same individuals took each test/repeated measure).
-   Difference score are normally distributed (Gaussian).
-   There's no significant outliers in the difference between the
    Congruent and Incongruent condition.

***Known Lurking Variables***

In the controlled environment described, the process each person go
through is by taking two tests one after the other in a particular order
(congruent condition first and then incongruent condition right after).
We can re-arrange the same controlled experience in other ways to better
understand if there's significant correlation between the test order and
number of tests taken and the time reported. Possible scenarios would
be:

S1: Person takes only one test: Congruent condition.

S2: Person takes only one test: Incongruent condition.

S3: Person takes two tests: Congruent Condition first, then Incongruent
Condition.

S4: Person takes two tests: Incongruent Condition first, then Congruent
Condition.

Exploring data from this full set of experiments we would be able to
better understand if this two properties affect the time reported and
can potentially show if there's a bias under certain circumstances.

**3. Report some descriptive statistics regarding this dataset. Include
at least one measure of central tendency and at least one measure of
variability.**

    library('ggplot2')
    library('gridExtra') 
    library(scales)
    library(reshape2)

    df <- read.csv("memory_scores.csv")

    descriptive <- function(arg){
    n <- length(arg)
    min <- min(arg)
    qt1 <- unname(quantile(arg,probs=0.25))
    mean <- mean(arg)
    median <- median(arg)
    qt2 <- unname(quantile(arg,probs=0.75))
    max <- max(arg)
    var <- var(arg)
    SD <- sd(arg)
    return(c(n,min,qt1,mean,median,qt2,max,var,SD))
    }

    istats <- data.frame(descriptive(df$Congruent),
                         descriptive(df$Incongruent))

    names(istats) <- c("Congruent","Incongruent")
    row.names(istats) <- c("Sample Size","Minimum","Lower Quartile (25%)","Mean","Median","Upper Quartile (75%)","Maximum","Variance","Standard Deviation")

    print.data.frame(istats)

    ##                      Congruent Incongruent
    ## Sample Size          24.000000   24.000000
    ## Minimum               8.630000   15.687000
    ## Lower Quartile (25%) 11.895250   18.716750
    ## Mean                 14.051125   22.015917
    ## Median               14.356500   21.017500
    ## Upper Quartile (75%) 16.200750   24.051500
    ## Maximum              22.328000   35.255000
    ## Variance             12.669029   23.011757
    ## Standard Deviation    3.559358    4.797057

**4. Provide one or two visualizations that show the distribution of the
sample data. Write one or two sentences noting what you observe about
the plot or plots.**

    #Reshaping Data
    df2 <- t(df)
    df2 <- melt(df2, id=c("v1"))
    df2$Var2 <- NULL
    colnames(df2)=c("Condition","Time_Reported")

    ggplot(data=df2,aes(x=df2$Time_Reported,fill=Condition))+
      geom_histogram(binwidth=2,alpha=0.5,position = 'identity')+
      scale_x_continuous(breaks=seq(0,36,2))+
      scale_y_continuous(breaks=seq(0,6,1))+
      ylab("# Of Occurrences")+
      xlab("Time Reported")

![](Test_a_perceptual_phenomenon_files/figure-markdown_strict/unnamed-chunk-2-1.png)

    ggplot(data=df2,aes(x=Condition,y=Time_Reported,color=Condition))+
      geom_boxplot()+
      scale_y_continuous(breaks=seq(0,36,2))

![](Test_a_perceptual_phenomenon_files/figure-markdown_strict/unnamed-chunk-2-2.png)

The histograms intercept occurs between the right tail region of the
Congruent condition and the left tail of the Incongruent condition,
showing that the Incongruent condition (indeed) seems to take
significantly more time to complete than the Congruent condition.

Looking at the 15s-23s range we can find that there's a common area
comprehending the fastest reported times of the incongruent condition
and the slowest reported times of the congruent condition, we can also
observe from the boxplots that the bulk of the data (75% of the data
which contained within the boxplots) shows at least a ~3s difference.

**5. Now, perform the statistical test and report your results. What is
your confidence level and your critical statistic value? Do you reject
the null hypothesis or fail to reject it? Come to a conclusion in terms
of the experiment task. Did the results match up with your
expectations?**

***Test Overall Information***

Test if treatment has signifcant impact on time reported with a
dependent t-test for paired samples

Pre-treatment: Congruent words condition Post-treatment: Incongruent
words condition.

    t.test(df$Congruent, df$Incongruent,alternative="less",mu=0,paired=TRUE,var.eq=FALSE,conf.level=0.95)

    ## 
    ##  Paired t-test
    ## 
    ## data:  df$Congruent and df$Incongruent
    ## t = -8.0207, df = 23, p-value = 2.052e-08
    ## alternative hypothesis: true difference in means is less than 0
    ## 95 percent confidence interval:
    ##       -Inf -6.262868
    ## sample estimates:
    ## mean of the differences 
    ##               -7.964792

t(23) = -8.02, p &lt; 0.05 , one-tailed Confidence interval on the mean
difference; 95% CI = -6.262868 (Inferior limit)

The p-value is the probability below the negative value of the
t-statistic, Since it's less than the alpha level we reject the null
hypothesis, such result matches the initial expectation.

Another way to look at the provided result is to compare the t-critical
value with the t-statistic, as the t-statistic is out of the t-critical
value boundary it gives us enough information to reject the null
hypothesis for the entire population.

Assuming there's no difference on the sample means (null is true) we
would obtain the observed difference or more in only ~0.00000002% of the
possible samples due to random sampling error, showing that it's
extremely unlikely that the null hypothesis is true.

**6. Optional: What do you think is responsible for the effects
observed? Can you think of an alternative or similar task that would
result in a similar effect? Some research about the problem will be
helpful for thinking about these two**

Probably there's a natural intuitive brain issue for this type of
situation, the observed effect occurs due conflicting information
between the name of the color and the color it's filled with, the brain
might recognize the word that is written before it recognizes the color
of the written word.

Although this is only a hypothesis, if that's true it can explain the
brain "lag" observed in the incongruent words condition, where overall
the time reported is greater than the ones under the congruent words
condition. If this hypothesis is false, is still possible that the order
the brain recognizes attributes doesn't matter but it highlights the
written name by default and not the color (bias), causing conflict when
attempting to fast and accurately report the color each word is filled
with.
