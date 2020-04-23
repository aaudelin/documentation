# Securité et gestion de certificats

## Generation d'un fichier pfx (appel de WS)
openssl pkcs12 -inkey key.pem -in cert.pem -export -out pfxName.pfx