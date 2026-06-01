
## 1. llmfit (Open-Source Rust CLI + TUI)
This is the prominent hardware-aware model lookup tool highlighted across several slides.
 * **Creator:** Alex Jones
 * **What it does:** It is an open-source Rust CLI and Terminal User Interface (TUI) that scans your local hardware (RAM, CPU cores, GPU VRAM via nvidia-smi, rocm-smi, or Apple Silicon unified memory). It checks an embedded database of nearly 500 models to instantly calculate fit, speed, quality, and context dimensions to determine what can actually run on your machine under a second.
 * **GitHub/Registry Details:**
   * The project can be run via the GitHub Container Registry using:
     docker run ghcr.io/alexsjones/llmfit
   * It is also available via Homebrew: brew install llmfit
   * The presentation notes that it has reached **21,000+ GitHub Stars**.
## 2. Docker Model Runner
This is Docker's official stable component for pulling, running, and serving LLMs locally like standard containers.
 * **What it does:** It acts as a local OCI registry container wrapper that auto-detects your GPU and uses backends like llama.cpp or vLLM to expose an OpenAI-compatible API on localhost:12434.
 * **Syntax Reference:**
   ```bash
   docker model pull ai/qwen3.5-coder
   docker model run ai/qwen3.5-coder
   
   ```
```
*   **GitHub Integration:** In the Architecture diagrams, the runner utilizes the `api.github.com` endpoint securely through proxies for policy checks, while blocking malicious exfiltration targets (like `bad.exfil.example`).

---

## 3. Docker Sandboxes (`sbx`)
A standalone CLI utility focused on isolating AI agent activity.

*   **What it does:** Provides strict microVM isolation instead of a shared kernel for running untrusted agent-generated code. It gives the agent its own disposable filesystem and network boundary so your host machine is safe from any destructive execution loops.
*   **Installation commands shown:**
    *   **macOS (Homebrew):** `brew install docker/tap/sbx`
    *   **Windows (Winget):** `winget install -h Docker.sbx`
    *   **Linux (Ubuntu/APT):** `sudo apt-get install docker-sbx`

---

## 4. Docker Compose + AI Integration
Docker has brought native LLM provisioning directly into the standard `docker-compose.yml` specification for 2026.

*   **What it does:** You can now define `models` as first-class primitives alongside services, volumes, and networks. Running `docker compose up` will automatically pull the specified model from the Hub, set up context boundaries, and inject the environment routing to your application services automatically.

```
