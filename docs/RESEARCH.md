# aiOS Research

## On-Device LLM Landscape

### Models That Fit Mobile

| Model | Size | RAM Needed | Notes |
|-------|------|------------|-------|
| Llama 3.2 1B | ~700MB | 2GB | Meta's smallest, good quality |
| Llama 3.2 3B | ~2GB | 4GB | Better quality, still mobile-viable |
| Phi-3-mini (3.8B) | ~2.5GB | 4GB | Microsoft, strong reasoning |
| Gemma 2 2B | ~1.5GB | 3GB | Google, Apache licensed |
| Qwen2.5-1.5B | ~1GB | 2GB | Alibaba, multilingual |
| SmolLM 1.7B | ~1.2GB | 2.5GB | HuggingFace, efficient |

### Inference Frameworks

| Framework | Platform | Notes |
|-----------|----------|-------|
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | Cross-platform | Best quantization, C++ |
| [MLC-LLM](https://github.com/mlc-ai/mlc-llm) | Android/iOS | Apache TVM backend |
| [executorch](https://github.com/pytorch/executorch) | Mobile | Meta, PyTorch native |
| [MediaPipe LLM](https://developers.google.com/mediapipe) | Android/iOS | Google, integrated |

### Quantization

- **GGUF**: Most common, llama.cpp native
- **Q4_K_M**: Good balance of size/quality
- **Q8_0**: Higher quality, 2x size
- **AWQ/GPTQ**: GPU-optimized alternatives

---

## Base OS Options

### Option A: Fork AOSP

**Pros:**
- Largest existing ecosystem
- Hardware support (drivers)
- Familiar development model
- Can potentially run Android apps in sandbox

**Cons:**
- Google's shadow (even without GMS)
- Massive codebase
- Not truly "clean slate"

**Examples:** GrapheneOS, CalyxOS, /e/OS, LineageOS

### Option B: Linux-Based (postmarketOS/Mobian)

**Pros:**
- True Linux, familiar tools
- Smaller, auditable codebase
- Desktop app potential (Phosh, Plasma Mobile)
- No Android baggage

**Cons:**
- Limited device support
- No Android app compatibility
- Less mature mobile UX patterns

**Examples:** postmarketOS, Mobian, Ubuntu Touch

### Option C: Custom Launcher on Android

**Pros:**
- Fastest to prototype
- Full hardware support
- Can still use Play Store if needed
- Lower risk

**Cons:**
- Not true OS control
- Google still underneath
- Limited system integration

**Examples:** Niagara Launcher, Ratio, etc.

### Recommendation

Start with **Option C** (custom launcher) for rapid prototyping, then evaluate **Option A** (AOSP fork) for production. Skip Linux-based for now — hardware support too limited.

---

## Banking App Problem

### Why Banking Apps Need Google

Most banking apps require:
1. **SafetyNet/Play Integrity** — Google's device verification
2. **Google Play Services** — Push notifications, location, etc.
3. **Proprietary DRM** — Widevine for secure video

### Workarounds

| Approach | Viability |
|----------|-----------|
| MicroG (open GMS replacement) | Works for some apps, not banking |
| Web banking | Most banks have decent web apps |
| PWA banking apps | Emerging, not universal |
| EU regulation (DMA) | May force alternatives |

### Strategy

1. Accept banking via web browser initially
2. Advocate for PWA banking adoption
3. Long-term: push for open attestation standards

---

## Camera AI Enhancement

### Current State of Art

| Project | Approach |
|---------|----------|
| Google Camera (GCam) | ML-based HDR+, Night Sight |
| Apple Computational | Photonic Engine, Deep Fusion |
| OpenCamera | Open source, basic ML |

### What We Can Do

1. **Real-time enhancement** with on-device models
2. **Generative fill** for low-light compensation
3. **Upscaling** (Real-ESRGAN variants)
4. **Portrait mode** without depth sensor (SAM/ControlNet)

### Models to Explore

- Real-ESRGAN (upscaling)
- Segment Anything Mobile (SAM)
- ControlNet (composition)
- LCM/SDXL-Turbo (fast generation)

### Challenges

- Inference speed (needs <100ms for viewfinder)
- Power consumption
- Heat management
- Storage for models

---

## Web3 Integration

### Wallet

- Built-in, non-custodial
- Supports EVM chains + Solana
- Hardware key backup (USB-C security key)
- Social recovery option

### Identity (ERC-8004)

- Agent identity on-chain
- Reputation portable across apps
- No KYC required for basic identity

### Payments (x402)

- Micropayments for premium features
- Pay-per-use vs subscription
- Fiat on/off-ramp integration

### Messaging

- Matrix protocol (federated, E2E encrypted)
- Bridges to Signal, Telegram, WhatsApp
- AI agent can manage all channels

---

## Target Hardware (Phase 1)

| Device | Why |
|--------|-----|
| **Google Pixel 7/8** | Best custom ROM support, NPU |
| **Fairphone 4/5** | Unlockable, ethical positioning |
| **OnePlus 12** | Bootloader unlockable, powerful |
| **Nothing Phone 2** | Developer-friendly, unique positioning |

**Not initially targeting:**
- Samsung (Knox makes it hard)
- Xiaomi (MIUI complications)
- PinePhone (too underpowered for on-device LLM)

---

## Competitive Landscape

| Product | Positioning | Threat Level |
|---------|-------------|--------------|
| Rabbit R1 | AI-first hardware | Medium (hardware-bound) |
| Humane AI Pin | Voice-first wearable | Low (niche form factor) |
| Siri/Google Assistant | Incumbent AI | High (integration) |
| Open Interpreter | AI agent on desktop | Low (not mobile) |

### Differentiation

We're not building:
- Another voice assistant (Siri clone)
- Separate hardware (Rabbit R1)
- A launcher skin (Niagara)

We're building:
- **Full OS where AI is the shell**
- On existing phone hardware
- Privacy-first, Web3-native
- Agent that can truly act autonomously
