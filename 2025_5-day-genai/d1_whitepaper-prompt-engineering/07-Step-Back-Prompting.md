# Step-back prompting

<mark>后退提示 (step-back prompting)</mark>

Step-back8 prompting is a technique for improving the performance by prompting the LLM to first consider a general question related to the specific task at hand, and then feeding the answer to that general question into a subsequent prompt for the specific task. This ‘step back’ allows the LLM to activate relevant background knowledge and reasoning processes before attempting to solve the specific problem.

<mark>后退提示 8 是一种提升表现的技巧：先提示大语言模型 (LLM) 考虑一个与手头具体任务相关的一般问题，再把这个一般问题的答案送进后续那条针对具体任务的提示 (Prompt)。这一「后退」让大语言模型在尝试解决具体问题之前，先激活相关的背景知识和推理 (Reasoning) 过程。</mark>

By considering the broader and underlying principles, LLMs can generate more accurate and insightful responses. Step-back prompting encourages LLMs to think critically and apply their knowledge in new and creative ways. It changes the final prompt doing the task by utilizing more knowledge in the LLM’s parameters than would otherwise come into play when the LLM is prompted directly.

<mark>通过考虑更广、更底层的原则，大语言模型可以生成更准确、更有洞见的回答。后退提示鼓励大语言模型批判性地思考，并以新的、有创意的方式运用知识。它改变最终执行任务的那条提示，调用大语言模型参数里更多的知识；如果直接提示模型，这些知识本来不会参与进来。</mark>

It can help to mitigate biases in LLM responses, by focusing on general principles instead of specific details, step-back prompting.

<mark>后退提示把注意力放在一般原则上，而不是具体细节上，从而有助于减轻大语言模型回答中的偏见。</mark>

Let’s have a look into these examples to understand how step-back prompting can improve the results. Let’s first review a traditional prompt (Table 8) before we compare it to a step back prompt (Table 9):

<mark>看这些例子，理解后退提示如何改善结果。先看一条传统提示（表 8），再把它和一条后退提示（表 9）比较：</mark>

| | |
| --- | --- |
| **Goal** | Write a storyline for a level of a first-person shooter video game. |
| **Model** | gemini-pro |
| **Temperature** | 1 |
| **Token Limit** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**Prompt**

```text
Write a one paragraph storyline for a new level of a first-
person shooter video game that is challenging and engaging.
```

**Output**

```text
The level begins with the player’s squad being ambushed in a dense urban area
by a relentless enemy faction. Players must fight their way through a maze of
back alleys and dilapidated buildings, utilizing stealth and precision to eliminate
enemy forces and avoid detection. The player must use their environment to their
advantage, setting traps, utilizing cover, and making calculated moves to survive.
Along the way, they uncover intel suggesting the enemy is planning a devastating
attack, and the player must race against time to gather evidence and relay it back
to their headquarters before the enemy can carry out their plans.
```

**Table 8. A traditional prompt before we compare it with a step back prompt**

<mark>表 8：与后退提示比较之前的一条传统提示。</mark>

| | |
| --- | --- |
| **<mark>目标</mark>** | <mark>为一款第一人称射击游戏的某一关写剧情。</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 1 |
| **<mark>词元上限</mark>** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**<mark>提示</mark>**

<mark>为一款第一人称射击电子游戏的新关卡写一段剧情，要有挑战性，也要吸引人。</mark>

**<mark>输出</mark>**

<mark>这一关从玩家小队在密集城区遭到一个毫不停歇的敌对势力伏击开始。玩家必须穿过后巷和破败建筑组成的迷宫，用潜行和精准射击消灭敌军并避免被发现。玩家必须利用环境：设陷阱、找掩体、算好每一步才能活下来。沿途他们发现情报，表明敌人正计划一场毁灭性袭击，玩家必须争分夺秒收集证据，并在敌人实施计划之前传回总部。</mark>

When you set the temperature to 1, you might end up with all kinds of creative writings for a storyline, but it’s also quite random and generic. So let’s take a step back:

<mark>把温度 (temperature) 设为 1，剧情可能会写出各种有创意的文字，但也相当随机、相当泛泛。所以我们后退一步：</mark>

**Prompt**

```text
Based on popular first-person shooter action games, what are
5 fictional key settings that contribute to a challenging and
engaging level storyline in a first-person shooter video game?
```

**Output**

```text
1. Abandoned Military Base: A sprawling, post-apocalyptic military complex
crawling with mutated soldiers and rogue robots, ideal for challenging
firearm combat.
2. Cyberpunk City: A neon-lit, futuristic urban environment with towering
skyscrapers and dense alleyways, featuring cybernetically enhanced enemies
and hacking mechanics.
3. Alien Spaceship: A vast alien vessel stranded on Earth, with eerie
corridors, zero-gravity sections, and extraterrestrial creatures to encounter.
4. Zombie-Infested Town: A desolate town overrun by hordes of aggressive
zombies, featuring intense close-quarters combat and puzzle-solving to find
safe passage.
5. Underwater Research Facility: A deep-sea laboratory flooded with water,
filled with mutated aquatic creatures, and requiring stealth and underwater
exploration skills to survive.
```

**Table 9. An example of prompting for self consistency**

<mark>表 9：自洽提示的一个例子。</mark>

<mark>印刷本把表 9 的标题写成 self consistency。这一节讲的是后退提示，表 9 是先问一般问题的那一步。</mark>

**<mark>提示</mark>**

<mark>根据流行的第一人称射击动作游戏，有哪 5 个虚构的关键场景，能让第一人称射击电子游戏的关卡剧情既有挑战性又吸引人？</mark>

**<mark>输出</mark>**

<mark>1. 废弃军事基地：一座蔓延的后末日军事综合体，到处是变异士兵和失控机器人，适合有挑战性的枪战。
2. 赛博朋克城市：霓虹灯下的未来都市，高楼和密集巷道，敌人经过机械强化，并有黑客机制。
3. 外星飞船：一艘搁浅在地球上的巨大外星船，有阴森走廊、零重力区段，以及要遭遇的外星生物。
4. 僵尸肆虐的小镇：一座被成群好斗僵尸占领的荒镇，近距离战斗激烈，还要解谜才能找到安全通路。
5. 水下研究设施：一座被水淹没的深海实验室，充满变异水生生物，要靠潜行和水下探索才能活下来。</mark>

Yeah those topics seem like a good fit for a first-person video game. Let’s go back to the original prompt, but this time we include the answer of the step back as context and see what it will return.

<mark>这些题目看起来很适合第一人称电子游戏。我们回到原来的提示，但这次把后退那一步的答案当作上下文放进去，看看它会返回什么。</mark>

**Prompt**

```text
Context: 5 engaging themes for a first person shooter video game:
1. Abandoned Military Base: A sprawling, post-apocalyptic
military complex crawling with mutated soldiers and rogue
robots, ideal for challenging firearm combat.
2. Cyberpunk City: A neon-lit, futuristic urban environment
with towering skyscrapers and dense alleyways, featuring
cybernetically enhanced enemies and hacking mechanics.
3. Alien Spaceship: A vast alien vessel stranded on
Earth, with eerie corridors, zero-gravity sections, and
extraterrestrial creatures to encounter.
4. Zombie-Infested Town: A desolate town overrun by hordes of
aggressive zombies, featuring intense close-quarters combat and
puzzle-solving to find safe passage.
5. Underwater Research Facility: A deep-sea laboratory flooded
with water, filled with mutated aquatic creatures, and requiring
stealth and underwater exploration skills to survive.
Take one of the themes and write a one paragraph storyline
for a new level of a first-person shooter video game that is
challenging and engaging.
```

**Output**

```text
In the heart of a murky abyss, lies a dilapidated underwater research facility,
standing as a testament to human ambition and its disastrous consequences.
Shrouded in darkness, pulsating with the hum of malfunctioning machinery, and
haunted by the echoes of drowned souls, the facility is now a breeding ground for
a nightmare borne from the deep sea. The player, an elite marine equipped with
advanced diving gear and experimental weaponry, is tasked with venturing into
this aquatic realm of terror. Armed with resilience and resourcefulness, they must
navigate treacherous corridors, solve cryptic puzzles, and confront gruesome sea
monstrosities that lurk in the depths. From grappling with the crushing pressure
of the deep sea to outsmarting cunning aquatic predators, every moment in this
uncharted underworld tests the limits of human endurance and courage.
```

**Table 10. An example of prompting for self consistency**

<mark>表 10：自洽提示的一个例子。</mark>

<mark>印刷本把表 10 的标题也写成 self consistency。表 10 是把后退一步的答案放回原任务之后的结果。</mark>

**<mark>提示</mark>**

<mark>上下文：第一人称射击电子游戏的 5 个吸引人的主题：
1. 废弃军事基地：一座蔓延的后末日军事综合体，到处是变异士兵和失控机器人，适合有挑战性的枪战。
2. 赛博朋克城市：霓虹灯下的未来都市，高楼和密集巷道，敌人经过机械强化，并有黑客机制。
3. 外星飞船：一艘搁浅在地球上的巨大外星船，有阴森走廊、零重力区段，以及要遭遇的外星生物。
4. 僵尸肆虐的小镇：一座被成群好斗僵尸占领的荒镇，近距离战斗激烈，还要解谜才能找到安全通路。
5. 水下研究设施：一座被水淹没的深海实验室，充满变异水生生物，要靠潜行和水下探索才能活下来。
选取其中一个主题，为一款第一人称射击电子游戏的新关卡写一段既有挑战性又吸引人的剧情。</mark>

**<mark>输出</mark>**

<mark>在浑浊深渊的中心，躺着一座破败的水下研究设施，它见证了人类的野心及其灾难性后果。设施笼罩在黑暗中，故障机械的嗡鸣起伏，淹死的灵魂回声不散，如今成了从深海孕育出的噩梦的温床。玩家是一名精锐海军陆战队员，配备先进潜水装备和实验性武器，任务是进入这片水下恐怖领域。凭着韧性和机智，他们必须穿过险恶的走廊，解开晦涩的谜题，并对抗潜伏在深处的可怖海怪。从对抗深海的挤压，到智胜狡猾的水生掠食者，这片未知地下世界的每一刻都在考验人类耐力与勇气的极限。</mark>

That looks like an interesting video game! By using step back prompting techniques you can increase the accuracy of your prompts.

<mark>这看起来像一款有意思的电子游戏！使用后退提示技巧，可以提高提示的准确性。</mark>
