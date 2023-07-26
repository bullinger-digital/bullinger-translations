# bullinger-translations

This repository contains automatically generated translations of the letters of the [Bullinger Digital Edition](https://www.bullinger-digital.ch/).
They were not manually checked and may therefore contain errors.


## German translations of Latin letters
The folder [la_de](la_de) contains German translations of the Latin letters. Only letters that contain at least one 
latin sentence are included. Each sentence was translated separately by the
[Machine Translation system](https://translate.bullinger-digital.ch/) (Model Update: January 2023) as part of the Bullinger 
Digital Project. Therefore, context information across sentences is not taken into account.

## English translations
The folder [all_en](all_en) contains English translations of the first 123 letters of the Bullinger Digital Edition. All sentences were translated, regardless of the source language. The
translations were created using GPT3 by [openAI](https://openai.com/) (specifically, the `text-davinci-003` model) 
in May 2023.
The letters were split into chunks of paragraphs that fit the context length of the model and translated separately. 
Therefore, context information within chunks is taken into account, but not across chunks. Each chunk was prefixed with
the prompt `Translate the following text into English:`. 


