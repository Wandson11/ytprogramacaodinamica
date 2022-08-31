Sintaxes para adequar o numero de caracteres de uma coluna: pd.get_option('max_colwidth'), vai te mostrar quantos caracteres seu interpretador aceita para cada coluna.
pd.set_option('max_colwidth', None), vai alterar o tamanho das colunas, e "None" e sem limite, mas pode ao invés de None pode ser digitado qualquer valor, 60, 170, etc.
Para saber quantos caracteres tem o df: variavel['coluna a ser analisada'].str.len().max().
A função pd.get_option('max_columns'), vai te mostrar a quantidade de colunas apresentadas no display, se forem muitas, algumas serão suprimidas por reticências.
Para mostrar todas: pd.set_option('max_columns', xx), o "xx" é a quantidade de colunas que se deseja que apareça na tela.

dica03:ordenar o resultado via "sort_values" de um describe, por parâmetro a ser definido (mean, median, min, max).
O comando geral que não funciona: variável.describe().sort_values(by='mean') mas, se ao inves de mean, inserir o nome da coluna, o interpretador funcionará, mas esse não é o ponto.
A forma para usar o mean é indicando qual eixo "axis" será ordenado, se nada for alterado, o eixo modificado será 0, o que remete a linha, mas o correto é alterar para 1, coluna
variável.describe().sort_values(by='mean', axis=1).
Outra forma de fazer isso sem especificar o "axis", é transpondo a coluna: variável.describe().T.sort_values(by='mean') , o "T", é o comando que transpor.

dica04: verificar se 2 dfs são iguais.
a sintaxe para esse análise de 2 dfs é: assert_frame_equal(df1, df2), podendo ainda ser acrescentando o 'check_dtype=False', para ignorar o tipo.
https://pandas.pydata.org/docs/reference/api/pandas.testing.assert_frame_equal.html
é necessário carregar a biblioteca: from pandas.testing import assert_frame_equal
Outra dica é a função "variavel ou df.copy()"

dica05: usar style para destacar determinadas células do df, seja por valor máx, min, mean, median, etc.
https://pandas.pydata.org/pandas-docs/stable/user_guide/style.html
variavel.style.highlight_max() , vai destacar os maiores valores de cada coluna de um df. 
Ainda é possível repassar esse comando para somente uma coluna: variavel.style.highlight_max(subset = ['coluna a'], color='red'), não precisa indicar a cor, pois já tem um predefinida, mas se quiser alterar.
Se o caso, for de colocar um conjunto de cores em um dataframe numérico, existe tambem essa função:
dataframe.style.background_gradient(cmap='viridis') ou cmpa='Reds'. Paleta de cores: https://matplotlib.org/stable/tutorials/colors/colormaps.html
Para pintar um dataframe inteiro, mesmo que sem o efeito gradiente, a expressão é: dataframe/variavel. style.set_properties(**{'background-color': 'black', 'color': 'lawngreen', 'border-color': 'white'}), essas cores são editáveis
E, por último, remetendo ainda a style, existe a função para quando o mouse passar por cima de uma linha, essa linha ser destacada:
variável.set_table_style([{'selector': 'tr:hover', 'props': [('background-clor', 'red'), ('color', 'white')]}])

dica06 - variável categórica e transformação.
Logo no "pd.read", é possivel informar ao interpretador se alguma coluna é categórica pela sintaxe dtype = {'colunacategorica':'category'}.
Uma vez feito isso, de indicar coluna categórica, uma forma de transformar categórica em númerica, é pela expressão: cat.codes, assim, cada grupo, receberá um número.
dataframe['coluna a ser transformada'].cat.codes
Se quiser transformar uma coluna float em categórica, a sintaxe a ser usada é "pd.cut", onde será indicado a divisão grupo a grupo:
pd.cut(dataframe.coluna, bins=[x, 2x, 3x, 4x], labels=[um nome para cada grupo, com aspas simples e separadas por vírgula])
existe ainda o qcut, que faz de forma automatica essa parte do bins, informando apenas em quantos grupo deseja a separação, que seja feita de forma distribuida
pd.qcut(dataframe.coluna, q=4 (4 é so um exemplo, pode ser qualquer número)),se não colocar labels, funciona também

dica07: bar_chart_race: para fazer download pip install bar_chart_race.
corrida dos gráficos de barra em tempo real.
É indicado que o index sejam as datas, e as colunas, por exemplo, estados, cidades, paises.

dica08: para construir um gráfico mais interativo via pd e plotly
o material, será carregado pela sintaxe: pd.options.plotting.backend='plotly'
expressoa do gráfico. dataframe.grafico.value_counts().sort_index().plot(kind='bar')
Não precisa citar o tamanho do gráfico com fontsize e, nao precisa do ";" depois do parênteses.

dica09: upar um arquivo diramente do winrar sem descompactar.
Inicialmente, é necessário importar uma biblioteca de nome "zipfile".
feita a importação, o passo seguinte é o de abrir o winrar e verificar os arquivos ali dentro, para isso: with zipfile.ZipFile('caminho do arquivo carregado no colab') as z:
print(*z.namelist(), sep='\n').
analisada a lista de arquivo, basta verificar quais dos arquivos será upado com df, nessa etapa o procedimento a ser feito é o seguinte:
with zipfile.ZipFile('') as z:
  with z.open('nome do arquivo dentro do winrar') as f:
    variavel = pd.read_csv(f)
    
dica11: uso de geopandas as gpd, para elaborar mapas
o procedimento inicial é igual ao pandas: variavel= gpd.read_file(); variavel.head().
variavel.plot() - primeiro gráfico

dica13: para saber se um site permite a raspagem de dados, basta ao final inserir "/robots.txt".
https://pt.wikipedia.org/robots.txt
