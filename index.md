<!-- <h1 align="center"> Faithful LLMs for Long-Horizon Task Planning </h1> -->

<!--
<div align='center'>
  <font size=4 color=black>ICRA 2024</font>
</div>
-->

<!--
[author1](https://www.yuque.com/zhangjiatao-grdyv/rn49ht/lq7xzy4xmxgrpgz9), [author2](https://www.yuque.com/zhangjiatao-grdyv/rn49ht/vsarazgdts43o7y4)
-->

## Abstract
Recent planning methods based on LLMs typically employ the In-Context Learning paradigm. Complex long-horizon tasks require more context(including instructions and demonstrations) to guarantee generated plan can be executed. However, in such condition, LLMs may overlook(unfaithful) the rules in the given context, resulting in plans that can be invalid or even lead to dangerous actions. In this paper, we investigate the faithfulness of LLMs for complex long-horizon tasks. Inspired by human intelligence, we introduce a novel framework named DiEP. DiEP employs a language-based RNN structure to integrate task decomposition, memory management into LLM planning inference, which could effective improve the faithfulness of LLM and make planner more reliable. We conducted experiments in VirtualHome household tasks. Results show that our model significantly improves faithfulness and success rates for complex long-horizon tasks.


## Video

<div align='center'>
  <video id="video" controls="" preload="none" poster="作者(图片地址)">
    <source src="https://www.youtube.com/embed/MrKrnHhk8IA?rel=0&amp;showinfo=0"  frameborder="0" allow="autoplay; encrypted-media" allowfullscreen>
  </video>
</div>

<div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Video</h2>
        <div class="publication-video">
          <iframe src="https://www.youtube.com/embed/MrKrnHhk8IA?rel=0&amp;showinfo=0"
                  frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
        </div>
      </div>
</div>

## Results
Example of our frameworks for long-horizon task planning:

<div align='center'>
  <img src="https://github.com/tannl/FLTRNN.github.io/blob/main/result.PNG">
</div>

## Methodology
The framework uses the task description as input and outputs the task plan. Our framework consists of three stages: 
1. Decompose a complex, long-horizon task into several simpler sub-tasks and formulate an abstract plan.
2. Represent the task goal, abstract plan, and instruction as long-term memory, while designating the selected sub-goal in the plan, demonstration, and sub-task specifics as short-term memory.
3. Input the combined long and short-term memories and the environment observation into the LLM to retrieve the sub-task plan. Update memory simultaneously and repeat the above steps until the task is complete.

<div align='center'>
  <img src="https://img-blog.csdnimg.cn/aae970d1b957498aa83e3cfd9f0e9a57.png">
</div>

<br/>

<div align='center'>
  <img src="https://img-blog.csdnimg.cn/5b6bb19b0f534fe49aa2cafec9d614b1.png">
</div>

## BibTeX
