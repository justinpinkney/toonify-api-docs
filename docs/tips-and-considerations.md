## Please note

- __The current model costs 2 credits per use. We expect to introduce other models for both more and fewer credits in future.__
- This works out around 45 cents per thousand uses for one of the prepaid bundles. If you're interested in different pricing bundles then please contact us.
- Inference time is around 7 seconds. I could to much to improve this is there is sufficient demand and usage.
- We expect to release other models, for different transformations and also different resolutions. If you're interested in something please let us know!
- If you want to see examples of the current Toonify model being used look at https://toonify.justinpinkney.com
- The RapidAPI endpoint interface doesn't appear to send mulipart/form data properly, so doesn't work. Please see our code examples for reference.

## How to get good results

- Make sure the original image is fairly high quality (e.g. face is around 512x512 pixels)
- Faces in the image which are below around 128x128 pixels are unlikely to be found
- Straight on faces work best, side on faces aren't likely to be found.