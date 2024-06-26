# oobapi-stream
[oobabooga/text-generation-webui](https://github.com/oobabooga/text-generation-webui) streaming api wrapper

  This is a simple isomorphic wrapper for the oobabooga api that handles the necessary HTTP shenanigans to stream token predictions to you as they come instead of getting a result all at once. To use it, API mode must be enabled when [launching ooba](https://github.com/oobabooga/text-generation-webui#api) by using `--api`
  
## Usage

  Ｗhen instantiating the api you can specify a host and a port, as well as default generation options．
  ```js
  import ooba from 'oobapi-stream'
  const generation_options = {max_new_tokens: 1000}
  const host = 'remote.host.net'
  const port = 1337
  const api = ooba({host,port}, generation_options)
  ```
  or if you're running ooba locally and you want to use the default options you can omit both
  ```js
  const api = ooba()
  ```
  this will return an api object that is ready to make streaming requests.

  in order to generate text simply call `api.generate()` with a prompt
  ```js
  const prompt = "In order to make homemade bread, follow these steps:\n1)"
  api.generate(prompt)
  ```
  
  and listen to generated tokens by supplying a function to `api.ontoken` 
  ```js
  api.ontoken = token => console.log(token)
  ```

  you can also pass an options object containing any parameters for the specific generation instead of a string 
  ```js
  api.generate({
    prompt: 'please write me a very long poem\n',
    max_new_tokens: 1000,
  })
  ```

  additionally, the default `parameters` object is exposed as a property of the `api` object and can be freely modified to change the default parameters after instantiation
  ```js
  api.parameters.max_new_tokens = 1000
  ```

## Additional Notes

  Currently only the `stream` [api](https://github.com/oobabooga/text-generation-webui/blob/main/api-example-stream.py) is supported. The `chat-stream` [api](https://github.com/oobabooga/text-generation-webui/blob/main/api-example-chat-stream.py) is coming soon.

