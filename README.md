# Organizador de Dinâmicas IQVIA

Ferramenta web (HTML único, sem backend) que recebe a base bruta do IQVIA e gera um arquivo Excel com duas tabelas dinâmicas **nativas** do Excel, já formatadas e prontas para uso.

Todo o processamento acontece no navegador do usuário. Nenhum dado é enviado para servidor.

## O que ela gera

Um arquivo `.xlsx` com duas abas, cada uma com uma tabela dinâmica nativa do Excel:

- **MARCA-BRICK-PDV**: Setor > Marca > Brick > PDV
- **PDV-MARCA-APRESENTAÇÃO**: Setor > PDV > Marca > Apresentação

Características da saída:

- Tabelas dinâmicas nativas (objeto vivo do Excel, não grade estática), expansíveis pelo "+"
- Recolhidas por setor ao abrir
- Meses no eixo de coluna como data (formato mmm-yy)
- Congelamento da coluna A e do cabeçalho
- Degradê de cores por nível da hierarquia, negrito, itálico e bordas, ancorados à estrutura da tabela (a formatação se mantém ao expandir os níveis)

## Como usar

1. Abra a ferramenta no navegador
2. Arraste a base bruta do IQVIA (arquivo `.xlsx`) para a área indicada
3. Aguarde o processamento
4. Baixe o arquivo gerado

A base de entrada precisa ter o cabeçalho com as colunas Regional, Distrital, Setor, Marca, Brick, Bandeira, PDV, Apresentação, além das colunas de valor e mês.

## Rodar localmente

Não há build. Basta abrir o arquivo `index.html` no navegador, ou servir a pasta com qualquer servidor estático:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000
```

## Publicar no Render

A ferramenta é um site estático, então o deploy é direto.

1. Suba este repositório no GitHub
2. No Render, clique em **New > Static Site**
3. Conecte o repositório
4. Configure:
   - **Build Command**: deixe em branco
   - **Publish Directory**: `.`
5. Clique em **Create Static Site**

A cada novo commit no GitHub, o Render publica automaticamente.

O arquivo `render.yaml` incluído permite também usar o recurso de Blueprint do Render (New > Blueprint), que já aplica essas configurações.

## Tecnologias

- HTML, CSS e JavaScript puro (vanilla), sem framework
- Web Worker (processamento fora da thread principal da interface)
- SheetJS (leitura da base) e fflate (compactação do .xlsx), ambos via CDN
- Geração direta do OOXML da tabela dinâmica nativa
