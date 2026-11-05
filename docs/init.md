# Install
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Exec
# Cli
python ileapp.py -t <zip | tar | fs | gz> -i <path_to_extraction> -o <path_for_report_output>

# gui
python ileappGUI.py
python ileapp.py --help

# Compile
pyinstaller /scripts/pyinstaller/ileapp_macos.spec
pyinstaller /scripts/pyinstaller/ileappGUI_macos.spec




python aleapp.py -t <zip | tar | fs | gz> -i <path_to_extraction> -o <path_for_report_output>
python aleappGUI.py
python aleapp.py --help