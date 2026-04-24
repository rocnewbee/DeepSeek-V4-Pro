---
license: mit
library_name: transformers
---
# DeepSeek-V4 : vers une intelligence à contexte d’un million de tokens, hautement efficace

<!-- markdownlint-disable first-line-h1 -->
<!-- markdownlint-disable html -->
<!-- markdownlint-disable no-duplicate-header -->

<div align="center">
  <img src="https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/logo.svg?raw=true" width="60%" alt="DeepSeek-V4" />
</div>
<hr>
<div align="center" style="line-height: 1;">
  <a href="https://deepseekfr.org/" target="_blank" style="margin: 2px;">
    <img alt="Homepage" src="https://github.com/deepseek-ai/DeepSeek-V2/blob/main/figures/badge.svg?raw=true" style="display: inline-block; vertical-align: middle;"/>
  </a>
  <a href="https://deepseekfr.org/" target="_blank" style="margin: 2px;">
    <img alt="Chat" src="https://img.shields.io/badge/🤖%20Chat-DeepSeek%20V4-536af5?color=536af5&logoColor=white" style="display: inline-block; vertical-align: middle;"/>
  </a>
</div>
<div align="center" style="line-height: 1;">
  <a href="https://huggingface.co/Rooc" target="_blank" style="margin: 2px;">
    <img alt="Hugging Face" src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-DeepSeek%20AI-ffc107?color=ffc107&logoColor=white" style="display: inline-block; vertical-align: middle;"/>
  </a>
  <a href="https://twitter.com/deepseek_ai" target="_blank" style="margin: 2px;">
    <img alt="Twitter Follow" src="https://img.shields.io/badge/Twitter-deepseek_ai-white?logo=x&logoColor=white" style="display: inline-block; vertical-align: middle;"/>
  </a>
</div>
<div align="center" style="line-height: 1;">
  <a href="LICENSE" style="margin: 2px;">
    <img alt="License" src="https://img.shields.io/badge/License-MIT-f5de53?&color=f5de53" style="display: inline-block; vertical-align: middle;"/>
  </a>
</div>

<p align="center">
  <a href="https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro/blob/main/DeepSeek_V4.pdf"><b>Rapport technique</b>👁️</a>
</p>

## Introduction

Nous présentons une version d’aperçu de la série **DeepSeek-V4**, comprenant deux puissants modèles de langage Mixture-of-Experts (MoE) — **DeepSeek-V4-Pro** avec 1,6T de paramètres (49B activés) et **DeepSeek-V4-Flash** avec 284B de paramètres (13B activés) — tous deux prenant en charge une longueur de contexte d’**un million de tokens**.

La série DeepSeek-V4 intègre plusieurs améliorations clés en matière d’architecture et d’optimisation :

1. **Architecture d’attention hybride :** nous concevons un mécanisme d’attention hybride combinant la Compressed Sparse Attention (CSA) et la Heavily Compressed Attention (HCA) afin d’améliorer drastiquement l’efficacité sur les longs contextes. Dans le réglage de contexte à 1M de tokens, DeepSeek-V4-Pro ne nécessite que **27 % des FLOPs d’inférence d’un seul token** et **10 % du cache KV** par rapport à DeepSeek-V3.2.
2. **Hyperconnexions à contrainte de variété (Manifold-Constrained Hyper-Connections, mHC) :** nous intégrons les mHC pour renforcer les connexions résiduelles classiques, améliorant la stabilité de la propagation du signal à travers les couches tout en préservant l’expressivité du modèle.
3. **Optimiseur Muon :** nous utilisons l’optimiseur Muon pour une convergence plus rapide et une meilleure stabilité d’entraînement.

Nous pré-entraînons les deux modèles sur plus de **32T** de tokens diversifiés et de haute qualité, suivis d’un pipeline complet de post-entraînement. Le post-entraînement suit un paradigme en deux étapes : culture indépendante d’experts spécialisés par domaine (via SFT et RL avec GRPO), puis consolidation unifiée du modèle par distillation on-policy, intégrant des compétences distinctes issues de domaines variés dans un seul modèle.

**DeepSeek-V4-Pro-Max**, le mode de raisonnement à effort maximal de DeepSeek-V4-Pro, fait progresser de manière significative les capacités de connaissance des modèles open source, s’imposant fermement comme le meilleur modèle open source disponible aujourd’hui. Il atteint des performances de tout premier plan sur les benchmarks de code et réduit considérablement l’écart avec les meilleurs modèles fermés sur les tâches de raisonnement et les tâches agentiques. Par ailleurs, **DeepSeek-V4-Flash-Max** obtient des performances de raisonnement comparables à la version Pro lorsqu’on lui accorde un budget de réflexion plus important, bien que sa plus petite échelle de paramètres le place naturellement un peu en retrait sur les tâches de connaissance pures et les workflows agentiques les plus complexes.

<div align="center">
 <img src="assets/dsv4_performance.png" >
</div>

## Téléchargements du modèle

<div align="center">

| **Modèle** | **# Paramètres totaux** | **# Paramètres activés** | **Longueur de contexte** | **Précision** | **Téléchargement** |
| :---: | :---: | :---: | :---: | :---: | :---: |
| DeepSeek-V4-Flash-Base | 284B | 13B | 1M | FP8 Mixed | [HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-Base) \| [ModelScope](https://modelscope.cn/models/deepseek-ai/DeepSeek-V4-Flash-Base) |
| DeepSeek-V4-Flash | 284B | 13B | 1M | FP4 + FP8 Mixed* | [HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) \| [ModelScope](https://modelscope.cn/models/deepseek-ai/DeepSeek-V4-Flash) |
| DeepSeek-V4-Pro-Base | 1.6T | 49B | 1M | FP8 Mixed | [HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-Base) \| [ModelScope](https://modelscope.cn/models/deepseek-ai/DeepSeek-V4-Pro-Base) |
| DeepSeek-V4-Pro | 1.6T | 49B | 1M | FP4 + FP8 Mixed* | [HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) \| [ModelScope](https://modelscope.cn/models/deepseek-ai/DeepSeek-V4-Pro) |

</div>

*\*FP4 + FP8 Mixed : les paramètres des experts MoE utilisent la précision FP4 ; la plupart des autres paramètres utilisent FP8.*

## Résultats d’évaluation

### Modèle de base

<div align="center">

| Benchmark (métrique) | # Shots | DeepSeek-V3.2-Base | DeepSeek-V4-Flash-Base | DeepSeek-V4-Pro-Base |
| :--- | :---: | :---: | :---: | :---: |
| Architecture | - | MoE | MoE | MoE |
| # Paramètres activés | - | 37B | 13B | 49B |
| # Paramètres totaux | - | 671B | 284B | 1.6T |
| **Connaissances du monde** | | | | |
| AGIEval (EM) | 0-shot | 80.1 | 82.6 | **83.1** |
| MMLU (EM) | 5-shot | 87.8 | 88.7 | **90.1** |
| MMLU-Redux (EM) | 5-shot | 87.5 | 89.4 | **90.8** |
| MMLU-Pro (EM) | 5-shot | 65.5 | 68.3 | **73.5** |
| MMMLU (EM) | 5-shot | 87.9 | 88.8 | **90.3** |
| C-Eval (EM) | 5-shot | 90.4 | 92.1 | **93.1** |
| CMMLU (EM) | 5-shot | 88.9 | 90.4 | **90.8** |
| MultiLoKo (EM) | 5-shot | 38.7 | 42.2 | **51.1** |
| Simple-QA vérifié (EM) | 25-shot | 28.3 | 30.1 | **55.2** |
| SuperGPQA (EM) | 5-shot | 45.0 | 46.5 | **53.9** |
| FACTS Parametric (EM) | 25-shot | 27.1 | 33.9 | **62.6** |
| TriviaQA (EM) | 5-shot | 83.3 | 82.8 | **85.6** |
| **Langage et raisonnement** | | | | |
| BBH (EM) | 3-shot | **87.6** | 86.9 | 87.5 |
| DROP (F1) | 1-shot | 88.2 | 88.6 | **88.7** |
| HellaSwag (EM) | 0-shot | 86.4 | 85.7 | **88.0** |
| WinoGrande (EM) | 0-shot | 78.9 | 79.5 | **81.5** |
| CLUEWSC (EM) | 5-shot | 83.5 | 82.2 | **85.2** |
| **Code et mathématiques** | | | | |
| BigCodeBench (Pass@1) | 3-shot | **63.9** | 56.8 | 59.2 |
| HumanEval (Pass@1) | 0-shot | 62.8 | 69.5 | **76.8** |
| GSM8K (EM) | 8-shot | 91.1 | 90.8 | **92.6** |
| MATH (EM) | 4-shot | 60.5 | 57.4 | **64.5** |
| MGSM (EM) | 8-shot | 81.3 | **85.7** | 84.4 |
| CMath (EM) | 3-shot | 92.6 | **93.6** | 90.9 |
| **Long contexte** | | | | |
| LongBench-V2 (EM) | 1-shot | 40.2 | 44.7 | **51.5** |

</div>

### Modèle Instruct

DeepSeek-V4-Pro et DeepSeek-V4-Flash prennent tous deux en charge trois modes d’effort de raisonnement :

| Mode de raisonnement | Caractéristiques | Cas d’usage typiques | Format de réponse |
| :--- | :--- | :--- | :--- |
| Non-think | Réponses rapides et intuitives | Tâches quotidiennes courantes, décisions à faible risque | Résumé `</think>` |
| Think High | Analyse logique consciente, plus lente mais plus précise | Résolution de problèmes complexes, planification | Pensée `<think>` `</think>` résumé |
| Think Max | Pousser le raisonnement à son maximum | Explorer les limites des capacités de raisonnement du modèle | Prompt système spécial + pensée `<think>` `</think>` résumé |

#### DeepSeek-V4-Pro-Max vs modèles frontier

<div align="center">

| Benchmark (métrique) | Opus-4.6 Max | GPT-5.4 xHigh | Gemini-3.1-Pro High | K2.6 Thinking | GLM-5.1 Thinking | DS-V4-Pro Max |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Connaissance et raisonnement** | | | | | | |
| MMLU-Pro (EM) | 89.1 | 87.5 | **91.0** | 87.1 | 86.0 | 87.5 |
| SimpleQA-Verified (Pass@1) | 46.2 | 45.3 | **75.6** | 36.9 | 38.1 | 57.9 |
| Chinese-SimpleQA (Pass@1) | 76.4 | 76.8 | **85.9** | 75.9 | 75.0 | 84.4 |
| GPQA Diamond (Pass@1) | 91.3 | 93.0 | **94.3** | 90.5 | 86.2 | 90.1 |
| HLE (Pass@1) | 40.0 | 39.8 | **44.4** | 36.4 | 34.7 | 37.7 |
| LiveCodeBench (Pass@1) | 88.8 | - | 91.7 | 89.6 | - | **93.5** |
| Codeforces (Rating) | - | 3168 | 3052 | - | - | **3206** |
| HMMT 2026 Feb (Pass@1) | 96.2 | **97.7** | 94.7 | 92.7 | 89.4 | 95.2 |
| IMOAnswerBench (Pass@1) | 75.3 | **91.4** | 81.0 | 86.0 | 83.8 | 89.8 |
| Apex (Pass@1) | 34.5 | 54.1 | **60.9** | 24.0 | 11.5 | 38.3 |
| Apex Shortlist (Pass@1) | 85.9 | 78.1 | 89.1 | 75.5 | 72.4 | **90.2** |
| **Long contexte** | | | | | | |
| MRCR 1M (MMR) | **92.9** | - | 76.3 | - | - | 83.5 |
| CorpusQA 1M (ACC) | **71.7** | - | 53.8 | - | - | 62.0 |
| **Agentique** | | | | | | |
| Terminal Bench 2.0 (Acc) | 65.4 | **75.1** | 68.5 | 66.7 | 63.5 | 67.9 |
| SWE Verified (Resolved) | **80.8** | - | 80.6 | 80.2 | - | 80.6 |
| SWE Pro (Resolved) | 57.3 | 57.7 | 54.2 | **58.6** | 58.4 | 55.4 |
| SWE Multilingual (Resolved) | **77.5** | - | - | 76.7 | 73.3 | 76.2 |
| BrowseComp (Pass@1) | 83.7 | 82.7 | **85.9** | 83.2 | 79.3 | 83.4 |
| HLE avec outils (Pass@1) | 53.1 | 52.0 | 51.6 | **54.0** | 50.4 | 48.2 |
| GDPval-AA (Elo) | 1619 | **1674** | 1314 | 1482 | 1535 | 1554 |
| MCPAtlas Public (Pass@1) | **73.8** | 67.2 | 69.2 | 66.6 | 71.8 | 73.6 |
| Toolathlon (Pass@1) | 47.2 | **54.6** | 48.8 | 50.0 | 40.7 | 51.8 |

</div>

#### Comparaison entre modes

<div align="center">

| Benchmark (métrique) | V4-Flash Non-Think | V4-Flash High | V4-Flash Max | V4-Pro Non-Think | V4-Pro High | V4-Pro Max |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Connaissance et raisonnement** | | | | | | |
| MMLU-Pro (EM) | 83.0 | 86.4 | 86.2 | 82.9 | 87.1 | **87.5** |
| SimpleQA-Verified (Pass@1) | 23.1 | 28.9 | 34.1 | 45.0 | 46.2 | **57.9** |
| Chinese-SimpleQA (Pass@1) | 71.5 | 73.2 | 78.9 | 75.8 | 77.7 | **84.4** |
| GPQA Diamond (Pass@1) | 71.2 | 87.4 | 88.1 | 72.9 | 89.1 | **90.1** |
| HLE (Pass@1) | 8.1 | 29.4 | 34.8 | 7.7 | 34.5 | **37.7** |
| LiveCodeBench (Pass@1) | 55.2 | 88.4 | 91.6 | 56.8 | 89.8 | **93.5** |
| Codeforces (Rating) | - | 2816 | 3052 | - | 2919 | **3206** |
| HMMT 2026 Feb (Pass@1) | 40.8 | 91.9 | 94.8 | 31.7 | 94.0 | **95.2** |
| IMOAnswerBench (Pass@1) | 41.9 | 85.1 | 88.4 | 35.3 | 88.0 | **89.8** |
| Apex (Pass@1) | 1.0 | 19.1 | 33.0 | 0.4 | 27.4 | **38.3** |
| Apex Shortlist (Pass@1) | 9.3 | 72.1 | 85.7 | 9.2 | 85.5 | **90.2** |
| **Long contexte** | | | | | | |
| MRCR 1M (MMR) | 37.5 | 76.9 | 78.7 | 44.7 | 83.3 | **83.5** |
| CorpusQA 1M (ACC) | 15.5 | 59.3 | 60.5 | 35.6 | 56.5 | **62.0** |
| **Agentique** | | | | | | |
| Terminal Bench 2.0 (Acc) | 49.1 | 56.6 | 56.9 | 59.1 | 63.3 | **67.9** |
| SWE Verified (Resolved) | 73.7 | 78.6 | 79.0 | 73.6 | 79.4 | **80.6** |
| SWE Pro (Resolved) | 49.1 | 52.3 | 52.6 | 52.1 | 54.4 | **55.4** |
| SWE Multilingual (Resolved) | 69.7 | 70.2 | 73.3 | 69.8 | 74.1 | **76.2** |
| BrowseComp (Pass@1) | - | 53.5 | 73.2 | - | 80.4 | **83.4** |
| HLE avec outils (Pass@1) | - | 40.3 | 45.1 | - | 44.7 | **48.2** |
| MCPAtlas (Pass@1) | 64.0 | 67.4 | 69.0 | 69.4 | **74.2** | 73.6 |
| GDPval-AA (Elo) | - | - | 1395 | - | - | **1554** |
| Toolathlon (Pass@1) | 40.7 | 43.5 | 47.8 | 46.3 | 49.0 | **51.8** |

</div>

## Modèle de chat

Cette version ne comprend pas de modèle de chat au format Jinja. À la place, nous fournissons un dossier dédié `encoding` contenant des scripts Python et des cas de test démontrant comment encoder des messages au format compatible OpenAI en chaînes d’entrée pour le modèle, et comment analyser la sortie texte du modèle. Veuillez vous référer au dossier [`encoding`](encoding/README.md) pour la documentation complète.

Un exemple rapide :

```python
from encoding_dsv4 import encode_messages, parse_message_from_completion_text

messages = [
    {"role": "user", "content": "hello"},
    {"role": "assistant", "content": "Hello! I am DeepSeek.", "reasoning_content": "thinking..."},
    {"role": "user", "content": "1+1=?"}
]

# messages -> string
prompt = encode_messages(messages, thinking_mode="thinking")

# string -> tokens
import transformers
tokenizer = transformers.AutoTokenizer.from_pretrained("deepseek-ai/DeepSeek-V4-Pro")
tokens = tokenizer.encode(prompt)
```

## Comment exécuter en local

Veuillez consulter le dossier [inference](inference/README.md) pour des instructions détaillées sur l’exécution locale de DeepSeek-V4, y compris la conversion des poids du modèle et les démonstrations de chat interactif.

Pour le déploiement local, nous recommandons de régler les paramètres d’échantillonnage sur `temperature = 1.0, top_p = 1.0`. Pour le mode de raisonnement Think Max, nous recommandons une fenêtre de contexte d’au moins **384K** tokens.

## Licence

Ce dépôt et les poids du modèle sont placés sous licence [MIT](LICENSE).

## Citation

```
@misc{deepseekai2026deepseekv4,
      title={DeepSeek-V4: Towards Highly Efficient Million-Token Context Intelligence},
      author={DeepSeek-AI},
      year={2026},
}
```

## Contact

Si vous avez des questions, veuillez ouvrir une issue ou nous contacter à l’adresse [service@deepseek.com](service@deepseek.com).
