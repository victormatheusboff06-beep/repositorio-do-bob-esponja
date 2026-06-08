from ursina import *
from ursina.prefabs.first_person_controller import FirstPersonController

# 1. Inicializar o jogo
app = Ursina()

# 2. Definir texturas básicas (usando cores sólidas para simplificar)
textura_grama = color.green
textura_terra = color.brown

# 3. Definir a classe do Bloco (Voxel)
class Voxel(Button):
    def __init__(self, position=(0,0,0), texture=textura_grama):
        super().__init__(
            parent=scene,
            position=position,
            model='cube',
            origin_y=0.5,
            texture=texture,
            color=color.color(0, 0, random.uniform(0.9, 1.0)), # Pequena variação de tom
            highlight_color=color.lime,
        )

    # Lógica para colocar ou quebrar blocos ao clicar
    def input(self, key):
        if self.hovered:
            if key == 'left mouse down':  # Botão esquerdo: Cria bloco
                voxel = Voxel(position=self.position + mouse.normal, texture=textura_terra)
            if key == 'right mouse down': # Botão direito: Destrói bloco
                destroy(self)

# 4. Gerar o mundo (um mapa plano de 20x20 blocos)
for z in range(20):
    for x in range(20):
        voxel = Voxel(position=(x, 0, z))

# 5. Adicionar o jogador (Câmera em primeira pessoa)
player = FirstPersonController()

# Remover o botão padrão do mouse na tela
mouse.visible = False

# Executar a aplicação
app.run()
