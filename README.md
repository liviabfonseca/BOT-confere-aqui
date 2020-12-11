# BOT-confere-aqui
conseguiu desenvolver todo o algoritmo de cálculo baseado em princípios da lógica fuzzy, porém apenas testes offline e fora do Twitter podem ser realizados com um algoritmo de teste. Alguns erros e limitações impediram o protótipo de se tornar testável online. Impedimentos na API do Twitter e na Cloud do serviço pythonanywhere.com tornaram o processo de solução mais complexo limitando o tempo.  O protótipo da nossa aplicação se baseia em ler o texto que o usuário escreveu no Twitter e verifica, a princípio, duas características: 1- Se possui algum link de referência; 2- Se contém algumas das palavras-chave propostas pela equipe e que, conforme pesquisa, tendem a caracterizar uma notícia falsa.
#ALGORITMO DESENVOLVIDO PELA EQUIPE UNDER CONTROL


textoTweet = input('Informe um texto de Tweet para teste: ')

indiceDePerigoGeral = 0
textoTweet = textoTweet.lower()
textoTweetSeparado = textoTweet.split()

def verificarPalavrasChave(textoTweetSeparado):
    indiceDeConfianca = 100
    palavrasChave = ['você','vacina','causa','causar','cura','curar','covid-19','farsa','conspiração','revolucionário','milagrosa','revolucionária','agora','câncer']
    for text in textoTweetSeparado:
        if text in palavrasChave:
            indiceDeConfianca = indiceDeConfianca - 1
    return indiceDeConfianca


def verificarLinkDeReferencia(textoTweetSeparado):
    indiceDePerigo = 100
    for text in textoTweetSeparado:
        if ('www' in text)or('.com' in text):
                indiceDePerigo = indiceDePerigo - 1
    return indiceDePerigo

indiceDePerigoGeral = verificarPalavrasChave(textoTweetSeparado) + verificarLinkDeReferencia(textoTweetSeparado)

confianca = indiceDePerigoGeral - 100
if confianca > 95:
    print(f' Olá, encontrei alguns detalhes no Tweet, recomendo a revisão, porém não parece ser Fake\n Meu índice de confiança é de {confianca}%')
else:
    print(f'Olá, algumas informações neste Tweet não parecem concisas, cuidado ao compartilhar, pode ser uma Fake News\n Meu índice de confiança é de {confianca}%')
