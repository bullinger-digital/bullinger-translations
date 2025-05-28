# bullinger-translations

This repository contains automatically generated translations of the letters of the [Bullinger Digital Edition](https://www.bullinger-digital.ch/).
They were not manually checked and may therefore contain errors.

## German translations of Latin letters

The folder [la_de](la_de) contains German translations of the Latin letters. Only letters that contain at least one
latin sentence are included. Each sentence was translated separately by the
[Machine Translation system](https://translate.bullinger-digital.ch/) (Model Update: January 2023) as part of the Bullinger
Digital Project. Therefore, context information across sentences is not taken into account.

## English translations

The folder [all_en](all_en) contains English translations of all letters in the HBBW edition (volumes 1 to and including 21) as well as all letters with provisional transcription. The translations were created using GPT4o by [openAI](https://openai.com/) in April 2025. Since previous experiments had shown that this could improve the translation quality, the summary (the regest) of a letter (created manually for all letters in the HBBW edition) was sent to GPT together with the letter text to be translated and lexical information on Early New High German expressions (created manually as footnotes in the HBBW edition) was added to these as a note in brackets. The detailed documentation (in German) can be found in [all_en_gpt4o.md](all_en_gpt4o.md)
