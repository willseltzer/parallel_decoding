Example implementation of parallel decoding from [Skeleton-of-Thought:
Large Language Models Can Do Parallel Decoding](https://arxiv.org/pdf/2307.15337.pdf).

This approach seems to be effective for queries where the query has independent subcomponents. For example,

in `What are some practical tips for individuals to reduce their carbon emissions?` each practical tip is independent, so you first have an LLM return a skeleton like:

```
    1. Energy conservation.
    2. Efficient transportation.
    3. Home energy efficiency.
    4. Reduce water consumption.
    5. Sustainable diet.
    6. Sustainable travel.
```

Then you send a parallel request for each subcomponent with one request per "point". 

You could also imagine this working well for code, where you ask the scaffolding to give you the function interfaces. Then you dispatch each function to be written. However, this assumes the functions don't depend on each other in any way (no global state).

However, this approach is quite poor for cases like Math problems where you want chain-of-thought reasoning. 
<img width="534" alt="Screenshot 2023-08-20 at 4 42 27 PM" src="https://github.com/willseltzer/parallel_decoding/assets/1661264/1c0b8fe5-3797-424c-a0c7-20614382dfc4">
and fermi estimates
<img width="554" alt="Screenshot 2023-08-20 at 4 43 12 PM" src="https://github.com/willseltzer/parallel_decoding/assets/1661264/eef74ccd-7fe1-4471-b1ce-835edbab8d02">

# How to experiment
* Set OPENAI_API_KEY to your openai api key. 
