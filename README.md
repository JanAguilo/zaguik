# Zaguik

Zaguik is a privacy-preserving attestation system for LLM outputs. It proves, in zero knowledge, that a certified PII filter was applied to a language model's response and returned a passing result, without revealing the response itself, the filter parameters, or any personal data it may have contained.

The system chains four stages: an LLM generates a response (DistilGPT-2 by default), a PII filter checks it (regex- or NER-based), a zk-SNARK proof is generated via [EzKL](https://github.com/zkonduit/ezkl) attesting that the filter circuit accepted the encoded output, and the proof is verified. A SHA-256 hash commitment binds each proof to a specific output at the protocol level, so a verifier can confirm the attestation without seeing the underlying text.

The motivation is regulatory: under GDPR and the EU AI Act, providers of AI systems handling personal data must be able to demonstrate that their safeguards actually work. Zaguik explores whether zero-knowledge proofs can provide that evidence to an external auditor without the auditor gaining access to the sensitive content the filter was meant to protect. The thesis accompanying this implementation evaluates proof size, generation time, and verification time across encoding lengths of 128-2048 bytes on commodity hardware, and discusses where this attestation primitive fits, and falls short, as a compliance tool.

## Repository structure

```
scripts/        # Python pipeline 
thesis/         # LaTeX source and compiled PDF of the bachelor's thesis
paper/          # Paper presented at JNIC 2026 conferences
```