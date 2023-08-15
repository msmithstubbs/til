# Using llama.cpp and Llama2 with GPU on M1

[llama.cpp](https://github.com/ggerganov/llama.cpp) can run large language models such as Llama2 locally on a Mac using the M1 or M2 CPU. But it can also be built to make use of the GPU. GPUs are very good at the kind of calculations LLMs require so this is much faster.

Replicate.com has a blog post (https://replicate.com/blog/run-llama-locally) on how to do this but it misses a key step when running it: you need to include `-ngl 1` to tell llama.cpp to use the GPU.

Here's the script from their blog post. The last line adds this flag.

```bash
#!/bin/bash

# Clone llama.cpp
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp

# Build it. `LLAMA_METAL=1` allows the computation to be executed on the GPU
LLAMA_METAL=1 make

# Download model
export MODEL=llama-2-13b-chat.ggmlv3.q4_0.bin
if [ ! -f models/${MODEL} ]; then
    curl -L "https://huggingface.co/TheBloke/Llama-2-13B-chat-GGML/resolve/main/${MODEL}" -o models/${MODEL}
fi

# Set prompt
PROMPT="Hello! How are you?"

# Run in interactive mode
./main -m ./models/llama-2-13b-chat.ggmlv3.q4_0.bin \
  --color \
  --ctx_size 2048 \
  -n -1 \
  -ins -b 256 \
  --top_k 10000 \
  --temp 0.2 \
  --repeat_penalty 1.1 \
  -t 8
  -ngl 1

```

There is a [readme](https://github.com/ggerganov/llama.cpp/blob/3ebb00935f3f0522b75df49c2769ab1774b91380/examples/main/README.md) for `main` with information on the available options. Here’s what each used above does:

* `--color` uses coloured text to differentiates the user input and the AI responses.
* `--ctx_size 2048` set the prompt context size to the maximum available for LLama2 of 2048 tokens
* `-n -1`  sets the number of tokens to predict to infinity
* `-ins` run in instruction mode. Without this you need to pass a prompt (if you don’t a random prompt is used)
* `-b 256` batch size for prompt processing.
* `--top_k 10000` Limits next token to the most probable tokens. A higher number here will give more diverse output, but it could make less sense.
* `--temp 0.2` sets the randomness level. A higher number will produce less predictable results, but could be more interesting.
* `--repeat_penalty 1.1` helps reduce repetitive output by assigning a penalty to repeating the same text
* `-t 8` sets the number of threads to use. Best set to the number of physical cores. Not sure if you would use a higher number here if the GPU has more cores, or the CPU cores are the limiting factor.
* `-ngl 1` offloads some layers to the GPU. Use this to enable GPU usage on the Mac M1/M2
