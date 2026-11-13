# Architecture Document Classifier

The code companion to the master's thesis **"Automated Classifying Software Architecture Documentation in Open Source Projects"** by **Abel Haile Magicho**.

## What this is

Research in software engineering constantly needs documents that describe a system's software architecture — its components, connectors, and design decisions. In open source projects those documents are buried among thousands of other files: requirements documents, API references, Javadoc and Doxygen output, tutorials, and specifications. Finding the architecture documents by hand is slow and does not scale.

This project implements the classifier designed in the thesis: given a document, it decides whether the document is a **software architecture document** or not — including the hard cases, the *close negatives* that talk about code without describing architecture.

## Files in this repository

| File | What it is |
|---|---|
| `architecture-document-classifier.html` | The classifier itself — a complete working app in a single HTML file. Open it in any browser; no installation, no server, no dependencies. |
| `automated-classification-software-architecture-documentation-thesis-full-advanced.pdf` | The full advanced thesis (45 pages): problem, literature review, research questions and hypotheses, the classifier design, the evaluation protocol, formal foundations, and advanced contributions. |
| `architecture-document-classifier-code.pdf` | The full source code of the classifier as a printable document (45 pages). |
| `classifier-code-with-layman-comments.pdf` | The code explained section by section in plain words. |

## How the classifier works

Following the design in the thesis, the app combines several strands of evidence instead of trusting any single signal:

- **Text strand** — the document text is processed with tokenising, TF-IDF weighting, and an inverted index; architecture vocabulary (components, connectors, deployment, views, decisions, rationale) scores against vocabulary typical of the close negatives.
- **Diagram strand** — architecture documents usually carry class or UML-style diagrams; the presence and kind of diagrams is treated as evidence, testing the thesis hypothesis that a class diagram may be enough to mark a document as architectural.
- **Structure and metadata strand** — headings, document structure, and metadata signals are combined with the text evidence into one decision with a confidence indication, so borderline documents can be routed to human review instead of being silently mislabelled.

The app ships with built-in demo documents — including an API reference as a close negative — and shows the classifier's verdict against the intended label for each one, so the pipeline can be exercised end to end in the browser.

## Honest status

The thesis is a **research proposal and design**: the classifier design, the labelling guide, and the full evaluation protocol (precision, recall, F1, cross-validation, ablation) are specified in the thesis, and the large labelled sample of 50–100 real project documents described there has **not** been collected yet. The HTML app in this repository is a working demonstration implementation of the design, verified against its built-in demo documents — it is not a claim that the full thesis evaluation has been run. Figures quoted inside the thesis from other studies are those studies' own results, attributed as such.

## Running it

Download `architecture-document-classifier.html` and open it in a browser. Paste or load a document, and the classifier reports its verdict with the evidence strands that produced it.

## Author

Abel Haile Magicho — [github.com/kembAB](https://github.com/kembAB)
