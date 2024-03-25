# crypto_challenge

> [!CAUTION]
> A regarder seulement si vous avez des doutes ou que vous êtes bloqué !!!


__On vous donne cinq fichiers qui se trouvent dans /home/kali/examsecu/challenge :__
1.	cleFinale : (fichier binaire obtenu en chiffrant un texte avec openssl et la commande enc. L'algorithme de chiffrement symétrique est "aes256" en mode cbc. Ce fichier contient le mot de passe qui est à trouver comme objectif final. Il vous permettra de connaître le nombre de points liés à cette question.
2.	motDePasse.rsa : ce fichier contient un mot de passe qui est chiffré à partir de la clé symétrique en AES
3.	MaCleRSA.pem qui est la clé privée RSA qui a servi à chiffrer mdpRSA.rsa
4.	mdpBase64 : qui contient le mot de passe qui protège la clé RSA. Ce mot de mot est codé en Base 64.
5.	coffrefort.chiffre : qui contient ce que vous devez déchiffrer au final avec le mot de passe qui se trouve dans le fichier chiffré cleFinale

__Quelle est la taille de la clé RSA qui protège le mot de passe ?__
A voir

__Décoder mdpBase64 qui contient le mot de passe qui protège la clé MaCleRSA.pem__ 
openssl enc -d -base64 -in mdpBase64
*examRT2*

__Avec quel algorithme symétrique avons-nous chiffrer la clé privée MaCleRSA.pem ?__
*RSA*
openssl rsa -in MaCleRSA.pem (Pour voir le contenu de la clé)

__Dechiffrer motDePasse.rsa avec la clé privée MaCleRSA.pem ?__
openssl rsautl -decrypt -inkey MaCleRSA.pem -in motDePasse.rsa
*mdp2*
openssl rsautl -decrypt -inkey MaCleRSA.pem -in motDePasse.rsa -out mdprsa.txt (pour l'avoir directement dans un fichier)

__Grace au mot de passe trouvé à la question précédente, on vous demande de trouver le mot de passe caché dans le fichier cleFinale__
openssl enc -d -aes-256-cbc -in cleFinale -out cleDeciphered.txt -pass file:mdprsa.txt
cat cleDeciphered.txt 
*Hello, vous avez réussi le challange : le mot de passe du coffre fort est : Bonjour

__Enfin, déchiffrer le fichier coffrefort.chiffre__ 
openssl enc -d -aes-256-cbc -in coffrefort.chiffre -out coffrefort_dechiffre.txt -pass file:mdpcf.txt (fichier avec seulement *Bonjour*)
cat coffrefort_dechiffre.txt 
*Bravo, vous avez réussi et le nombre de points qui vous aurez pur avoir vancu ce challenge est de : 4 points*




