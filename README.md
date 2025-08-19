# ourivesaria-tavares
Repository name: ourivesaria-tavares Description: 💎 Sistema de gestão para ourivesaria - Django API REST ✅ Public ✅ Add a README file

Trabalho final de apresentação de projeto em FrontEnd SENAI-RJ O Projeto: Sistema de Gestão Integrada "Ourivesaria Tavares"

A História da Empresa: "Ourivesaria Tavares - Tradição e Modernidade" A história da "Ourivesaria Tavares" começa com Manuel Tavares, um jovem ourives que imigrou de Portugal para o Brasil nos anos 70. Em 1975, ele abriu sua pequena oficina em São Paulo, que se tornou referência por suas joias em ouro e prata de alta qualidade. Em 2024, seu neto, Rafael, formado em Administração e Tecnologia, assume o negócio com uma nova visão. Para honrar o legado de seu avô e ao mesmo tempo atrair um público mais amplo, Rafael decide expandir a linha de produtos. A loja agora oferecerá não apenas as tradicionais joias finas, mas também uma curadoria de semijoias banhadas, bijuterias de design exclusivo e peças modernas em aço inox. A filosofia da empresa, que guia essa nova fase, é clara: "Nos juntamos por amor a joias. Criamos joias que simbolizam sentimentos e histórias únicas. Atendemos as expectativas, pois serão memórias que passarão para futuras gerações." Essa expansão, no entanto, tornou o controle manual, feito em livros de registro, completamente obsoleto. Era impossível gerenciar um inventário tão diverso, com diferentes materiais, categorias e tipos de peças, e obter dados diários para entender o que vendia mais. Para organizar a operação e impulsionar o crescimento, Rafael decidiu que era essencial criar um sistema de gestão sob medida. Assim nasceu a necessidade do SGI - Sistema de Gestão Integrada "Ourivesaria Tavares", uma plataforma para gerenciar um catálogo de produtos diversificado e complexo.
Entidades do Sistema O modelo de dados foi atualizado para refletir o novo escopo: 1.Material: O metal base da peça. oExemplos: Ouro 18k, Prata 950, Aço Inox, Latão (para bijuterias). 2.Joia (Peça): A entidade central do produto, agora com mais classificações. oTipo: Classificação principal da peça. Valores: Joia, Semijoia, Bijuteria. oCategoria: O formato ou uso da peça. Valores: Anel, Aliança, Brinco, Colar/Gargantilha, Piercing, Conjunto. oAtributos: Nome, SKU, Preço, Material, etc. 3.Designer: O criador da peça (pode ser a própria ourivesaria ou um terceiro). 4.Gema: Pedras usadas, mais comuns em joias e semijoias. 5.Estoque: Controla a quantidade disponível de cada Joia. 6.Venda: Registra uma transação comercial.
Modelo Lógico (Estrutura do Banco de Dados) O modelo lógico é adaptado para incluir as novas classificações na entidade Joia. models.py (Exemplo da classe Joia) class Joia(models.Model):
--- Novas Classificações --2. Entidades do Sistema
O modelo de dados foi atualizado para refletir o novo escopo: 1.Material: O metal base da peça. oExemplos: Ouro 18k, Prata 950, Aço Inox, Latão (para bijuterias).

2.Joia (Peça): A entidade central do produto, agora com mais classificações. Tipo: Classificação principal da peça.

Valores: Joia, Semijoia, Bijuteria. Categoria: O formato ou uso da peça. Valores: Anel, Aliança, Brinco, Colar/Gargantilha, Piercing, Conjunto. Atributos: Nome, SKU, Preço, Material, etc.

3.Designer: O criador da peça (pode ser a própria ourivesaria ou um terceiro).

4.Gema: Pedras usadas, mais comuns em joias e semijoias.

5.Estoque: Controla a quantidade disponível de cada Joia.

6.Venda: Registra uma transação comercial.

Modelo Lógico (Estrutura do Banco de Dados) O modelo lógico é adaptado para incluir as novas classificações na entidade Joia. models.py (Exemplo da classe Joia)
class Joia(models.Model): # --- Novas Classificações --- TIPO_CHOICES = [- TIPO_CHOICES = [ ('JOIA', 'Joia'), ('SEMIJOIA', 'Semijoia'), ('BIJUTERIA', 'Bijuteria'), ] CATEGORIA_CHOICES = [ ('ANEL', 'Anel'), ('ALIANCA', 'Aliança'), ('BRINCO', 'Brinco'), ('COLAR', 'Colar/Gargantilha'), ('PIERCING', 'Piercing'), ('CONJUNTO', 'Conjunto'), ]

tipo = models.CharField(max_length=10, choices=TIPO_CHOICES)
categoria = models.CharField(max_length=10, choices=CATEGORIA_CHOICES)

# --- Atributos Principais ---
nome = models.CharField(max_length=255)
sku = models.CharField("SKU", max_length=50, unique=True)
preco = models.DecimalField(max_digits=12, decimal_places=2)
material_principal = models.ForeignKey(Material, on_delete=models.PROTECT)

# --- Atributos Opcionais ---
designer = models.ForeignKey(Designer, on_delete=models.SET_NULL, null=True, blank=True)
gemas = models.ManyToManyField(Gema, blank=True)

def __str__(self):
    return f"{self.get_categoria_display()}: {self.nome} ({self.sku})"
Projeto Django, Repositório e Apresentação
As demais seções do plano (Projeto Django, Repositório GitHub e Apresentação em Slides) seguem a mesma estrutura, mas com o conteúdo atualizado para refletir: Apresentação: O "Problema" agora é a gestão de um catálogo diversificado. A "Solução" é um sistema capaz de lidar com essa complexidade. Demonstração: A interface da plataforma deve mostrar os novos filtros e campos para Tipo e Categoria de joia. Desafios: Um novo desafio é criar uma interface de usuário (UI) que seja intuitiva para cadastrar produtos com tantas variações.
