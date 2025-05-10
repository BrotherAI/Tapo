Official implementation of the paper:  
**"TAPO: Dynamic Teacher and Perturbed Answer Injection for Policy Optimization"**  
🚀 NeurIPS 2025 Submission · Anonymous Authors

TAPO is a fine-grained reinforcement learning framework that improves reasoning alignment in large language models (LLMs). Built on GRPO, TAPO introduces four innovations to inject token-level learning signals and stabilize optimization:

- ✅ **Dynamic Teacher Injection (DTI)**: Injects contrastive completions (correct/incorrect) into all-correct or all-wrong groups to recover collapsed gradients.
- ✅ **Perturbed Answer Injection (PAI)**: Flips answers of correct completions to create informative contrast and encourage robust reasoning.
- ✅ **Advantage-Level Intervention (ALI)**: Assigns fixed token-level advantages while preserving group normalization.
- ✅ **InfoLen-Aware Reward Shaping**: Penalizes overly long and redundant completions while preserving informativeness.

TAPO outperforms existing RLHF approaches (e.g., GRPO, DAPO) on math reasoning benchmarks such as AIME, MATH500, AMC, and Minerva-Math.

---

## 🔧 Installation

```bash
git clone https://github.com/your-org/tapo.git
cd tapo
conda create -n tapo python=3.10
conda activate tapo
pip install -r requirements.txt
````

> TAPO is built on [VeRL](https://github.com/your-org/verl) and tested with PyTorch 2.1, Transformers 4.39, and 4x NVIDIA 4090 GPUs.

---

## 🧠 Training

To train TAPO from a pretrained policy (e.g., DeepSeek-R1-Distill-Qwen-1.5B):

```bash
python train.py \
  --config configs/tapo_math.yaml \
  --output_dir ./checkpoints/tapo_math \
  --use_dti --use_pai --use_infolen
```

You can ablate any module by removing the corresponding flag. Example: `--no_infolen`.

---

## 📊 Evaluation

Evaluate the trained model using pass\@1 accuracy on AIME / MATH / AMC:

```bash
python eval.py \
  --model_path ./checkpoints/tapo_math \
  --dataset aime2024
```

Evaluation results will be saved to `results/`.

---

## 📁 Project Structure

```
tapo/
├── core/                 # TAPO training components (DTI, PAI, ALI, InfoLen)
├── configs/              # YAML configs for different experiments
├── data/                 # Dataset loading and preprocessing
├── models/               # Model wrappers (Qwen, DeepSeek, etc.)
├── train.py              # Training entry
├── eval.py               # Evaluation script
└── README.md
```

---

## 📈 Results (AIME 2024)

| Model         | AIME Pass\@1 (%) |
| ------------- | ---------------- |
| DeepSeek-Base | 28.9             |
| + Naive GRPO  | 34.3             |
| + TAPO (Full) | **44.3**         |

---

## 📖 Citation

```bibtex
@article{anonymous2025tapo,
  title   = {TAPO: Dynamic Teacher and Perturbed Answer Injection for Policy Optimization},
  author  = {Anonymous Authors},
  journal = {Conference on Neural Information Processing Systems (NeurIPS)},
  year    = {2025}
}
```

---

## 🤝 Acknowledgements

TAPO builds on the ideas of GRPO, DAPO, and VeRL. We thank the authors of DeepSeekMath and OpenAI-o1 for inspiring this line of work.

---

## 📬 Contact

For questions or collaborations, please open an issue or submit a pull request.

```

---

如你想用非匿名版（比如开源后），我也可以帮你加上作者、实验机构等。如果未来模型训练代码/数据依赖变更，也可以帮你写 `setup.py` 或 `docs/` 文档结构。是否需要我也做一版“中英文对照版”README？
```
