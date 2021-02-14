!!! warning 
        There seems to be an issue with the RapidAPI interactive endpoint explorer not properly sending requests as multipart/form-data. Make sure you use this guide as your reference for testing the API as the code snippets generated by RapidAPI don't work. Instead, please visit our own [interactive endpoint page](https://toonify.photos/api/interactive).

!!! info 
        All the examples below use the `v0/toonify` endpoint for the original Toonify model. We have [other models](../models) available at different endpoints. The expected parameters etc. are all the identical between the models, so the examples should work simply by changing the url.

## First steps

The following example uses the Python library Requests to send an image file for toonification. If the `Accept` header is `application/json` the response will be json, with images base64 encoded. 

```python
import requests

url = "https://toonify.p.rapidapi.com/v0/toonify"
headers = {
        "x-rapidapi-host": "toonify.p.rapidapi.com",
        "x-rapidapi-key": "KEY_HERE",
        "accept": "application/json",
        }
files = {"image": open("imagefile.jpg", "rb")}

response = requests.request("POST", url, files=files, headers=headers)

print(response.json())
```

will return a json response like this:

```json
{
    "num_faces": 1,
    "b64_encoded_output": "BASE64_IMAGE_HERE",
    "b64_encoded_aligned": ""
}
```

!!! note
    When returning a json response all images are base64 encoded and returned as a string. Here's an example of how to read one of these into a PIL Image in Python:

    ```python
    import base64
    from io import BytesIO
    from PIL import Image

    b64_encoded_output = "BASE64_IMAGE_HERE"
    file_like = BytesIO(base64.b64decode(b64_encoded_output))
    image = Image.open(file_like)

    image.show()
    ```

## Returning an image

If you want an image directly returned then set the `Accept` header to `image/jpeg`. Here is an example using curl for variety.

```bash
curl -X POST "https://toonify.p.rapidapi.com/v0/toonify" -H  "accept: image/jpeg" -H  "Content-Type: multipart/form-data" -H "x-rapidapi-host: toonify.p.rapidapi.com" -H "x-rapidapi-key: KEY_HERE" -F "image=@test.jpg;type=image/jpeg"
```


## Returning aligned image

If you want to return the cropped and aligned face as well as the toonified result you can pass a query parameter of `return_aligned=True`. If the return type is json then the aligned face will be returned base64 encoded in the `b64_encoded_aligned` field. If the return type is an image then the two images will be horizontally concatenated and returned.


```python
import requests

url = "https://toonify.p.rapidapi.com/v0/toonify"
query = {
        "face_index": 1, 
        "return_aligned":"true",
        }
headers = {
        "x-rapidapi-host": "toonify.p.rapidapi.com",
        "x-rapidapi-key": "KEY_HERE",
        "accept": "image/jpeg"
        }
files = {"image": open("imagefile.jpg", "rb")}

response = requests.request("POST", url, files=files, headers=headers, params=query)

print(reponse.content) #will be the jpeg image bytes
```

![](https://assets.justinpinkney.com/toonify/images/pair.jpeg)

__Next take a look at the various options you have: [More Options](more-options)__