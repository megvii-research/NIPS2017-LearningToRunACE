# NIPS2017-LearningToRun with ACE
[Zhewei Huang](https://scholar.google.com/citations?user=zJEkaG8AAAAJ&hl=zh-CN&oi=sra), [Shuchang Zhou](https://scholar.google.com/citations?user=zYI0rysAAAAJ&hl=zh-CN&oi=sra), BoEr Zhuang, [Xinyu Zhou](https://scholar.google.com/citations?user=Jv4LCj8AAAAJ&hl=zh-CN&oi=ao)

![Demo](https://github.com/hzwer/NIPS2017-LearningToRun/raw/master/demo/hzwer-NIPS2017-LearningToRun-small.gif)

A keras solution for 2nd place [NIPS RL 2017 challenge](https://www.crowdai.org/challenges/nips-2017-learning-to-run/leaderboards?challenge_round_id=12).

There is a [slide](https://docs.google.com/presentation/d/1dgXDFlr62jQ-OdEoYVCGwuUgux3u-jrMaXVp94OVOSk/edit?usp=sharing), a [lecture](https://drive.google.com/open?id=15_XBOms-T1G1jeiDm7xGTn2JGQ2FviT5) and a [writeup(arxiv)](https://arxiv.org/abs/1712.08987) about our work.

## To Run
### preparation

These instructions expect that opensim-rl conda environment is already setup as described in : https://github.com/stanfordnmbl/osim-rl/ .

```
$ source activate opensim-rl
```

Other dependencies is needed as follow
* Keras(since old version does not support selu activation)
* TensorFlow
* matplotlib
* numpy
* Pyro4
* parse
* pymsgbox(optional)

### parallelism

This version requires farming, before starting `train.py`, you should first start some farms by running `python farm.py` on each <u>SLAVE</u> machine you own. Then  create a `farmlist.py` in the working directory (on the <u>HOST</u> machine) with the following content :

```
farmlist_base = [('127.0.0.1', 4), ('192.168.1.1', 8)]

# a farm of 4 cores is available on localhost, while a farm of 8 is available on another machine.

# expand the list if you have more machines.

# this file will be consumed by the host to find the slaves.
```
Try `python farm.py --help` to get more information about how to set the environment.

More information can be found in https://github.com/ctmakro/stanford-osrl .

Thanks to @ctmakro for providing us with this frame.

### test

Test the model in parallel and calculate the average score.

We provide you with some [trained parameters](https://drive.google.com/open?id=10RDVQA5zjUjNXz7Igak3k92_s_XKI2Uw).

```
python test.py -a=10 -c=5 -t=200 -p logs

# test the model for 200 times with 10 actor networks and 5 critic networks ensemble

# the network parameters should be placed as logs/actormodel1.h5 ... logs/actormodel10.h5
```

Try `python test.py --help` to get more information .

## Contributors

- [hzwer](https://github.com/hzwer)
- [floz](https://github.com/NewGod)

## Resources
- [Official YouTube demos](https://www.youtube.com/watch?v=rhNxt0VccsE)
- [赛后专访](https://www.leiphone.com/news/201711/b2OfTdcMUmpYKx6S.html)
- Also a teaser video from the winning team https://www.bilibili.com/video/BV1jE411B74u
