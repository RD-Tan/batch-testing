# Testing RiSPICE

This is assuming your machine is on Windows.

## Creating .venv
We need to create a virtual environment so that we don't pollute your global python packages. Just run the following:

```bash
python -m venv .venv
```

Then to enter the venv:

```bash
.venv\Scripts\activate
```

You should notice that your command line is now prepended with `(.venv)`

## Installing requirements

There are two provided bare requirements file, `cpu-only.txt` and `cuda-enabled.txt`. I provide `cpu-only.txt` as a just in case the GPU doesn't work out. To install the packages run:

```bash
pip install -r requirements\cuda-enabled.txt
```

This took forever on my end so I guess you can stand up and do something else.

## Cloning models

We need to grab the models from Hugging Face. To do so:

```
cd .models
git clone https://huggingface.co/paolomanlapaz/rispice-base
git clone https://huggingface.co/paolomanlapaz/rispice-1000bp
```

## Running pipeline

I kept the project structure of the original repo, only keeping the important stuff for this dry run. Run this in the project root:

```bash
python -m scripts.predict.batch_test -m .models\rispice-base -l .models\rispice-1000bp -i .data\hak1\sequences.tsv -o .data\hak1\ --cuda
```

Hopefully, this just runs as is. CUDA only works with nvidia chips, daw. If it fails, try running:

```bash
python -m scripts.predict.batch_test -m .models\rispice-base -l .models\rispice-1000bp -i .data\hak1\sequences.tsv -o .data\hak1\
```

this runs the model without cuda enabled (as in, CPU only). Even if you installed `cuda-enabled.txt`, this should still work. If this still didn't, some setup didn't go right. Maybe I can help with the debugging, but I'm sure an AI can read an error message better.