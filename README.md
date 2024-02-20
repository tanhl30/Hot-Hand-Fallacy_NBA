# A Simple Analysis of Hot Hand Fallacy in the NBA
## Introduction

Hot hand fallacy is a phenomenon, or some considered cognitive bias, where a person who experience a successful outcome has a greater chance of success in further attempts. 
While it has many real life implications in the field of stock-buying and gambling, it is most famously applied in basketball, where a shooter is more likely to hit their next shot 
after hitting the previous shot, ie, having the 'hot hand'

Whether hot hand exist in the nba is still widely debatable, as research have find evidences for both sides, depending how the condition of the shot is set. Today, I want to do a simple analysis
on Hot Hand Fallacy using Conditional Probability and t-test.

## Conditional Probability
We define Conditional Probability of hitting a shot given hitting the previous shot as:

$$Conditional \ Probability=\frac{Probability \ of \ Making \ Consecutive \ Shots}{Probability \ of \ Making \ Previous \ Shot}$$

To obtain that, we created two new variables:
- `lag_shot_hit` : whether previous shot is made
- `conse_shot_hit` : whether both previous shot and current shot are made
  
Following is an exaple of our data with player Breadley Beal in a game. Note that the first shot of him in the game is removed due to having a NULL value for `lag_shot_hit`

![image](https://github.com/tanhl30/Hot-Hand-Fallacy_NBA/assets/73421294/f2dfc5ea-3657-47f2-b63d-20c0393c543a)


Next, we obtained an average of `lag_shot_hit` and `conse_shot_hit` over an entire season for every player, and calculated the actual probability that a player will hit a shot in that season (`FG%`). 
To remove player who only shoot very few shot every game, we filtred out players who shot less than 200 shot in the season.

![image](https://github.com/tanhl30/Hot-Hand-Fallacy_NBA/assets/73421294/e858d1d4-a12a-4618-8630-42d8112a5959)

We see that while some players have a higher conditional probability than their actual probability (thus having hot hand), it seems like there are an equal amount of players who had the reverse.
To test the result more rigorously, we do a paired t-test, with null hypothesis being that the mean of conditional probability of these players are equal to their actual probability.

![image](https://github.com/tanhl30/Hot-Hand-Fallacy_NBA/assets/73421294/bba5de58-717b-4f9c-9190-4c717ace698e)

With Conditional Prob > Actual Prob as alternative hypothesis (Hot Hand), we have an very high p-value. Thus **we do not have enough evidence to support Hot Hand**. However, we have enough evidence to conclude the 
reverse of hot hand, ie the player is more likely to miss a shot after hitting the previous one, due to the small p-value when we put Conditional Prob < Actual Prob as alternative hypothesis.


## Conclusion
While our simple analysis reject the existence of Hot Hand, it is not enought to fully deny Hot Hand. There are a variety of conditions that we did not consider, such as:
- player shooting location (eg mid-range or three-pointer)
- player shot type (eg pull up or catch & shoot)
- the cool-off time between two shots
- defender distance when the shot is taken
- home court or away court
- game score (eg leading or losing the game)

It will be interesting to read more research papers on this topic and learn from their analysis method.
