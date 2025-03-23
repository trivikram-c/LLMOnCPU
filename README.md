# LLMOnCPU
Study of deploying LLMs on CPUs. We recommand run the notebook file in Colab.
To run the script, please follow the following steps:
## 1. Install packages
   run these commands in a virtual environment:
   ```
   pip install -U "huggingface_hub[cli]"
   pip install llama-cpp-python
   pip install psutil
   pip install tqdm
   pip install datasets
   pip install torch
   pip install transformers
   ```
## 2. Log in to huggingface
   After installing all the packages, run the following command:
   `huggingface-cli login`
## 3. Run the script
   `python gsm8k_test.py [-h] [--model MODEL] [--device DEVICE] [--quantization_scheme QUANTIZATION_SCHEME]
                     [--prompt PROMPT] [--limit LIMIT] [--latency_measure LATENCY_MEASURE] [--verbose VERBOSE]
                     [--do_memory_profiling DO_MEMORY_PROFILING] [--memory_constrain MEMORY_CONSTRAIN] `

  ### options:
    -h, --help            show this help message and exit
    --model MODEL         select the model. (default) 0 = Llama-3.2-1B-Instruct, 1 = Llama-3.2-3B-Instruct, 2 =
                          DeepSeek-R1-Distill-Qwen-1.5B
    --device DEVICE       select the device (cpu or gpu)
    --quantization_scheme QUANTIZATION_SCHEME
                          select the quantization scheme. (default) -1 = no quantization, 8 = Q8_0 quantization
    --prompt PROMPT       select the quantization scheme. 0 = zero-shot Cot, (default) 1 = one-shot Cot, 8 = 8-shot Cot
    --limit LIMIT         a float number between 0 and 1, indicating the percentage of the dataset to be used, or an
                          integer that indicates how many samples to use. Default is 1.0.
    --latency_measure LATENCY_MEASURE
                          an integer, 0 means to measure the TTFT of the model, (default) 1 means to measure the total   generation
                          time of the model
    --verbose VERBOSE     a boolean, whether to print the accuracy, total output token count, total generation time, and
                          TTFT. Default is True
    --do_memory_profiling DO_MEMORY_PROFILING
                          a boolean, whether to do memory profiling of the model the result is valid only when
                          quantization=False and device=cpu the memory footprint is obtained by sending one sample to
                          the model and recording the memory footprint during the inference. Not implemented when using
                          llama_cpp to do the inference. Default is False.
    --memory_constrain MEMORY_CONSTRAIN
                          the memory constrain applied on the process in GB. If -1, no constrain is applied. Only valid
                          in linux platform. Default is -1.
   
## 4. Check the results
   When the run finishes, the results will be written into a json file. You can use ece226_plot.ipynb to see the results. Please modify the path and filename accordingly. 
   In the results folder are the results of our experiments. The 12 files in the outer folder are all under hardware config 2, and the files in the inner folder are from config 3,4,5 based on their names: \_20\_ means config 3, \_16\_ means config 4, and \_6C12T\_ means config 5.
