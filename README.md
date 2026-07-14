# Neural Sound Synthesis · Part 9 — Neural Audio Codecs

The ninth part of the [Neural Sound Synthesis](https://github.com/BrendanJamesLynskey/Neural_Sound_Synthesis) series. A neural audio codec is an autoencoder with a *discrete* bottleneck: it compresses audio to a few kilobits per second **and** turns a waveform into a sequence of integer tokens a language model can read. This part builds the machinery from vector quantization up through residual VQ, SoundStream / EnCodec, and DAC — the hinge between signal (Parts 1–8) and language (Part 10).

### [Launch App](https://brendanjameslynskey.github.io/Neural_Sound_Synthesis_09_Neural_Audio_Codecs/)

Part of the [DSP & Music](https://github.com/BrendanJamesLynskey/DSP_and_Music) collection.

---

## What's inside

| Section | Content |
|---------|---------|
| **The Bottleneck** | Why a discrete latent buys compression *and* tokenization in one architecture |
| **Vector Quantization** | VQ-VAE: nearest-codebook lookup, the straight-through estimator, codebook + commitment losses (β), EMA updates, codebook collapse |
| **Residual VQ** | A stack of codebooks quantizing successive residuals — with the **flagship RVQ visualiser** showing residuals collapse stage by stage |
| **SoundStream & EnCodec** | Streaming conv encoder/decoder, multi-scale STFT + adversarial + commitment losses, quantizer dropout, entropy coding — with an **interactive architecture diagram** |
| **Bitrate & Quality** | `bits/s = f_r × N_q × log₂K`, with a **hearable SNR-vs-bitrate demo** driven by residual quantization |
| **DAC** | Descript Audio Codec: factorized L2-normalized codes, snake activations, near-100% codebook usage |
| **Tokens → Language** | Why discretization unlocks Part 10's language models; contrast with classical MDCT codecs (Opus/MP3) |
| **Timeline** | VQ-VAE (2017) → SoundStream → EnCodec → DAC (2023) |

## Live demos (all synthesised in-browser, no audio files)

1. **RVQ visualiser** (flagship) — an input vector reached by a chain of chosen codewords, one per stage; watch the residual magnitude collapse and the reconstruction converge as you change `N_q` and codebook size `K`, with the live bitrate readout.
2. **Bitrate vs quality** — a residual quantizer over a synthesised clip; add stages to climb the SNR-vs-bitrate curve and A/B the original against the quantized reconstruction to *hear* quality rise with bitrate.
3. **Codec architecture diagram** — hover (or click) the pipeline: raw audio → conv encoder → RVQ tokens → conv decoder → audio, plus the reconstruction / adversarial / commitment losses that train it. The RVQ tokens are exactly what Part 10's language models consume.

## Technology

Single-file HTML/CSS/JS · Web Audio API · HTML5 Canvas · KaTeX · Palatino + Lucida Console · No external dependencies · No build step
