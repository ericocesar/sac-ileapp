# Install (Python 3.11 a 3.15)
python3 -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt

# O venv guarda caminhos absolutos: activate e os shebangs de venv/bin apontam
# para a pasta onde ele foi criado. Se o repositorio for movido, recrie o venv
# (rm -rf venv) antes de usar de novo, senao pip falha com "bad interpreter".

## A GUI precisa de Tk
python3 -c "import tkinter"     # precisa responder, senao a GUI nao abre

# macOS: o Homebrew python@3.14 (/opt/homebrew/bin/python3) NAO traz _tkinter,
# e a GUI falha com ModuleNotFoundError: _tkinter. Use o instalador do python.org
# (https://www.python.org/downloads/mac-osx/), que ja vem com Tcl/Tk, ou o
# Homebrew python@3.12, que tambem ja vem:
#   /opt/homebrew/opt/python@3.12/bin/python3.12 -m venv venv
# Para-arrancar o 3.14 com Tk:
#   brew install tcl-tk && brew reinstall python@3.14
#
# Linux:
#   sudo apt-get install python3-tk

# Exec
# Cli: -t aceita fs, tar, zip, gz, itunes, file, raw
# A pasta de output precisa existir antes de rodar.
python ileapp.py -t <fs | tar | zip | gz | itunes | file | raw> -i <path_to_extraction> -o <path_for_report_output>
python ileapp.py --help

# gui
python ileappGUI.py

# Compile
# Um driver, um spec (packaging/ileapp.spec) e UM executavel, `ileapp`: sem
# argumento ele abre a janela, com argumento e a CLI. Nao existe spec separado
# para a GUI, e os specs antigos em scripts/pyinstaller/ nao existem mais.
python packaging/build.py exe                # dist/iLEAPP/ (e dist/iLEAPP.app no macOS)
python packaging/build.py exe --onefile      # dist/ileapp, um arquivo so
python packaging/build.py smoke              # roda o que a fase 1 construiu, sem abrir janela
python packaging/build.py installer          # .exe (Windows), .dmg (macOS), .AppImage (Linux)
python packaging/build.py all                # as duas fases, sem assinatura
python packaging/build.py verify <path>      # confere a assinatura
