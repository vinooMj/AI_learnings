ust Quantized Qwen2.5-VL 3B from 6GB to 1.8GB using llama.cpp and the results are impressive! 

Sharing my personal experience 

In a recent project, I needed to extract text from images using free and open-source tools. I started with traditional OCR libraries like Tesseract and EasyOCR, but they struggled with curved or artistic text.

After some digging, I discovered Qwen2.5-VL 3B, a powerful open-source multimodal model that handles both vision and language. It was a great fit but the model size (~6GB) made local usage slow and memory-intensive.

Entering into LLM Quantization⚡️

▪️To overcome this, I explored LLM quantization a process that reduces model size and memory usage by converting weights to lower precision (like 2-bit, 3-bit, or 4-bit) with minimal performance drop.
▪️Using llama.cpp, I successfully quantized the Qwen2.5-3B model down to just 1.8GB, and it runs super smoothly on my machine! 

Note on Multimodals ⚠️
▪️Currently, llama.cpp doesn’t fully support multimodal models (like vision + language) support is still in development. So for now, it works best with text-only LLMs.

💡 Why Quantization Matters
⚡ Faster performance
💾 Lower memory footprint
💻 Runs on local and edge devices
🌍 Makes powerful AI models more accessible
