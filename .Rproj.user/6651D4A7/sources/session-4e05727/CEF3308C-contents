---
date: "2019-06-17T23:53:00+01:00"
draft: false
hideLastModified: true
summary: Infinite Monkey Theorem
tags:
- R
title: Infinite Monkey
---

Living is the art of dealing with as many problems as there are solutions. For this reason, as long as we are alive, we constantly have to struggle with a number of problems.

There will always be problems, waiting to be solved. All we need to do is to try over and over again to overcome them. Just like Albert Einstein states:

> *"It's not that I'm so smart, it's just that I stay with problems longer."*

In this article, I'm going to repeat the Infinite Monkey theorem using the R programming language, which I think can make you feel better when you think you are in a difficult situation.

------------------------------------------------------------------------

The infinite monkey theorem is a hypothesis that states that an infinite number of monkeys, given an infinite amount of time and typewriters, would eventually produce the complete works of William Shakespeare or any other written text[1]. The idea behind the theorem is that given enough time and randomness, even highly improbable events can occur. The earliest known reference to the idea of monkeys typing at random comes from a 1913 essay by French mathematician Émile Borel, who used the concept to illustrate the concept of probability.

The statistical proof of the theorem can be explained in a basic form as if two events are statistically independent (the events do not affect each other's outcome), the probability of these two events occurring together is equal to the product of the probabilities of these events occurring separately.

In fact, it can also be said that this theorem also points us to the Gambler's Fallacy[2], a logical fallacy that many people fall victim to. To illustrate this fallacy, consider the classical coin toss experiment. Most people assume that because a coin has come up heads several times in a row, it's more likely to come up tails in the next flip. However, it is absolutely impossible to know this for sure. After all, the probability for each independent flip is always 50%. Of course, this only applies if the coin is not cheated.

------------------------------------------------------------------------

Now, I am going to create a monkey to implement this theorem in R. This monkey is of course a function. Then I will try to randomly print some text to this monkey.

I think it is a good coding exercise to put some theorems, thought experiments, ideas into code. Thinking like a machine(algorithmic thinking) can be the most important component to turn the ideas in your mind into code. So, if you are faced with a task that you have never encountered before and you don't know what to do, instead of struggling with writing the code, you can create a road map for yourself. This road map will actually "code" your coding skills. In this project, I will also show how I cope with this situation.

What do I need to do to code the infinite monkey theory?

Of course, I need the monkey! Lets create our monkey that randomly hits keys on a typewriter.

{{< code language="r" >}} monkey_the_author <- function(passage) { chars <- c(letters, ” ") paste0(sample(chars, length(passage[1]), replace = TRUE), collapse ="“) {{< /code >}}

After I have monkey, I need to do the experiment. Let's start with a simple single word, monkey.

To wrote this code, basically, I can say that I think in this way:

*I have a monkey that hits random keys. I'm going to ask this monkey to type a certain text, so I know the length of this text, I know the content of this text. When the monkey presses random keys, I have to make sure that the key it presses is the same as my target passage. And I have to keep doing this until the condition I want is met. So instead of for, I need to use a repeat loop. And the end of this loop is when the monkey reaches the final text.*

To make it easy to understand, I wrote explanation about what each line does in code chunk!

------------------------------------------------------------------------

    passage1 <- ("monkey")

    count <- 0 # I want to know how many hits the monkey needed to write the passage.
    set.seed(123)
    repeat { # I will use repeat loop because the loop has to continue until the condition I want is met.
      count <- count + 1
      test_passage <- rep("", length(passage1)) # vector to store the generated text.
      for (i in 1:length(passage1)) { # iterate through each line 
        for (j in 1:nchar(passage1[[i]])) { # iterate through each character
          test_char <- monkey_the_author(passage1) # monkey hits
          # for each character, the loop generates random strings until a character that matches the corresponding character in the target text is found.
          while (test_char != substr(passage1[[i]], j, j)) { # it uses the substr function to extract the character from the target text and compare it to the generated character.
            test_char <- monkey_the_author(passage1) # if the generated character does not match the target character, the loop generates another random string and continues until a match is found
            count <- count + 1 # to keep track of the number of attempts required
          }
          test_passage[i] <- paste0(test_passage[i], test_char) # Once a match is found, the loop concatenates the matched character to the current line
        }
      }
      if (identical(test_passage, passage1)) { # If the entire test_passage vector matches the passage vector
        break # the loop breaks
      }
    }

Experiment is over. Now, let us check whether the entire test_passage matches the original passage.

    test_passage

    ## [1] "monkey"

Now, let us see how many attempts required to generate the target passage. test_passage

    cat("It took", count, "attempts to generate the target passage.")

    ## It took 148 attempts to generate the target passage.

Even though we succeeded with a low number of attempts, 148, what was the probability that a monkey pressing random keys would type this word correctly?

The word "monkey" has 6 letters. At first, we need to determine the total number of possible ways to draw 6 letters from the 26 letters of the alphabet with replacement. Since we are drawing with replacement, each letter can be drawn more than once, so the number of ways to draw 6 letters from 26 with replacement is:

26⁶ = 26 x 26 x 26 x 26 x 26 x 26 = 308,915,776

This means there are 308,915,776 possible 6-letter combinations that can be drawn with replacement from the alphabet.

To calculate the probability of spelling "monkey", we need to determine how many of these 6-letter combinations contain the letters "m", "o", "n", "k", "e", and "y" in the correct order. Since each letter can be drawn with replacement, the probability of drawing any particular letter is 1/26.

To calculate the probability of drawing all 6 letters in the correct order, we simply multiply the probability of drawing each letter:

(1/26) x (1/26) x (1/26) x (1/26) x (1/26) x (1/26) = 1/308,915,776

So the probability of spelling "monkey" by randomly drawing 6 letters from the alphabet with replacement is approximately 1 in 308,915,776 or 0.000000324%. This is amazing!

------------------------------------------------------------------------

Now, let me repeat the experiment with a more complicated passage which is "monkey wrote this passage". I run the code again by repeating the steps I did for the word "monkey".

    passage2 <- ("monkey wrote this passage")

    # again, the same processes

    count2 <- 0
    set.seed(122)
    repeat {
      count2 <- count2 + 1
      test_passage2 <- rep("", length(passage2))
      for (i in 1:length(passage2)) {
        for (j in 1:nchar(passage2[[i]])) {
          test_char2 <- monkey_the_author(passage2)
          while (test_char2 != substr(passage2[[i]], j, j)) {
            test_char2 <- monkey_the_author(passage2)
            count2 <- count2 + 1
          }
          test_passage2[i] <- paste0(test_passage2[i], test_char2)
        }
      }
      if (identical(test_passage2, passage2)) {
        break
      }
    }

Let us check whether the entire test_passage matches the original passage.

    test_passage2

    ## [1] "monkey wrote this passage"

Let us see how many attempts required to generate the target passage

    cat("It took", count2, "attempts to generate the target passage.")

    ## It took 744 attempts to generate the target passage.

Again, even though we succeeded with a relatively low number of attempts, 744, what was the probability that a monkey pressing random keys would type this word correctly?

The sentence "monkey wrote this passage" has 23 letters. Thus, firstly, we first need to determine the total number of possible ways to draw 23 letters from the 26 letters of the alphabet with replacement. Since we are drawing with replacement, each letter can be drawn more than once, so the number of ways to draw 23 letters from 26 with replacement is:

26²³ = 351,843,720,888,320,000,000,000,000

This means there are 351,843,720,888,320,000,000,000,000 possible 23-letter combinations that can be drawn with replacement from the alphabet.

To calculate the probability of spelling "monkey wrote this passage", we need to determine how many of these 23-letter combinations contain the letters in the correct order. Since each letter can be drawn with replacement, the probability of drawing any particular letter is 1/26.

To calculate the probability of drawing all 23 letters in the correct order, we simply multiply the probability of drawing each letter:

(1/26)²³ = 1/817,0728068870529046... × 10²³

So the probability of spelling "monkey wrote this passage" by randomly drawing 23 letters from the alphabet with replacement(hang on to your hat!) is approximately 1 in 8.170728068870529046... × 10²³ or 0.0000000000000000000000000000000000000000865% !!!!!

Not surprisingly, As the number of words in the passage that the monkeys are asked to write increases, the number of iterations in the loop, i.e. the number of attemps required, will also increase. This inevitable relationship is actually the basis of the theorem. Aside from the astonishment of realizing such low probabilities, however, it is also possible to interpret this theorem from another perspective. For example, it took 148 attempts for monkeys to type the word `monkey` by pressing random keys. What would happen if I used a for loop instead of repeat and iterated the loop 147 times?

Yes, sometimes a certain number of iterations will be enough to achieve the goal. But the thing to never forget is the real key to success: keep going until the condition is met! `Repeat`doing what you need to do to get what you want, until you get what you want! If you are struggling to achieve something you want to achieve and you can't get it even after countless attempts, you either don't have enough time or you don't have enough resources. Keep trying, get the resources you need (try a `repeat`loop instead of a `for`loop), and eventually you will succeed!

> If you have enough time and resources, you can perform an event with a probability of 0.0000000000000000000000000000000000000000000000000000000000000000865%.

Let's end this project with the output of the code whose input I have hidden. Let's see what the monkey wrote for us[3] this time.

    ## i am the master of my fate 
    ##  i am the captain of my soul

------------------------------------------------------------------------

**Readings**

[1] Crowley, John. "The Million Monkeys of M. Borel." Conjunctions 67 (2016): 57--60.

[2] <https://yourlogicalfallacyis.com/the-gamblers-fallacy>

[3] <https://www.poetryfoundation.org/poems/51642/invictus>
