def vigenere_encrypt(plain_text, key):
    encrypted_text = ''
    key_length = len(key)
    
    for i in range(len(plain_text)):
        char = plain_text[i]
        key_char = key[i % key_length]
        
        if char.isalpha():
            shift = ord(key_char.lower()) - ord('a')
            if char.isupper():
                encrypted_char = chr(((ord(char) - ord('A') + shift) % 26) + ord('A'))
            else:
                encrypted_char = chr(((ord(char) - ord('a') + shift) % 26) + ord('a'))
        else:
            encrypted_char = char
        
        encrypted_text += encrypted_char
    
    return encrypted_text

def vigenere_decrypt(encrypted_text, key):
    decrypted_text = ''
    key_length = len(key)
    
    for i in range(len(encrypted_text)):
        char = encrypted_text[i]
        key_char = key[i % key_length]
        
        if char.isalpha():
            shift = ord(key_char.lower()) - ord('a')
            if char.isupper():
                decrypted_char = chr(((ord(char) - ord('A') - shift + 26) % 26) + ord('A'))
            else:
                decrypted_char = chr(((ord(char) - ord('a') - shift + 26) % 26) + ord('a'))
        else:
            decrypted_char = char
        
        decrypted_text += decrypted_char
    
    return decrypted_text

# Contoh penggunaan
key = "SECRETKEY"
username = "Alice"
password = "Password123"

# Enkripsi username dan password sebelum menyimpannya
encrypted_username = vigenere_encrypt(username, key)
encrypted_password = vigenere_encrypt(password, key)

# Simpan encrypted_username dan encrypted_password di database

# Saat login, dekripsi username dan password yang diinputkan
input_username = input("Masukkan username: ")
input_password = input("Masukkan password: ")

decrypted_username = vigenere_decrypt(encrypted_username, key)
decrypted_password = vigenere_decrypt(encrypted_password, key)

if input_username == decrypted_username and input_password == decrypted_password:
    print("Login berhasil!")
else:
    print("Login gagal!")

