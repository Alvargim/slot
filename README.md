# slot
crear una maquina slot de 5 rieles en pygame
import pygame
import random

# Define las figuras
figuras = ["bar", "cherry", "lemon", "seven", "bell", "joker"]

# Define las apuestas
apuestas = [1, 2, 5, 10]

# Define el contador de premios
premios = 0

# Inicializa Pygame
pygame.init()

# Crea la ventana del juego
pantalla = pygame.display.set_mode((400, 600))

# Carga las imágenes de las figuras
imagenes = {}
for figura in figuras:
    imagenes[figura] = pygame.image.load(f"{figura}.png")

# Define las combinaciones ganadoras
combinaciones = [
    ("bar", "bar", "bar"),
    ("cherry", "cherry", "cherry"),
    ("lemon", "lemon", "lemon"),
    ("seven", "seven", "seven"),
    ("bell", "bell", "bell"),
    ("joker", "joker", "joker"),
]

# Define la variable apuesta
apuesta = 1

# Bucle principal del juego
while True:
    # Actualiza la pantalla
    pantalla.fill((0, 0, 0))

    # Dibuja los rieles
    for i in range(4):
        pygame.draw.rect(pantalla, (255, 0, 0), (100 + i * 100, 100, 100, 100))
        imagen = imagenes[random.choice(figuras)]
        pantalla.blit(imagen, (100 + i * 100, 100))

    # Detecta las pulsaciones de tecla
    for evento in pygame.event.get():
        if evento.type == pygame.KEYDOWN and evento.key == pygame.K_a:
            # Gira los rieles
            for i in range(4):
                imagen = imagenes[random.choice(figuras)]
                pantalla.blit(imagen, (100 + i * 100, 100))

            # Calcula las combinaciones ganadoras
            for combinacion in combinaciones:
                if combinacion in [imagen.filename for imagen in imagenes.values()]:
                    premios += apuestas[apuesta]

    # Dibuja el contador de premios
    pygame.draw.rect(pantalla, (255, 255, 255), (100, 500, 200, 50))
    pygame.draw.rect(pantalla, (0, 0, 0), (100, 500, 200, 50), 2)
    pygame.draw.text(pantalla, str(premios), (150, 525), (255, 255, 255), 20)

    # Actualiza la pantalla
    pygame.display.update()

