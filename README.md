import random

cartas = [
    {
        "nome": "Dragão Branco de Olhos Azuis",
        "atributos": {"ataque": 3000, "defesa": 2500, "nivel": 8},
    },
    {
        "nome": "Mago Negro",
        "atributos": {"ataque": 2500, "defesa": 2100, "nivel": 7},
    },
    {
        "nome": "Exodia",
        "atributos": {"ataque": 9999, "defesa": 9999, "nivel": 10},
    },
    {
        "nome": "Kuriboh",
        "atributos": {"ataque": 300, "defesa": 200, "nivel": 1},
    },
    {
        "nome": "Cavaleiro do Caos",
        "atributos": {"ataque": 2300, "defesa": 1800, "nivel": 6},
    },
    {
        "nome": "Dragão Negro",
        "atributos": {"ataque": 2400, "defesa": 2100, "nivel": 7},
    },
    {
        "nome": "Gárgula",
        "atributos": {"ataque": 1800, "defesa": 1500, "nivel": 5},
    },
    {
        "nome": "Fênix",
        "atributos": {"ataque": 2800, "defesa": 2300, "nivel": 7},
    },
]

def criar_baralhos():
    deck = cartas.copy()
    random.shuffle(deck)
    meio = len(deck) // 2
    return deck[:meio], deck[meio:]

def exibir_carta(carta):
    print(f"🃏 Carta: {carta['nome']}")
    for atr, val in carta["atributos"].items():
        print(f"  - {atr.capitalize()}: {val}")

def jogar():
    baralho_jogador, baralho_maquina = criar_baralhos()
    turnos = 7
    turno_atual = 1

    print("🔮 Super Trunfo - Yu-Gi-Oh! (Turnos) 🔮\n")
    while turno_atual <= turnos and baralho_jogador and baralho_maquina:
        print(f"\n--- Turno {turno_atual} ---")
        carta_jogador = baralho_jogador.pop(0)
        carta_maquina = baralho_maquina.pop(0)

        print("Sua carta:")
        exibir_carta(carta_jogador)

        atributo = input("Escolha um atributo para competir (ataque, defesa, nivel): ").lower()
        if atributo not in carta_jogador["atributos"]:
            print("Atributo inválido, tente novamente.")
            # coloca as cartas de volta no baralho para repetir o turno
            baralho_jogador.insert(0, carta_jogador)
            baralho_maquina.insert(0, carta_maquina)
            continue

        val_jogador = carta_jogador["atributos"][atributo]
        val_maquina = carta_maquina["atributos"][atributo]

        print(f"\nCarta da máquina: {carta_maquina['nome']}")
        print(f"Atributo '{atributo}' da máquina: {val_maquina}")
        print(f"Seu atributo '{atributo}': {val_jogador}")

        if val_jogador > val_maquina:
            print("✅ Você venceu o turno!")
            baralho_jogador.append(carta_jogador)
            baralho_jogador.append(carta_maquina)
        elif val_jogador < val_maquina:
            print("❌ Você perdeu o turno.")
            baralho_maquina.append(carta_maquina)
            baralho_maquina.append(carta_jogador)
        else:
            print("⚖️ Empate! As cartas retornam para seus donos.")
            baralho_jogador.append(carta_jogador)
            baralho_maquina.append(carta_maquina)

        print(f"\nCartas que você tem: {len(baralho_jogador)}")
        print(f"Cartas que a máquina tem: {len(baralho_maquina)}")

        turno_atual += 1

    print("\n--- Fim do jogo ---")
    if len(baralho_jogador) > len(baralho_maquina):
        print("🎉 Parabéns! Você ganhou o jogo!")
    elif len(baralho_jogador) < len(baralho_maquina):
        print("😞 A máquina ganhou o jogo. Tente de novo!")
    else:
        print("🤝 Empate geral!")

if __name__ == "__main__":
    jogar()
