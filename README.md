# Hello World no ESP32 com ESP-IDF

Atividade em equipe com o objetivo de compilar, gravar e executar o exemplo `hello_world` em uma placa ESP32, usando o framework oficial ESP-IDF.

## Equipe
- Antônio Cruz
- Lucas de Lima
- João Otávio
- Fransisco Williann

## Sobre o projeto

O ESP32 é um microcontrolador de baixo custo, com processador dual-core e conectividade Wi-Fi e Bluetooth integradas, muito usado em projetos de IoT e automação.

O ESP-IDF (Espressif IoT Development Framework) é o framework oficial da Espressif para programar o ESP32. Ele é baseado no FreeRTOS e disponibiliza toda a cadeia de ferramentas (toolchain, build system, gravação e monitoramento serial) através de uma única interface de linha de comando, o `idf.py`.

## Pré-requisitos

- Placa ESP32 e cabo USB com pinos de dados (não apenas de carga)
- Driver USB-serial instalado (CP210x ou CH340, dependendo do chip da placa)
- Git instalado
- Python 3 instalado

## Instalação do ESP-IDF

```powershell
mkdir ~\esp
cd ~\esp
git clone https://github.com/FCI-Code/IOT.git
cd esp-idf
.\install.ps1 esp32
```

## Ativando o ambiente

Toda vez que abrir um terminal novo, é necessário ativar o ambiente do ESP-IDF:

```powershell
. $HOME\esp\esp-idf\export.ps1
```

Esse passo ativa um ambiente virtual Python (`venv`) usado internamente pelas ferramentas do IDF e adiciona o `idf.py` ao PATH.

## Copiando o projeto de exemplo

```powershell
cp -r $env:IDF_PATH\examples\get-started\hello_world ~\esp\hello_world
cd ~\esp\hello_world
```

## Fluxo de compilação e execução

| Passo | Comando | O que faz |
|---|---|---|
| 1 | `idf.py set-target esp32` | Define o chip alvo da compilação |
| 2 | `idf.py build` | Compila o projeto e gera o binário |
| 3 | `idf.py -p COM3 flash monitor` | Grava o binário na placa via USB e abre a leitura serial |

Troque `COM3` pela porta correspondente à sua placa. Para identificar a porta no Windows:

```powershell
Get-PnpDevice -Class Ports -PresentOnly | Select-Object Name, Status
```

Para sair do monitor serial: `Ctrl+]`



## Resultado esperado

Após o flash, o monitor deve exibir algo como:

```
Hello world!
This is esp32 chip with 2 CPU core(s)...
Restarting in 10 seconds...
```
