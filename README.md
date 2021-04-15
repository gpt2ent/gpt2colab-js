# gpt2colab-js
Make GPT-2 complete your text in Colab. Use fancy JS, instead of default ugly colab interface.
This is proof of concept for developers that want to create apps with graphics in Colab.

If you want to use this code as your playground check out [the 'multisample' branch](https://github.com/gpt2ent/gpt2colab-js/tree/multisample) for more useful notebooks.
![Teaser image](./gpt2js.png)

# How to use the interface with your model

If your model [is uploaded to HuggingFace](https://huggingface.co/models?pipeline_tag=text-generation), check out [the 'multisample' branch](https://github.com/gpt2ent/gpt2colab-js/tree/multisample).

For custom models the idea is the following:

1. Train your model *outside* of this notebook. This notebook is supposed to inference from already pretrained models.
3. Ensure you have a way to call your model *from within Python code* and get a string. That means if you infer text via calling external script -- something like `!python main.py --predict output.txt`) -- you need to examine the inference code of the script and write some sort of a function or an object that will handle your inference and return strings to the code, not just print the result or write it to file.
2. Discard all of the code that goes before `import google.colab.output` and copy your own code that loads and prepares your model. Add `model_name` and `spinner_speed` variables or your HTML code won't run. Note that `spinner_speed` is a string variable that looks like `"400ms"`.
5. Use the `ai_generate` function to connect your model to the JS:
   * The simplest way is to not change any arguments and just use your function/object to generate a string and put it into `result` variable before returning `JsonRepr(result)`.
       * Note that the function will receive `top_k`, `temp` and `length` as *string* variables and will convert these into numbers internally.
       * Also note that you aren't supposed to output any part of `prefix` as part of your output string.
   * If you want to use other parameters (e.g. `top_p`) you need to fix HTML and JS code (`generate()` function) in the second block. Again, note that JS will pass any arguments as *strings*.
