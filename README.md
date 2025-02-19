# Rapport : Projet Final AWS 

Date : 19/02/2025 

Crée par : KADI Soulaymane, HOMBOURGER Tomy, BERNARD Jonathan, AHMADI Rateb et FIGAROLI Romain




# Partie 1 : Configuration sur AWS 

## Création du VPC : 
![image](https://github.com/user-attachments/assets/bb9d68e6-f875-49fe-99aa-d2fe516e7272)


## Création de la base de données : 
![image](https://github.com/user-attachments/assets/a15bdc78-1419-4ea7-87b9-795f48ee5b3c)


## Création de l'instance EC2
![image](https://github.com/user-attachments/assets/1575cd57-e7c2-44bc-8091-3cf3b9ff71f3)
![image](https://github.com/user-attachments/assets/0db8aea7-2b88-4124-957d-2d2b105d7dbf)
![image](https://github.com/user-attachments/assets/0d024bc8-1a18-49bc-95aa-f5f04ed6b9bd)

### Cloudinit à mettre dans la création de l'instance EC2
```
#!/bin/bash  
sudo apt update -y && sudo apt upgrade -y  
sudo apt install -y docker.io git default-mysql-client  
sudo systemctl start docker  
sudo systemctl enable docker  

sudo usermod -aG docker ubuntu  

git clone https://github.com/app-generator/flask-datta-able.git  

cd flask-datta-able  

docker build -t flask-datta-able . 

docker run -d -p 5085:5085 --name flask-app flask-datta-able
```
![image](https://github.com/user-attachments/assets/2b41ff51-3f0e-4b95-a8c7-bf4d5ac93e13)



# Partie 2 : Configuration sur la VM 

### Connexion en SSH sur le VM grâce à la clé généré 

![image](https://github.com/user-attachments/assets/b699835e-d7e0-495b-b906-1919c41530d9)
![image](https://github.com/user-attachments/assets/c77094ca-8d38-47d6-bba2-5c63c8263507)


### Modification du fichier .env pour établir la connexion avec la base de donnée

![image](https://github.com/user-attachments/assets/6e3c4b2b-378d-4651-80ef-6f9e8e325050)


### Pull de l'image grâce à la commande : 
```docker-compose up -d```
![image](https://github.com/user-attachments/assets/b81c0db5-29b9-4e83-8417-123cbc8133c9)


### Vérification de l'image grâce à la commande : 
```docker ps```

![image](https://github.com/user-attachments/assets/86041d11-767d-4f91-9d17-7a78d96cf3ac)

### Vérification de l'accès à l'application grâce à la commande curl et avec l'interface web

![commane curl](https://github.com/user-attachments/assets/79170b9d-bafa-4c87-8692-f758134c8b7c)
![interface web](https://github.com/user-attachments/assets/9e2fd872-b2c8-4248-a1f6-b8b648bc3063)

# Partie 3 : Modification du virtual env pour connecter la DB et l'application

### Mettre à jour le config.py ;:

![image](https://github.com/user-attachments/assets/c6b27351-513f-489f-9d3e-7299c8649111)

### Création et activation d'un environnement virtuel Python : 

```
bash 
CopierModifier 
python3 -m venv venv 
source venv/bin/activate 
```
![image](https://github.com/user-attachments/assets/e5d6e57b-1c74-4ddf-95d3-45fdf2b861f4)

### Modifier requirement.txt pour ajouter pymysql :
![image](https://github.com/user-attachments/assets/0fb4ca54-209a-4759-b930-3462b92d5361)

Ensuite lancer la commande : 
```
pip install -r requirements.txt
```

### À cause des erreurs d’environnement on a dû installer :  

```
pip install flask-migrate 
```

### Mettre à jour pip, setuptools et wheel  

Cette commande : 
```pip install --upgrade pip setuptools wheel ``` 

remplace : python3-distutils qui est requit pour la migration 

nous  avons eu des erreurs car la python3-distutils n’était pas reconnu 

### Connexion de la DB et l'application
![image](https://github.com/user-attachments/assets/c5f2bbf7-c815-41f8-b087-4fa1ffce2335)
![image](https://github.com/user-attachments/assets/1d31abd6-1349-4b59-92a5-24162bd2f23c)
![image](https://github.com/user-attachments/assets/2d782320-5e33-4683-a40e-f7b2fdc9e683)

### Connexion à la DB et vérification des tâbles

![image](https://github.com/user-attachments/assets/db936769-8bb1-4b00-8080-5b6f8f833f5b)
![image](https://github.com/user-attachments/assets/8b1713ce-a8a5-4602-ac0b-dfae13062031)

# Partie 4 : Test de la connexion entre la DB et l'application

### Création d'un compte utilisateur sur l'interface web 

![image](https://github.com/user-attachments/assets/e37c8da1-7b04-4a70-9b20-cf51687dc182)

### Vérification de l'utilisateur crée en amont dans la DB

![image](https://github.com/user-attachments/assets/836dfe09-d5d8-42f3-994b-e5125f593b47)


# Partie 5 : Création du bucket S3

### Création du bucket S3
![image](https://github.com/user-attachments/assets/7ca8a8dd-77e8-4c5c-92bb-464d8bcb1ab3)

### Activation de l’hébergement de site web Statique  
![image](https://github.com/user-attachments/assets/21abe861-275a-48c7-a724-caf2a812bdd5)

###  Autorisation de l’accès au public  
![image](https://github.com/user-attachments/assets/dc94255d-bf5a-48dd-a3bc-b690d4d9ad6f)

### Installation de la dépendance ZIP
![image](https://github.com/user-attachments/assets/11a91f94-5681-44d5-b6d9-dac70cd949c9)

### ZIP de l’application flask-datta-able 
![image](https://github.com/user-attachments/assets/bee48548-c5fd-4fc1-a463-ff6bfbe4974d)

### Sauvegarde de la base de données en format SQL  
![image](https://github.com/user-attachments/assets/e9a1fa6f-142e-4ec3-8119-5b5f099fedb6)

### Sauvegarde de l’application et de la base donnée 
![image](https://github.com/user-attachments/assets/d50328b3-6434-4e84-b479-e3de271603d4)

### Configuration de GIT pour importer notre projet et le télécharger en .zip
![image](https://github.com/user-attachments/assets/8395fba8-4b79-4c28-ad0f-989c46aa246b)
![image](https://github.com/user-attachments/assets/cf2c6f18-78d1-481e-8eda-7b381eccfc34)

### Ajouter l'URL du dépôt distant :  
![image](https://github.com/user-attachments/assets/0008be3a-6904-4c67-925b-08a02d2ba655)

### Initialiser le dépôt :  
![image](https://github.com/user-attachments/assets/49417294-3e50-449e-9464-c573e8dc8ff2)

### Ajouter les fichiers modifiés : 
![image](https://github.com/user-attachments/assets/f3bffbbd-cf9a-4312-baa5-acdc8ecc0362)

### Créer un commit :  
![image](https://github.com/user-attachments/assets/679044e0-b3c1-4afe-8160-7c6f8eb7500b)

### Mettre branch main en principal :  
![image](https://github.com/user-attachments/assets/037132f2-0b1e-4254-b4ed-93fd7f493c82)

### Push les changements 
![image](https://github.com/user-attachments/assets/92789df9-8e60-4470-ab83-0508fdb61510)
![image](https://github.com/user-attachments/assets/2b5fb217-fc42-4313-8e56-22f9603a7108)

### Envoie du backup de l’application et de la base de donnée vers le bucket S3  
![image](https://github.com/user-attachments/assets/e4f2e64c-8aae-49d8-9e4e-79a2c9dbcff9)


# Partie 6 : Serveur de test

![image](https://github.com/user-attachments/assets/cbf6036a-5e0a-4f55-a005-5878425087f4)
![image](https://github.com/user-attachments/assets/999f539f-8630-448e-8b26-7f7b384f7114)




