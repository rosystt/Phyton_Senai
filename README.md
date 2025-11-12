# --- IMPORTAÇÃO DAS BIBLIOTECAS ---
import pandas as pd
import matplotlib.pyplot as plt

# --- FASE 1: CRIAÇÃO DA BASE DE DADOS ---
print("=== FASE 1: CRIAÇÃO DA BASE DE DADOS ===")

# Criando dados dos clientes
clientes = {
    'ID_Cliente': [1, 2, 3, 4, 5, 6],
    'Nome_Cliente': ['Ana Silva', 'Bruno Costa', 'Carla Dias', 'David Martins', 'Elisa Fernandes', 'Fábio Guedes'],
    'Estado': ['SP', 'RJ', 'MG', 'BA', 'SP', 'RJ']
}
df_clientes = pd.DataFrame(clientes)
print("\n1. Tabela de Clientes:")
print(df_clientes)

# Criando dados dos produtos
produtos = {
    'ID_Produto': [101, 102, 103, 104, 105],
    'Nome_Produto': ['Notebook Pro', 'Mouse Óptico', 'Teclado Mecânico', 'Monitor 4K', 'Cadeira Gamer'],
    'Categoria': ['Eletrônico', 'Eletrônico', 'Eletrônico', 'Eletrônico', 'Escritório'],
    'Preco_Unitario': [5000.00, 80.00, 350.00, 1800.00, 1200.00]
}
df_produtos = pd.DataFrame(produtos)
print("\n2. Tabela de Produtos:")
print(df_produtos)

# Criando dados das vendas
vendas = {
    'ID_Venda': list(range(1, 16)),
    'ID_Cliente': [1, 2, 1, 3, 5, 6, 4, 2, 5, 1, 3, 6, 2, 4, 5],
    'ID_Produto': [101, 102, 104, 105, 103, 101, 105, 104, 102, 103, 105, 102, 101, 103, 104],
    'Quantidade': [1, 2, 1, 1, 1, 1, 1, 1, 3, 2, 1, 1, 1, 3, 1]
}
df_vendas = pd.DataFrame(vendas)
print("\n3. Tabela de Vendas:")
print(df_vendas)

# --- FASE 2: TRANSFORMAÇÃO E ENRIQUECIMENTO ---
print("\n=== FASE 2: TRANSFORMAÇÃO E ENRIQUECIMENTO ===")

# Unindo as tabelas
df_completo = df_vendas.merge(df_clientes, on='ID_Cliente').merge(df_produtos, on='ID_Produto')

# Calculando o valor total de cada venda
df_completo['Valor_Total'] = df_completo['Quantidade'] * df_completo['Preco_Unitario']

# Classificando prioridade de entrega
def classificar_entrega(valor):
    if valor > 1000:
        return 'Expresso'
    else:
        return 'Normal'

df_completo['Prioridade_Entrega'] = df_completo['Valor_Total'].apply(classificar_entrega)

print("\nTabela Completa após transformações:")
print(df_completo.head(8))

# --- FASE 3: ANÁLISE E RESPOSTAS DE NEGÓCIOS ---
print("\n=== FASE 3: ANÁLISE E RESPOSTAS DE NEGÓCIOS ===")

# 1. Faturamento por categoria
faturamento_categoria = df_completo.groupby('Categoria')['Valor_Total'].sum()
print("\n1. Faturamento por Categoria:")
print(faturamento_categoria)

# 2. Quantidade vendida por estado
vendas_estado = df_completo.groupby('Estado')['Quantidade'].sum()
print("\n2. Quantidade Vendida por Estado:")
print(vendas_estado)

# 3. Top 3 clientes
top_clientes = df_completo.groupby('Nome_Cliente')['Valor_Total'].sum().nlargest(3)
print("\n3. Top 3 Clientes:")
print(top_clientes)

# 4. Produto mais vendido em Eletrônicos
eletronicos = df_completo[df_completo['Categoria'] == 'Eletrônico']
mais_vendido = eletronicos.groupby('Nome_Produto')['Quantidade'].sum().nlargest(1)
print("\n4. Produto Mais Vendido em Eletrônicos:")
print(mais_vendido)

# --- FASE 4: APRESENTAÇÃO DOS RESULTADOS ---
print("\n=== FASE 4: APRESENTAÇÃO DOS RESULTADOS ===")

import pandas as pd
import matplotlib.pyplot as plt

# --- FASE 1: CRIAÇÃO DA BASE DE DADOS ---
print("=== FASE 1: CRIAÇÃO DA BASE DE DADOS ===")

# Criando dados dos clientes
clientes = {
    'ID_Cliente': [1, 2, 3, 4, 5, 6],
    'Nome_Cliente': ['Ana Silva', 'Bruno Costa', 'Carla Dias', 'David Martins', 'Elisa Fernandes', 'Fábio Guedes'],
    'Estado': ['SP', 'RJ', 'MG', 'BA', 'SP', 'RJ']
}
df_clientes = pd.DataFrame(clientes)
print("\n1. Tabela de Clientes:")
print(df_clientes)

# Criando dados dos produtos
produtos = {
    'ID_Produto': [101, 102, 103, 104, 105],
    'Nome_Produto': ['Notebook Pro', 'Mouse Óptico', 'Teclado Mecânico', 'Monitor 4K', 'Cadeira Gamer'],
    'Categoria': ['Eletrônico', 'Eletrônico', 'Eletrônico', 'Eletrônico', 'Escritório'],
    'Preco_Unitario': [5000.00, 80.00, 350.00, 1800.00, 1200.00]
}
df_produtos = pd.DataFrame(produtos)
print("\n2. Tabela de Produtos:")
print(df_produtos)

# Criando dados das vendas
vendas = {
    'ID_Venda': list(range(1, 16)),
    'ID_Cliente': [1, 2, 1, 3, 5, 6, 4, 2, 5, 1, 3, 6, 2, 4, 5],
    'ID_Produto': [101, 102, 104, 105, 103, 101, 105, 104, 102, 103, 105, 102, 101, 103, 104],
    'Quantidade': [1, 2, 1, 1, 1, 1, 1, 1, 3, 2, 1, 1, 1, 3, 1]
}
df_vendas = pd.DataFrame(vendas)
print("\n3. Tabela de Vendas:")
print(df_vendas)

# --- FASE 2: TRANSFORMAÇÃO E ENRIQUECIMENTO ---
print("\n=== FASE 2: TRANSFORMAÇÃO E ENRIQUECIMENTO ===")

# Unindo as tabelas
df_completo = df_vendas.merge(df_clientes, on='ID_Cliente').merge(df_produtos, on='ID_Produto')

# Calculando o valor total de cada venda
df_completo['Valor_Total'] = df_completo['Quantidade'] * df_completo['Preco_Unitario']

# Classificando prioridade de entrega
def classificar_entrega(valor):
    if valor > 1000:
        return 'Expresso'
    else:
        return 'Normal'

df_completo['Prioridade_Entrega'] = df_completo['Valor_Total'].apply(classificar_entrega)

print("\nTabela Completa após transformações:")
print(df_completo.head(8))

# --- FASE 3: ANÁLISE E RESPOSTAS DE NEGÓCIOS ---
print("\n=== FASE 3: ANÁLISE E RESPOSTAS DE NEGÓCIOS ===")

# 1. Faturamento por categoria
faturamento_categoria = df_completo.groupby('Categoria')['Valor_Total'].sum()
print("\n1. Faturamento por Categoria:")
print(faturamento_categoria)

# 2. Quantidade vendida por estado
vendas_estado = df_completo.groupby('Estado')['Quantidade'].sum()
print("\n2. Quantidade Vendida por Estado:")
print(vendas_estado)

# 3. Top 3 clientes
top_clientes = df_completo.groupby('Nome_Cliente')['Valor_Total'].sum().nlargest(3)
print("\n3. Top 3 Clientes:")
print(top_clientes)

# 4. Produto mais vendido em Eletrônicos
eletronicos = df_completo[df_completo['Categoria'] == 'Eletrônico']
mais_vendido = eletronicos.groupby('Nome_Produto')['Quantidade'].sum().nlargest(1)
print("\n4. Produto Mais Vendido em Eletrônicos:")
print(mais_vendido)

# --- FASE 4: APRESENTAÇÃO DOS RESULTADOS ---
print("\n=== FASE 4: APRESENTAÇÃO DOS RESULTADOS ===")

# Configurando o gráfico
fig, ax = plt.subplots(figsize=(10, 6))

# Pegando as categorias e os valores
categories = faturamento_categoria.index
values = faturamento_categoria.values

# Definindo as cores
colors = ['#2cb8b2', '#268fbe']

# Criando as barras com bordas pretas e espessura reduzida, e diminuindo a largura das barras
bars = ax.bar(categories, values, color=colors, edgecolor='black', linewidth=0.5, width=0.6)

plt.title('Faturamento Total por Categoria', fontsize=14, fontweight='bold')
plt.xlabel('Categoria', fontsize=12)
plt.ylabel('Faturamento (R$)', fontsize=12)
plt.xticks(rotation=45)
# Removendo a linha de fundo
ax.grid(False)

# Adicionando rótulos de porcentagem
total_faturamento = faturamento_categoria.sum()
for bar in bars.patches:
    height = bar.get_height()
    percentage = (height / total_faturamento) * 100
    ax.text(bar.get_x() + bar.get_width() / 2, # Posição x
            height / 2, # Posição y (centralizado dentro da barra)
            f'{percentage:.1f}%', # Texto do rótulo
            ha='center', # Alinhamento horizontal
            va='center', # Alinhamento vertical
            fontsize=10, # Tamanho da fonte
            color='white') # Cor da fonte (branco para contraste com a cor da barra)

plt.tight_layout()

# Salvando o gráfico
plt.savefig('faturamento_categoria.png', dpi=300)
plt.show()

# Exportando para Excel
df_completo.to_excel('relatorio_ecommerce.xlsx', index=False)
print("\nRelatório exportado para 'relatorio_ecommerce.xlsx'")

print("\n=== ANÁLISE CONCLUÍDA ===")
