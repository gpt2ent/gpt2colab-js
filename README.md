# gpt2colab-js
Make GPT-2 complete your text in Colab. Use fancy JS, instead of default ugly colab interface.
~~This is proof of concept for developers that want to create apps with graphics in Colab.~~

This is a branch with some extra scuffed JS that supports generating 10 samples per request. If you use this repo as a playground, this branch will likely be more useful.

"10 samples per request" is a hardcoded number and this won't be changed in this repo.

![Teaser image](https://pbs.twimg.com/media/Ey__EblWYAU9M1z?format=png&name=900x900)

# HuggingFace-powered models

* **transformers_js_playground.ipynb** enables you to use [text-generation models supported by HuggingFace](https://huggingface.co/models?pipeline_tag=text-generation) as long as they fit in your Colab runtime.
* **huggingface-api-js-playground.ipynb** lets you use [HuggingFace Inference API](https://api-inference.huggingface.co/docs/python/html/index.html) with the JS code. This is just an experimental piece of code and it is not really stable.
