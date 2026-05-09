# VastAI + mineru Docker Image

This repo provides a docker image via GHCR which extends the base VastAI CUDA image with an installation of [mineru](https://github.com/opendatalab/MinerU), the fabulous framework for extracting Markdown from PDFs.
My use case is for pulling plain Markdown (including maths) from academic papers to make them more easily searchable etc.
Although it is possible to run mineru on a CPU, you really need a GPU for speed.
Likewise, although my aged M1 Macbook Pro /w 16GB RAM is able to run mineru on the Apple Silicon GPU, it is much quicker and only a few cents to run on an nVidia GPU at VastAI.

You can [launch an instance with this image at VastAI](https://cloud.vast.ai/?ref_id=519296&creator_id=519296&name=VastAI%20base%20%2B%20mineru) (referral link).
At the time of writing, you'll need to make sure it supports CUDA 13.2.
I would also aim for 16GB VRAM to be safe, I have found this necessary for some journal length PDFs.

Once the instance is up and running, `scp` your PDF up, e.g.

```
scp -P <PORT> myfile.pdf root@<IP>:/workspace
```

where `<PORT>` is the SSH port and `<IP>` the instance IP address from the VastAI console.

Then connect with SSH which should place you in the `/workspace` folder, after which you run:

```
source .venv/bin/activate
mineru -p myfile.pdf -o .
```

This will process the PDF and output a folder `myfile` which contains `myfile.md` and PDFs showing how the original document was parsed, together with a directory of extracted images.
