# Análise de Sentimento com GPT-3.5-turbo

Este repositório mostra como fazer uma análise de sentimento usando o GPT-3.5-turbo da OpenAI.

## Como Usar

1. **Instale a biblioteca OpenAI**

   ```bash
   pip install openai==0.28
   ```

2. **Configure a chave da API**

   No seu script, defina a chave da API:

   ```python
   import openai

   openai.api_key = "sua-chave-aqui"
   ```

3. **Exemplo de Análise de Sentimento**

   Use o método `ChatCompletion` para analisar o sentimento de um texto:

   ```python
   text = "Does not let me connect with my library. Very disappointed"

   prompt = f"""
   Esta é uma tarefa de análise de sentimento.\n Por favor, analise o sentimento do seguinte texto:\n {text}\n Sentimento:
   Responda apenas com o sentimento: Negativo, Positivo ou Neutro.
   """

   response = openai.ChatCompletion.create(
       model="gpt-3.5-turbo",
       messages=[
           {"role": "system", "content": "Você é um assistente de análise de sentimento."},
           {"role": "user", "content": prompt}
       ],
       temperature=0.5
   )

   sentiment = response.choices[0].message['content']
   print(sentiment)
   ```

4. **Função para Análise de Sentimento**

   Crie uma função para reutilizar:

   ```python
   def sentiment_analysis(text):
       prompt = f"""
       Esta é uma tarefa de análise de sentimento.\n Por favor, analise o sentimento do seguinte texto:\n {text}\n Sentimento:
       Responda apenas com o sentimento: Negativo, Positivo ou Neutro.
       """
       
       response = openai.ChatCompletion.create(
           model="gpt-3.5-turbo",
           messages=[
               {"role": "system", "content": "Você é um assistente de análise de sentimento."},
               {"role": "user", "content": prompt}
           ],
           temperature=0.5,
           max_tokens=10
       )
       sentiment = response.choices[0].message['content']
       return sentiment

   # Exemplo de uso da função
   text_2 = "Does not let me connect with my library. Very disappointed"
   print(sentiment_analysis(text_2))
   ```

E pronto! Agora você pode analisar o sentimento de qualquer texto usando o GPT-3.5-turbo.
