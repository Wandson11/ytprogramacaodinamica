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
