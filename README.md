# Project: Applying Vietnamese language to the CLIP model
This Jupyter notebook can be considered an exercise to help me learn how to handle both image and text processing. Additionally, it helps me get familiar with OpenAI's CLIP model and apply Gradio UI to create an interface.
These following steps:
  1. Using dataset from Kaggle: [Flick 30k Dataset](https://www.kaggle.com/datasets/adityajn105/flickr30k)
  2. In order to handle in Vietnamese text, I download and import deep_translator
       ```python
       !pip install deep-translator -q
       from deep_translator import GoogleTranslator
       ```
     after that you can try some code
       ```python
       from deep_translator import GoogleTranslator
       def encode_text(text):
          # Translate English text to Vietnamese
          translated_text = GoogleTranslator(source='vi', target='en').translate(text)
          print(f"Translated text: {translated_text}")
       # Example usage:
       encode_text("bird")
       ```
       (Actually, my team tried to build and train from scratch, but due to limited machine capacity, that plan has been put off for now)
  3. After completing the text-to-image function, our team was asked to use a vector database to store the image embedding vectors. We found Pinecone, which is an ideal API for implementing image search.
     
     You can read more: [Pinecone](https://app.pinecone.io/organizations/-O8_zvi_yYrICdZWOojj/projects/a5d60944-5800-4cdf-a863-bf8c1df6c04d/indexes)

     Example code:

     ```python
     !pip install pinecone
     if df.empty:
      print("DataFrame is empty after filtering. Check the data and the fix_array_format_safe function.")
     else:
      pc = Pinecone(api_key='your_api_key')
  
     index_name = 'your_create_index'
     if index_name not in pc.list_indexes().names():
          pc.create_index(
              name=index_name,
              dimension=vector_dimension,
              metric='cosine',
              spec=ServerlessSpec(
                  cloud='aws',
                  region='us-east-1'
              )
          )
  
     index = pc.Index(index_name)
     ```

4. Use Gradio to integrate and deploy the functions we have developed
   ```python
   !pip install gradio -q
   ```



      


