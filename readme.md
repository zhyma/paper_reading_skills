## Inside the repo:

The repo contains two tools for paper reading. One is to handle Google Scholar daily subscription, the other is for general paper reading. You may first want to convert the SKILLs to your native lanuage, and modify it to output in your native language.

## How to use:

- `ChatGPT` chat mode does not consume token. These SKILLs are original designed to use in the chat mode to save token.

- `google-scholar-periodic-paper-subscription-PROMPT-V*.md` contains the prompt to handle Google Scholar daily subscription. You need to create a scheduled task, and add the content as the prompt.


- `paper-reading-unified-SKILL-V*.md` contains the prompt to handle paper in general (or a DLO manipulation paper). You first copy the ArXiv link or upload a paper PDF to the dialog box, copy paste the text in `paper-reading-execution-prompt.md` to the dialog box, and upload (or load from your file saved on ChatGPT) the `paper-reading-unified-SKILL-V*.md`. You can add additional prompt such as asking it to output a short summary only. These prompts explains how to read a paper structually (in my way).