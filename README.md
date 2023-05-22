import pygame
import random

# Inicialização do Pygame
pygame.init()

# Dimensões da janela do jogo
largura = 800
altura = 600

# Cores
branco = (255, 255, 255)
preto = (0, 0, 0)

# Criação da janela do jogo
janela = pygame.display.set_mode((largura, altura))
pygame.display.set_caption("Jogo de Tiro")

# Criação do jogador
jogador_img = pygame.image.load("jogador.png")
jogador_largura = 50
jogador_altura = 50
jogador_x = largura // 2 - jogador_largura // 2
jogador_y = altura - jogador_altura - 10

def jogador(x, y):
    janela.blit(jogador_img, (x, y))

# Criação do inimigo
inimigo_img = pygame.image.load("inimigo.png")
inimigo_largura = 50
inimigo_altura = 50
inimigo_x = random.randint(0, largura - inimigo_largura)
inimigo_y = random.randint(50, 200)
inimigo_velocidade = 3

def inimigo(x, y):
    janela.blit(inimigo_img, (x, y))

# Loop principal do jogo
jogo_ativo = True
while jogo_ativo:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            jogo_ativo = False

    # Movimentação do jogador
    teclas = pygame.key.get_pressed()
    if teclas[pygame.K_LEFT]:
        jogador_x -= 5
    if teclas[pygame.K_RIGHT]:
        jogador_x += 5

    # Limitando o jogador à janela do jogo
    if jogador_x < 0:
        jogador_x = 0
    elif jogador_x > largura - jogador_largura:
        jogador_x = largura - jogador_largura

    # Movimentação do inimigo
    inimigo_x += inimigo_velocidade
    if inimigo_x <= 0 or inimigo_x >= largura - inimigo_largura:
        inimigo_velocidade *= -1
        inimigo_y += 50

    # Verificando colisão entre jogador e inimigo
    if jogador_x < inimigo_x + inimigo_largura and jogador_x + jogador_largura > inimigo_x and jogador_y < inimigo_y + inimigo_altura and jogador_y + jogador_altura > inimigo_y:
        jogo_ativo = False

    # Preenchendo a janela com a cor de fundo
    janela.fill(branco)

    # Desenhando o jogador e o inimigo na tela
    jogador(jogador_x, jogador_y)
    inimigo(inimigo_x, inimigo_y)

    # Atualizando a janela do jogo
    pygame.display.update()

# Encerrando o Pygame
pygame.quit()




