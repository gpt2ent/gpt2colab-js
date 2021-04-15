# gpt2colab-js
Make GPT-2 complete your text in Colab. Use fancy JS, instead of default ugly colab interface.
~~This is proof of concept for developers that want to create apps with graphics in Colab.~~

This is a branch with some extra scuffed JS that supports generating 10 samples per request. If you use this repo as a playground, this branch will likely be more useful.

"10 samples per request" is a hardcoded number and this won't be changed in this repo.

![Teaser image](https://pbs.twimg.com/media/Ey__EblWYAU9M1z?format=png&name=900x900)

# HuggingFace-powered models

* **transformers_js_playground.ipynb** enables you to use [text-generation models supported by HuggingFace](https://huggingface.co/models?pipeline_tag=text-generation) as long as they fit in your Colab runtime.
* **huggingface-api-js-playground.ipynb** lets you use [HuggingFace Inference API](https://api-inference.huggingface.co/docs/python/html/index.html) with the JS code. This is just an experimental piece of code and it is not really stable.

# Tweaking the code for custom models

1. Train your model *outside* of this notebook. This notebook is supposed to inference from already pretrained models.
3. Ensure you have a way to call your model *from within Python code* and get strings. That means if you infer text via calling external script -- something like `!python main.py --predict output.txt`) -- you need to examine the inference code of the script and write some sort of a function or an object that will handle your inference and return strings to you.
2. Discard all of the code that goes before `import google.colab.output` and copy your own code that loads and prepares your model.
5. Use the `ai_generate` function to connect your model to the JS:
   * The simplest way is to not change any arguments and just use your function/object to generate **a list of 10 strings** and put it into `result` variable before returning `JsonRepr(result)`.
       * Note that the function will receive `top_k`, `temp` and `length` as *string* variables and will convert these into numbers internally.
       * Also note that you aren't supposed to output any part of `prefix` as part of your output string.
   * If you want to use other parameters (e.g. `top_p`) you need to fix HTML and JS code (`generate()` function) in the second block. Again, note that JS will pass any arguments as *strings*.
   * If you want to customize `n_samples` you'll need to carefully check JS code because the magic number is hardcoded in several places.
