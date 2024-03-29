# 方法简介
1. LLM
    1. direct系列：直接将问题输入LLM
    另一种写法是在问题后面加`The answer is`
    GPT-3.5-Turbo&emsp;&emsp;ChatGLM3-6B&emsp;&emsp;GLM-4
    2. CoT系列：在问题后面直接加` Let's think step by step.`
    另一种写法是：`Q: [Q]. A: Let’s think step by step`
    GPT-3.5-Turbo CoT
    3. PRP系列：算是CoT的一种延伸，通过重复多次CoT→验证答案→带着错误答案CoT的过程来实现预测
    GPT-3.5-Turbo PRP
    4. 微调系列：
        1. GPT-2 finetune
        GPT-2英文版/原版我用的是：https://huggingface.co/openai-community/gpt2
    5. verifier：通过generator生成答案，再用verifier验证答案
        1. GPT-2 verifier
        

# 运行命令

GPT-3.5-Turbo + Alg514：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn Alg514 -ds datasets/Alg514 -pt pure -rt codes/results/ChatGPT-3.5_Alg_result.txt`

GPT-3.5-Turbo + AI2：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn AI2 -ds datasets/AI2 -pt pure -rt codes/results/ChatGPT-3.5_AI2_result.txt`（约4分钟）

GPT-3.5-Turbo + dolphin1878: `python codes/zero_shot_infer.py -mc GPT-3.5 -dn dolphin1878 -ds datasets/dolphin1878 -pt pure -rt codes/results/ChatGPT-3.5_dolphin1878_result.txt`（约9分钟）

GPT-3.5-Turbo + Math23K：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn Math23K -ds datasets/math23k -pt pure -rt codes/results/ChatGPT-3.5_Math23K_result.txt`（约1小时32分钟）

GPT-3.5-Turbo + ASDiv：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn ASDiv -ds datasets/asdiv -pt pure -rt codes/results/ChatGPT-3.5_ASDiv_result.txt`（约28分钟）

GPT-3.5-Turbo + Ape210K：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn Ape210K -ds datasets/ape210k -pt pure -rt codes/results/ChatGPT-3.5_Ape210K_result.txt`（约7小时42分钟）

GPT-3.5-Turbo + GSM8K：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn GSM8K -ds datasets/gsm8k -pt pure -rt codes/results/ChatGPT-3.5_GSM8K_result.txt`（约2小时）

GPT-3.5-Turbo + SVAMP：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn SVAMP -ds datasets/svamp -pt pure -rt codes/results/ChatGPT-3.5_SVAMP_result.txt`（约20分钟）

GPT-3.5-Turbo CoT + Alg514：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn Alg514 -ds datasets/Alg514 -pt CoT -rt codes/results/ChatGPT-3.5_COT_Alg_result.txt`

GPT-3.5-Turbo CoT+tip + Alg514：`python codes/zero_shot_infer.py -mc GPT-3.5 -dn Alg514 -ds datasets/Alg514 -pt CoT+tip -rt codes/results/ChatGPT-3.5_COT+tip_Alg_result.txt`

GPT-3.5_PRP + Alg514: `python codes/PRP.py -mc GPT-3.5 -dn Alg514 -ds datasets/Alg514 -rt codes/results/ChatGPT_PRP_Alg_result.txt`（约10分钟）

ChatGLM3-6B + Alg514：`CUDA_VISIBLE_DEVICES=4 python codes/zero_shot_infer.py -mc /data/pretrained_models/chatglm3-6b -mn ChatGLM3 -dn Alg514 -ds datasets/Alg514 -rt codes/results/ChatGLM3_Alg_result.txt`

GLM-4 + Alg514：`python codes/zero_shot_infer.py -mc GLM-4 -dn Alg514 -ds datasets/Alg514 -pt pure -rt codes/results/GLM4_Alg_result.txt`（约2.1元 + 6分钟）

（由于网络问题未成功运行）llama2-70b-4096 + Alg514：`python codes/zero_shot_infer.py -mc llama2-70b-4096 -dn Alg514 -ds datasets/Alg514 -pt pure -rt codes/results/llama2-70b-4096_Alg_result.txt`

GPT + Alg514：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/test.py -dn Alg514 -ds datasets/Alg514 -cp openai-community/gpt2 -rt codes/results/gpt2_direct_Alg_result.txt`（约2分钟）

GPT-2 finetune + Alg514：
训练：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/finetune.py -dn Alg514 -ds datasets/Alg514 -cp my_checkpoints/gpt2_alg514`（约39秒）
测试：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/test.py -dn Alg514 -ds datasets/Alg514 -cp my_checkpoints/gpt2_alg514 -rt codes/results/gpt2_Alg_result.txt`（约1分钟）

GPT-2 finetune + AI2：（之所以采用不同的写法是为了练习代码能力）
训练：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/finetune_w_Trainer.py -dn AI2 -ds datasets/AI2 -cp my_checkpoints/gpt2_AI2`（约39秒）
测试：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/test.py -dn AI2 -ds datasets/AI2 -cp my_checkpoints/gpt2_AI2 -rt codes/results/gpt2_AI2_result.txt`

GPT-2 finetune + GSM8K：
训练：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/finetune.py -dn GSM8K -ds datasets/gsm8k -cp my_checkpoints/gpt2_gsm8k`（约1小时13分钟）
测试（未使用calculator）：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/test.py -dn GSM8K -ds datasets/gsm8k -cp my_checkpoints/gpt2_gsm8k -rt codes/results/gpt2_GSM8K_result.txt`（约21分钟）
测试（使用calculator）：`CUDA_VISIBLE_DEVICES=1 python codes/finetune/gpt2/test_w_calculator.py -dn GSM8K -ds datasets/gsm8k -cp my_checkpoints/gpt2_gsm8k -rt codes/results/gpt2_GSM8K_w_calculator_result.txt`（约28分钟）

GPT-2 verifier + GSM8K：
第一阶段-训练generator：直接用了上面的GPT-2 finetune + GSM8K的checkpoint（因为我把之前的checkpoint删了，所以其实是重跑了一遍，得到了不同的checkpoint。但是这个不重要）
第二阶段-获取用于训练verifier的数据集：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/verifier2_generate_verifier_train_data.py -dn GSM8K -ds datasets/gsm8k -cp my_checkpoints/gpt2_gsm8k -rt codes/finetune/gpt2/mid_result/gpt2_GSM8K_verifier_train_data.jsonl`（因为出现了OverflowError问题（已debug）所以没跑完，只跑了2%……就姑且先用这么多数据凑合一下吧，毕竟我没写mini-batch代码，运行太慢了）
第三阶段-训练verifier：`CUDA_VISIBLE_DEVICES=0 python codes/finetune/gpt2/verifier3_train_verifier.py -dp codes/finetune/gpt2/mid_result/gpt2_GSM8K_verifier_train_data.jsonl -ip my_checkpoints/gpt2_gsm8k -sp my_checkpoints/gpt2verifier_gsm8k`