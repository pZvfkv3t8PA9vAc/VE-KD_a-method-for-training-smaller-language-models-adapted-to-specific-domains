# VE-KD:a-method-for-training-smaller-language-models-adapted-to-specific-domains

This repository contains the model and evaluation dataset of our paper.
We use the same scripts from [LinkBERT](https://github.com/michiyasunaga/LinkBERT).
for fine-tuning model, please get the LinkBERT/src/{seqcls,tokcls}.

## Fine-tune VE-KD
To fine-tune for the BLURB biomedial datasets, using command as follows:
```
mkdir runs 
export MODEL_PATH=VE_KD_model 
export data=evaluation_data
export src=[path of LinkBERT/src] 
```

### QA: PubMedQA  
```
export task=pubmedqa_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 16 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 2e-5 --warmup_steps 100 --num_train_epochs 30 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir  
```

### QA: BioASQ  
```
export task=bioasq_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 16 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 2e-5 --warmup_steps 100 --num_train_epochs 20 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir  
``` 

### HoC 
```
export task=HoC_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict --metric_name hoc \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 4e-5 --num_train_epochs 40 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### RE: ChemProt  
```
export task=chemprot_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict --metric_name PRF1 \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 3e-5 --num_train_epochs 10 --max_seq_length 256 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### RE: DDI  
```
export task=DDI_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict --metric_name PRF1 \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 2e-5 --num_train_epochs 5 --max_seq_length 256 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### RE: GAD  
```
export task=GAD_hf
export datadir=$data/seqcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/seqcls/run_seqcls.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict --metric_name PRF1 \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 3e-5 --num_train_epochs 10 --max_seq_length 256 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### EBM PICO  
```
export task=ebmnlp_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict --return_macro_metrics \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 5e-5 --num_train_epochs 1 --max_seq_length 512  \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### NER: JNLPBA  
```
export task=JNLPBA_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 16 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 1e-5 --warmup_ratio 0.1 --num_train_epochs 5 --max_seq_length 512  \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### NER: NCBI-disease  
```
export task=NCBI-disease_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 5e-5 --warmup_ratio 0.1 --num_train_epochs 20 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### NER: BC2GM 
```
export task=BC2GM_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 6e-5 --warmup_ratio 0.1 --num_train_epochs 50 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### NER: BC5CDR-disease 
```
export task=BC5CDR-disease_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 16 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 5e-5 --warmup_ratio 0.1 --num_train_epochs 8 --max_seq_length 512 \
--save_strategy no --evaluation_strategy no --output_dir $outdir   
```

### NER: BC5CDR-chem  
```
export task=BC5CDR-chem_hf
export datadir=$data/tokcls/$task
export outdir=runs/$task/$MODEL
mkdir -p $outdir
python3 -u $src/tokcls/run_ner.py --model_name_or_path $MODEL_PATH \
--train_file $datadir/train.json --validation_file $datadir/dev.json --test_file $datadir/test.json \
--do_train --do_eval --do_predict \
--per_device_train_batch_size 32 --gradient_accumulation_steps 1 --fp16 \
--learning_rate 5e-5 --warmup_ratio 0.1 --num_train_epochs 20 --max_seq_length 512 \
--overwrite_cache \
--save_strategy no --evaluation_strategy no --output_dir $outdir --overwrite_output_dir 
```
