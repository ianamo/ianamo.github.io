---
layout: post
title: Deepseek -- how much is hype?
---

You've probably heard a lot about the Chinese AI Deepseek. It has been outperforming proprietary AIs on a bunch of benchmarks, and it was supposedly trained with much less expense than went into creating American models like Chat-GPT. This has sent stocks tumbling, and stoked fears about an AI bubble bursting. I was excited to download the model and give it a shot &mdash; I have been experimenting for a while with running LLMs locally, including for such shady deeds as having it [write my thank-you notes](https://ianamo.github.io/2024/11/27/ethics-thankyous-ai.html) (not that I've ever actually used that script...). 

My latest project is one called [Algo-Tutor](https://github.com/ianamo/algo-tutor). I've been trying to brush up on my algorithms using LeetCode, and was hoping to leverage LLMs as a kind of tutor when I couldn't quite get the hang of a problem. Unfortunately, Chat-GPT would skip straight to telling me the answer without trying to guide me along. So I decided to try running LLMs locally with a custom system prompt so that it would spin up a chat session stepping me through the problem. I'm just running a MacBook Air on Apple Silicon, so I can't run the biggest models, but I got reasonably good results from Gemma2 and Llama3.2 at about the two billion parameter range. 

So I figured, why not try DeepSeek for the same task? At first I had made a mistake, because the script just hung there after I entered the command. From other experiments, however, I knew that DeepSeek's pre-thinking stage meant that it had to run for a while before spitting out an answer, so I decided to let it run and see what I got. 

I checked back later and saw that I had a result.

A result which was, according to `wc -w`, 29,000 words long.

A prompt that triggered a short response and chat with another model triggered DeepSeek to write a doctoral dissertation!

Much of what it produced was not necessarily incoherent. The example script I had run through (the same script I had used to test the other models) was a Go program for removing duplicates from an ordered array that wasn't quite right. Initially, DeepSeek's response does attempt to address that problem:

> Okay, so I've got this function called removeDuplicates that's supposed to take an array of integer
s and remove any duplicates by keeping only the first occurrence. But it doesn't look right. Let me
 try to figure out what's going wrong.

>First, looking at the code:

```go
func removeDuplicates(nums []int) int {
    rPtr := 0 // where do repeats begin?
    for _, v := range nums {
        if v != nums[rPtr] {
            nums[rPtr+1] = v
            rPtr++
        }
    }
    return rPtr
}
```
>Hmm, okay. The function starts by initializing rPtr to 0. It then iterates over each element in the
 array using a range loop. For each value v, it checks if it's different from nums`[rPtr]`. If so, it
 moves the duplicate forward and increments rPtr.

>Wait a minute, when I run this code with an example, like `nums = [1, 2, 2, 3]`, what happens? Let me
 walk through it step by step.

>Initially, rPtr is 0. The first element is 1. Since `1 == nums[0]`, which is also 1, the condition v
!= `nums[rPtr]` becomes false. So nothing happens; `rPtr` stays at 0.

>Next, `nums[1]` is 2. It's not equal to `nums[0]` (which is 1), so we set `nums[rPtr+1] = 2` and incremen
t `rPtr` to 1.

>Now, processing the third element, which is also 2. We check if it's equal to `nums[1]`, which is 2.
So again, the condition is false; nothing happens here either. Wait, but I thought we should only c
hange elements when a new value comes in after the duplicates have been skipped.

>Wait no, maybe this isn't handling cases where multiple duplicates are encountered. Like, if nums is `[2, 2, 3]`, then rPtr starts at 0. The first v is 2; it's equal to `nums[0]`, so nothing happens, but we should move the duplicate forward and increment `rPtr`.

>Wait, no—when you process each element in order. So for `[2, 2, 3]`:

>`rPtr = 0`

So far, not bad, really. Some of this could be helpful, I guess. The trouble is that it continues second guessing itself and taking other approaches to the problem for another 28,500 words. Not that far later, it has already managed to segue itself into a discussion of algebra that seems pretty tangential:

>Wait another Idea: Let me think about the possible functions and see if any can result in -4 for Test case3 with x=-1 and y=1.                                                                                                                                                                           >Examples:
>Function f(x,y) = x^3 + y^2 → (-1)^3 +1^2 =-1+1=0→ no.                                                                                                                                                f(x,y)=x^5 + y^5→-1+1=0→ nope.                                                                                                                                                                        f(x,y)= (x+y)^n: For n= something? 0^n is undefined, so no.                                                                                                                                           Alternatively, maybe f is a product with some exponents:
>                                                                                                   f(x,y) = x * y^2 → (-1)*1= -1. No.                                                                                                                                                                    Or f(x,y)=x^2*y: 1*1=1→ nope.                                                                                                                                                                         Hmm.                                                                                                                                                                                                  Wait another Idea: Maybe the function involves higher-order operations but in series. Like first take something with exponents and then do another operation on the result.

...and so on. By the end, here is DeepSeek's executive summary:

>### Summary

>Substitution in algebra is a versatile method used across various structures, including linear equations, systems, functions, word problems, and quadratic equations. By systematically applying substitution, students can solve for variables and analyze relationships between different quantities. This approach emphasizes logical reasoning, problem-solving, and the interconnected nature of algebraic concepts.

>- **Linear Equations:** Basic introduction to solving for variables.
>- **System of Equations:** Extension using substitution across two or more equations.
>- **Function Composition:** Application in multiple iterations and compositions.
>- **Word Problems:** Real-world application showing versatility.
>- **Quadratic Equations:** Advanced technique using completing the square.

>Each section builds on previous knowledge, reinforcing algebraic manipulation and its practical applications.

I guess it got there somehow, but with 29,000 words it had a lot of time to work its way. A reuslt like this makes me wonder if a lot of the supposedly strong performance of DeepSeek comes from benchmarks that might bear only a tenuous connection to real world use cases. Some of the weirdness here _could_, I suppose, derive from the model's small size, but then again, I got reasonable results from a lot of other small models. It will be interesting to see whether some of the early enthusiasm for DeepSeek evaporates as people try using it to, you know, do stuff. 
