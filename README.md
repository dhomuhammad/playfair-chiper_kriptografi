# playfair-chiper-kriptografi

NAMA : RIDHA MUHAMMAD RIFQI

KELAS : TI.22.A.5

NIM : 312210491

```

# prompt: Lakukan enkripsi dan dekrip Playfair Cihper pada plaintext:
# GOOD BROOM SWEEP CLEAN
# REDWOOD NATIONAL STATE PARK
# JUNK FOOD AND HEALTH PROBLEMS
# Dengan kunci “TEKNIK INFORMATIKA”

def prepare_text(text):
    """
    Mengubah teks menjadi huruf kapital, menghapus spasi, dan mengganti 'J' dengan 'I'.
    """
    text = text.upper().replace(" ", "")
    text = text.replace("J", "I")
    return text


def create_matrix(key):
    """
    Membuat matriks Playfair dari kunci.
    """
    key = prepare_text(key)
    matrix = []
    for char in key:
        if char not in matrix:
            matrix.append(char)
    for char in "ABCDEFGHIKLMNOPQRSTUVWXYZ":
        if char not in matrix:
            matrix.append(char)
    matrix = [matrix[i:i + 5] for i in range(0, 25, 5)]
    return matrix


def find_position(matrix, char):
    """
    Mencari posisi karakter dalam matriks.
    """
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == char:
                return i, j


def encrypt(plaintext, key):
    """
    Melakukan enkripsi Playfair Cipher.
    """
    plaintext = prepare_text(plaintext)
    matrix = create_matrix(key)
    ciphertext = ""
    i = 0
    while i < len(plaintext):
        char1 = plaintext[i]
        if i + 1 < len(plaintext):
            char2 = plaintext[i + 1]
        else:
            char2 = "X"
        if char1 == char2:
            char2 = "X"
            i += 1
        row1, col1 = find_position(matrix, char1)
        row2, col2 = find_position(matrix, char2)
        if row1 == row2:
            ciphertext += matrix[row1][(col1 + 1) % 5]
            ciphertext += matrix[row2][(col2 + 1) % 5]
        elif col1 == col2:
            ciphertext += matrix[(row1 + 1) % 5][col1]
            ciphertext += matrix[(row2 + 1) % 5][col2]
        else:
            ciphertext += matrix[row1][col2]
            ciphertext += matrix[row2][col1]
        i += 2
    return ciphertext


def decrypt(ciphertext, key):
    """
    Melakukan dekripsi Playfair Cipher.
    """
    ciphertext = prepare_text(ciphertext)
    matrix = create_matrix(key)
    plaintext = ""
    i = 0
    while i < len(ciphertext):
        char1 = ciphertext[i]
        char2 = ciphertext[i + 1]
        row1, col1 = find_position(matrix, char1)
        row2, col2 = find_position(matrix, char2)
        if row1 == row2:
            plaintext += matrix[row1][(col1 - 1) % 5]
            plaintext += matrix[row2][(col2 - 1) % 5]
        elif col1 == col2:
            plaintext += matrix[(row1 - 1) % 5][col1]
            plaintext += matrix[(row2 - 1) % 5][col2]
        else:
            plaintext += matrix[row1][col2]
            plaintext += matrix[row2][col1]
        i += 2
    return plaintext


key = "TEKNIK INFORMATIKA"
plaintext1 = "GOOD BROOM SWEEP CLEAN"
plaintext2 = "REDWOOD NATIONAL STATE PARK"
plaintext3 = "JUNK FOOD AND HEALTH PROBLEMS"

ciphertext1 = encrypt(plaintext1, key)
ciphertext2 = encrypt(plaintext2, key)
ciphertext3 = encrypt(plaintext3, key)

decrypted1 = decrypt(ciphertext1, key)
decrypted2 = decrypt(ciphertext2, key)
decrypted3 = decrypt(ciphertext3, key)

print("Plaintext 1:", plaintext1)
print("Ciphertext 1:", ciphertext1)
print("Decrypted 1:", decrypted1)
print("\nPlaintext 2:", plaintext2)
print("Ciphertext 2:", ciphertext2)
print("Decrypted 2:", decrypted2)
print("\nPlaintext 3:", plaintext3)
print("Ciphertext 3:", ciphertext3)
print("Decrypted 3:", decrypted3)

```



![Screenshot 2024-10-16 153117](https://github.com/user-attachments/assets/5b676651-a4ac-4b0e-b2fc-ddbce1559d26)



