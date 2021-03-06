# TokyoWesterns 2018 : mixed-cipher

**category** : crypto

**points** : 233

**solves** : 39

## write-up ( English version )

This challenge has both AES and RSA encryption involve

`decrypt` function is obviously a RSA oracle, which can give us the last byte of decrypted message

Use RSA LSB oracle attack to decrypt the RSA encrypted AES key given by `print_key`

But `print_flag` does not give us IV, we can't find the top 16 bytes of the flag 

For now, we only have `ti#n_ora#le_c9630b129769330c9498858830f306d9}`

`iv = long_to_bytes(random.getrandbits(BLOCK_SIZE*8), 16)`

iv in `aes_encrypt` is generated by `random.getrandbits`

In python2, `random.getrandbits` is implemented using mersenne-twister, which is not cryptographically secure pseudorandom number generator

Use https://github.com/kmyk/mersenne-twister-predictor this repo to predict the iv

`TWCTF{L#B_de#r#pti#n_ora#le_c9630b129769330c9498858830f306d9}`

## write-up ( 中文版 )

這題有 AES 又有 RSA

`decrypt` 這個函式很明顯的是一個 RSA oracle 可以幫我們解密並給我們最後一個 byte

所以我們就直接作 RSA LSB oracle attack 找回 `print_key` 的 AES key

但是 `print_flag` 給的 AES encrypted flag 沒有給 IV 沒辦法解回 flag 的前 16 bytes

目前只有 `ti#n_ora#le_c9630b129769330c9498858830f306d9}`

`iv = long_to_bytes(random.getrandbits(BLOCK_SIZE*8), 16)`

不過他的 IV 是用 `random.getrandbits` 產生的

在 python2 `random.getrandbits` 內部是用 mersenne-twister 實作的

mersenne-twister 並不是 cryptographically secure pseudorandom number generator

直接用 https://github.com/kmyk/mersenne-twister-predictor 這個就可以預測出 IV

`TWCTF{L#B_de#r#pti#n_ora#le_c9630b129769330c9498858830f306d9}`

# other write-ups and resources

