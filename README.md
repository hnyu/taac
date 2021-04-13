# TASAC: Temporally abstract soft actor-critic for continuous control

This repo contains the experiment configuration files for training TASAC on 5 categories of 14 continuous control tasks as done in the report

> TASAC: Temporally Abstract Soft Actor-Critic for Continuous Control, Yu et al., arXiv 2021.

## Installation

Our experiments use the training pipelines and algorithms of [Agent Learning Framework (ALF)](https://github.com/HorizonRobotics/alf). Please follow ALF's installation instruction to clone and install it:

```bash
git clone https://github.com/HorizonRobotics/alf@
```

On top of the basic ALF installation,
- Two task categories (**Manipulation** and **Locomotion**) require installing [Mujoco](http://www.mujoco.org/). Our experiments use Mujoco 2.0 and a different version might result in a different task. So we suggest using this exact version for the reproduction purpose. Please follow the instructions at ``https://github.com/openai/mujoco-py``.
- One task category **Driving** requires installing [CARLA](https://carla.org/) and we used version [0.9.9](https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/CARLA_0.9.9.tar.gz) in the experiments. Installation instructions can be found in ``<ALF_ROOT>/alf/environments/suite_carla.py``.

After the installation, append the root of this repo to your `PYTHONPATH`:

```bash
export PYTHONPATH=<TASAC_ROOT>:PYTHONPATH
```

## Run experiments

To run an experiment (e.g., training TASAC on four Fetch tasks), you can launch jobs of the four tasks simultaneously via a grid search over environment names under ``<TASAC_ROOT>``:

```bash
cd <TASAC_ROOT>
python -m alf.bin.grid_search --root_dir=<TRAIN_JOB_DIR> --gin_file experiments/tasac/tasac_fetch.gin --search_config experiments/common/fetch.json
```

(This assumes that you have enough resources; see ``fetch.json`` for details.) Or just training a single job on one task:
```bash
cd <TASAC_ROOT>
python -m alf.bin.train --root_dir=<TRAIN_JOB_DIR> --gin_file experiments/tasac/tasac_fetch.gin --gin_param="create_environment.env_name='FetchPickAndPlace-v1'"
```

Then open the Tensorboard to view the training results

```bash
tensorboard --logdir=<TRAIN_JOB_DIR>
```

## Reference
If you use our TASAC algortihm, please consider citing

```
@article{Yu2021TASAC,
    author={Haonan Yu and Wei Xu and Haichao Zhang},
    title={TASAC: Temporally Abstract Soft Actor-Critic for Continuous Control},
    journal={arXiv},
    year={2021}
}
```