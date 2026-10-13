# projeto-do-calculo-de-fuma-a
 ele calcula a fumaça que voce emitio no dia 

informações sobre o projeto:
ele informa sobre a quantidade que voce emitio de fumaça no dia e mostra a  porcetagen adequada que voce mesmo coloca o limite

#meu projeto vai ser:
sistema de analise de dados

#meu projeto  
print("========================================")
print("      CALCULADORA DE EMISSAO DE CO2")
print("========================================")

limite_anual = 2500000
historico = []

while True:
    print("\nLimite anual: 2,5 toneladas de CO2")
    print("\n1 - Carro")
    print("2 - Barco")
    print("3 - Barco com carro")
    print("4 - Moto pequena")
    print("5 - Moto media")
    print("6 - Jet Ski 2 tempos")
    print("7 - Jet Ski 4 tempos")
    print("8 - Cigarro")
    print("9 - Lancha")
    print("10 - Ver historico")
    print("0 - Sair")

    opcao = input("\nDigite uma opcao: ").strip()

    if opcao == "0":
        print("Programa encerrado!")
        break

    if opcao == "10":
        print("\n========== HISTORICO ==========")

        if not historico:
            print("Nenhuma emissao registrada.")
        else:
            total = sum(valor for nome, valor in historico)

            for nome, valor in historico:
                print(nome, "-", round(valor, 2), "g de CO2")

            print("\nTotal:", round(total, 2), "g de CO2")
            print("Total em kg:", round(total / 1000, 3))
            print("Total em toneladas:", round(total / 1000000, 4))
            print(
                "Limite utilizado:",
                round(total / limite_anual * 100, 2),
                "%"
            )

            if total > limite_anual:
                print("ATENCAO: limite ultrapassado!")
            elif total / limite_anual >= 0.8:
                print("CUIDADO: perto do limite!")
            else:
                print("Dentro do limite.")

        input("\nPressione Enter para voltar ao menu...")
        continue

    veiculos = {
        "1": ("Carro", 160, "km"),
        "2": ("Barco", 19, "km"),
        "3": ("Barco com carro", 130, "km"),
        "4": ("Moto pequena", 70, "km"),
        "5": ("Moto media", 120, "km"),
        "6": ("Jet Ski 2 tempos", 5800, "horas"),
        "7": ("Jet Ski 4 tempos", 600, "horas"),
        "9": ("Lancha", 35000, "horas")
    }

    if opcao == "8":
        try:
            quantidade = int(input("Quantos cigarros? "))

            if quantidade < 0:
                print("Digite uma quantidade positiva.")
                continue

            co2 = quantidade * 1.5
            nome = "Cigarro"

        except ValueError:
            print("Digite um numero inteiro valido.")
            continue

    elif opcao in veiculos:
        nome, fator, unidade = veiculos[opcao]

        try:
            quantidade = float(
                input("Informe a quantidade em " + unidade + ": ")
                .replace(",", ".")
            )

            if quantidade < 0:
                print("A quantidade nao pode ser negativa.")
                continue

            co2 = quantidade * fator

        except ValueError:
            print("Valor invalido. Digite um numero.")
            continue

    else:
        print("Opcao invalida. Escolha de 0 a 10.")
        input("Pressione Enter para tentar novamente...")
        continue

    historico.append((nome, co2))

    total = sum(valor for nome, valor in historico)
    porcentagem = total / limite_anual * 100

    print("\n========== RESULTADO ==========")
    print("Atividade:", nome)
    print("CO2 calculado:", round(co2, 2), "gramas")
    print("Em kg:", round(co2 / 1000, 3))
    print("Em toneladas:", round(co2 / 1000000, 4))

    print("\n========== TOTAL ACUMULADO ==========")
    print("Total:", round(total, 2), "gramas de CO2")
    print("Limite anual: 2,5 toneladas")
    print("Limite utilizado:", round(porcentagem, 2), "%")

    if total > limite_anual:
        print("ATENCAO! LIMITE ULTRAPASSADO!")
    elif porcentagem >= 80:
        print("CUIDADO! Voce esta perto do limite.")
    else:
        print("DENTRO DO LIMITE!")

    input("\nPressione Enter para voltar ao menu...")
