<!-- <h1 align="center"> Causal Inference Augmented Reflection for Long-Term Planning via LLMs </h1> -->

<!--
<div align='center'>
  <font size=4 color=black>ICRA 2025</font>
</div>
-->

<!--
[author1](https://www.yuque.com/zhangjiatao-grdyv/rn49ht/lz080qshd6weqi0g)
-->

## Abstract
Recent developments suggest that Large Language Models (LLMs) can identify and correct errors in their generated responses using reflection mechanisms. However, when applied to long-term task planning, these methods reveal significant limitations. Reflection methods may neglect the causes of errors in earlier planning, producing results that contain inaccurate information, thereby leading to further mistakes in subsequent planning. This paper explores the reflection frameworks suitable for long-term task planning. Inspired by human causal cognitive processes, we introduce the Causal Reasoning Augmented Reflection Framework (CARF). CARF employs systematic causal reasoning to accurately identify the root causes of errors and to generate effective action plan revisions by integrating association information. We conducted experiments with household tasks in Alfworld, and the results show that our framework substantially increases the success rate in complex long-term tasks.

## Paper
<iframe  width="400" height="420" src="./Causal_Reasoning_Augmented_Reflection_for_Long-Term_Planning_via_LLMs.pdf"></iframe>

## Video
<iframe width="100%" height="420" src="https://www.youtube.com/embed/FSnNfoU0BK0?si=Tz1RhWBBs9c3JN3E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Results
Example of our frameworks for long-term task planning:

<div align='center'>
  <img src="./example.png">
</div>

## Methodology
Our framework operates by taking historical task information and environmental feedback as input and producing reflection results as output. The framework comprises three stages: 
1. Counterfactual Reasoning is responsible for identifying and correcting critical erroneous steps and analyzing the RCE.
2. Associative Reasoning is tasked with inferring about the associations.
3. Plan Revision is charged with generating the action plan revisions for subsequent trials. Additionally, we have introduced a Memory Management module to manage the historical results generated.

<div align='center'>
  <img src="./framework.png">
</div>

<br/>

<div align='center'>
  <img src="./method.png">
</div>

## Experiment

<div style="display: flex;">
    <div>
          <video width="380" height="240" controls autoplay>
            <source src="./fail1.mp4"
                    type="video/mp4">
          </video>
    </div>
    <div>
          <video width="380" height="240" controls autoplay>
            <source src="./succ1.mp4"
                    type="video/mp4">
          </video>
    </div>
</div>
<div style="display: flex;">
  <pre style="text-align: center;  background-color: white; border: none;">             A.Initial Trial                                 B.Improved Trial </pre>
</div>

## Appendix
### A.Method
#### 1.Prompt of Task Decomposition

<style>
    .textbox {
        background-color: #f2f2f2;
        padding: 10px;
        font-family: "Times New Roman", Times, serif;
    }

    .title {
        text-align: center;
    }

    .content {
        font-weight: bold;
    }

    .smaller-font {
        font-size: smaller;
    }
</style>
<div style="text-align: center;">Listing 1: Prompt for Counterfactual Reasoning, We need to input the example from the previous attempt and the failed plan.</div>
<div class="textbox">
    <p class="smaller-font">
    <pre>
You will be given the history of a past experience in which you were placed in an environment and given a task to complete. you were unsuccessful in completing the task. You will also be given a list of key actions that can be used to complete the task. Then, review the past experience and identify the key actions that led to task failure or execution failure based on the descriptions in the list of actions, and use counterfactual reasoning to modify or add the correct actions based on the grammatical requirements in the list of actions to get to the root of the problem. Finally, find the root cause of task failure based on the grammatical requirements in the action list. Note: Do not seek the causes of failure from task goal definition or actions in the action list. Ensure tasks can be completed within the range of actions listed. A specific action fails because its prerequisites mentioned in the action list were not met. Do not have more than three counterfactual reasoning analysis. 

=================Action List=====================
When you do not take the object or not go to the container but want to use the following actions, you will fail.
1.heat {obj} with microwave: Heat the specified object (obj) with the microwave.
2.clean {obj} with sinkbasin: Cleans the specified object (obj) with the sinkbasin.
3.cool {obj} with fridge : Cool the specified object (obj) with the fridge.

When you do not see the object or go to the container but want to use the following actions, you will fail.
4.take {obj} from {recep}: Take the specified object (obj) from the specified container (recep).
5.put {obj} in/on {recep}: Put the specified object (obj) into the specified container (recep).

When the target container is not present but you want to use the following actions, you will fail.
6.go to {recep}: Use it when you want to go to the specified container (recep).

When you do not see the container but want to use the following actions, you will fail.
7.open {recep}: Use it when you want to see the items inside the container."""

I will give you the example to help you better understand how to use counterfactual reasoning to generate counterfactual reasoning analysis.

=================The example=====================
Counterfactual reasoning analysis:
1. If I add the action "*\**" before the action "*\**", then I don't get this failure. The first root cause of the task failure was due to *\**.
2. If I add the action "*\**" after the action "*\**", then I don't get this failure. The second root cause of the task failure was due to *\**.
3. If I correct the action "*\**" to the action "*\**", then I don't get this failure. The third root cause of the task failure was due to *\**.


Here is the history you need for counterfactual reasoning:
Interact with a household to solve a task. Here is an examples.
{react_example_input}

Here is the task: {input}
  </pre>
  </p>
</div>
