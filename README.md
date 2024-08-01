# ggplotGPT

Um aplicativo shiny que faz a interface de um chat que te permite conversar com o conteúdo da documentação do pacote `ggplot2` usando o modelo de IA generativa da openAI, o chatgpt-4o.

Este aplicativo shiny usa o pacote `reticulate` para fazer a integração do R com o Python, e por isso, alguns cuidados devem ser tomados na hora de fazer o deploy. Para rodar localmente, basta ter uma versão do python 3 instalado. 

A publicação dele foi feita através do [shinyapps.io](https://www.shinyapps.io/).
No inicio do código, há a criação e configuração de um ambiente virtual python para possibilitar a execução do código, veja:

```{r}
reticulate::virtualenv_create("ggplotgpt")

reticulate::virtualenv_install(envname = "ggplotgpt",
                               packages = c(
                                 "langchain",
                                 "langchain-community",
                                 "pypdf",
                                 "pinecone",
                                 "langchain_pinecone",
                                 "langchain-openai",
                                 "pinecone-client[grpc]",
                                 "langchain_openai"
                               ))

reticulate::use_virtualenv("ggplotgpt")
```

**Importante:** não use o comando `library(reticulate)` para carregar o pacote, use a sintaxe `reticulate::`, do contrário, você terá problemas durante o deploy, já que o comando `library(reticulate)` carrega um ambiente do python imediatamente, e não será o ambiente correto, o que foi chamado no código acima de `ggplotgpt`.
