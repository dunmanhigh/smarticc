---
title: Recognising patterns with Regex
categories: tutorial
tags: "data"
authors: Lim Yong Jun
image: "/assets/img/2018-11-15-recognising-patterns-with-regex-preview.png"
---

Regular expressions, or regex for short, are patterns used to match character combinations in strings. They are extremely useful in extracting information from text and used in programming languages like Python and JavaScript.

With this simple Google Code-in task, you can quickly learn regex! If you have yet to register for Google Code-in, you can do so at codein.withgoogle.com. Then claim your task, [“[easy] Learn Regex”](https://codein.withgoogle.com/tasks/6361802221813760).

Next, go to RegexOne to learn about regex through short, interactive [exercises](https://regexone.com/lesson/introduction_abcs). 

If you already know regex, you can go straight to solving the task.

![][image-1]

Did you notice a pattern in the records? Each record started with “My username is ”. Hence, you regex should start with ‘My username is ’.

![][image-2]

Each record would then include the username itself. Since each username is unique, we cannot include every single username in the regex. We can solve this by using ‘(\w+). ’. 

![][image-3]

We use ‘\w+’ as it would match any alphanumeric characters of one or more repetitions. ‘\w+’ is placed inside brackets to signify that we are extracting the username and ‘. ’ is placed at the end as it immediately follows the username. Currently, your regex should look like this: ‘My username is (\w+). ’.

Finally, each record would end with a sentence stating an age. The task only requires records of those below 20 years of age. Hence, you can use ‘I am (1[0-9]|[0-9]) .+’.

![][image-4]

The ages can either be one (0-9) or two (10-19) digits. Hence we use to match either option, with ‘|’ separating each option. ‘1[0-9]|[0-9]’ is also placed inside brackets to signify that we are extracting the age of the person. This is placed in between ‘I am ’ and ‘ .+’. We used ‘ .+’ as we do not have to bother about characters after the age. As a result, the final regex to be used is **‘My username is (\w+). I am (1[0-9]|[0-9]) .+’.**

You do not need to have the same regex as shown above and can come up with your very own. You can also test your regex here before submitting the task for review at a previously shown [link](https://codein.withgoogle.com/tasks/6361802221813760).


[image-1]: {{ "/assets/img/2018-11-15-recognising-patterns-with-regex-1.png" | absolute_url }}
[image-2]: {{ "/assets/img/2018-11-15-recognising-patterns-with-regex-2.png" | absolute_url }}
[image-3]: {{ "/assets/img/2018-11-15-recognising-patterns-with-regex-3.png" | absolute_url }}
[image-4]: {{ "/assets/img/2018-11-15-recognising-patterns-with-regex-4.png" | absolute_url }}
