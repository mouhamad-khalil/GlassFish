![GlassFish Logo](/glassfish.png)
# GlassFish

___
## Plan
- La Definition du serveur 
- Historique
- La Fonctionalité
- Les Avantages
- L'installation
- Start/Stop/Restart du serveur
- Déploiement d'une application 
- La Configuration SSL/TLS

### Vous pouvez visiter aussi ma page github: https://mouhamad-khalil.github.io/GlassFish/
___
## La Definition: 
GlassFish est le nom du serveur d'applications Java qui permet aux développeurs de générer des technologies d'entreprise pratiques et évolutives, ainsi que des services supplémentaires pouvant être installés en fonction de leurs préférences.

Le GlassFish est un logiciel Libre sous licence GNU 
  - GPL (General Public License) 
  - CDDL (Common Development and Distribution License)
  
___
## Start/Stop/Restart du serveur 
Pour démarrer(Start) le GlassFish Server:

```asadmin start-domain non-domain```

Pour stopper(Stop) le GlassFish Server: 

```asadmin stop-domain nom-domain```

Pour redémarrer(Restart) le GlassFish Server:

```asadmin restart-domain nom-domain```

___
## Déploiement d'une application:
*Au moins un domaine GlassFish Server doit être démarré avant de déployer une application.*

#### Pour déployer une application en utilisant *la ligne de commande:*

```asadmin deploy nom-application```

Exemple: ``asadmin deploy sample-dir/hello.war``

#### Pour accéder à l'application hello en tapant l'URL suivante dans votre navigateur:

``
http://localhost:8080/hello
``

#### Pour lister les applications déployées:

```asadmin list-applications```

#### Pour annuler le déploiement d'une application:

```asadmin undeploy nom-application```

Exemple: ```asadmin undeploy hello```

### Déploiement d'une application à l'aide de *la console d'administration:*

1. Lancez la console d'administration en tapant l'URL suivante dans votre navigateur.

   ``http://localhost:4848``
2. Cliquez sur le nœud "Applications" dans l'arborescence sur la gauche.
3. Cliquez sur le boutton "Deploy".
4. Sélectionnez "Packaged File to Be Uploaded to the Server", puis cliquez sur "Browse".
5. Accédez à l'emplacement dans lequel vous avez enregistré l'application, sélectionnez le fichier et cliquez sur Ouvrir.
6. Spécifiez une description dans le champ Description.
7. Acceptez les autres paramètres par défaut et cliquez sur OK.
8. Cochez la case en regard de l'application et cliquez sur le lien "Launch" pour lancer l'application.

  *L'URL par défaut de l'application est:``localhost:8080:hello``*

#### Pour afficher les applications déployées dans la console d'administration:
1. Lancez la console d'administration en tapant l'URL suivante dans votre navigateur.

   ``http://localhost:4848``
2. Cliquez sur le nœud "Applications" dans l'arborescence sur la gauche.

#### Pour annuler le déploiement d'une application à l'aide de la console d'administration:
1. Lancez la console d'administration en tapant l'URL suivante dans votre navigateur.

   ``http://localhost:4848``
2. Cliquez sur le nœud "Applications" dans l'arborescence sur la gauche.
3. Cochez la case en regard de l'application que vous voulez annuler 
4. Supprimer ou désactiver l'application:
    - Pour supprimer l'application, cliquez sur le bouton "Undeploy".
    - Pour désactiver l'application, cliquez sur le bouton "Disable".

## Configuration SSL/TLS:
***Il faut générer un certificat à l'aide de keytool***

1. Accédez au répertoire contenant les fichiers keystore et truststore.
>  Générez toujours le certificat dans le répertoire contenant les fichiers keystore et truststore. La valeur par défaut est domain-dir / config.
2. Générez le certificat dans le fichier keystore, keystore.jks:
```
keytool -genkey -alias keyAlias 
 -keyalg RSA
 -keypass changeit
 -storepass changeit
 -keystore keystore.jks
```
> Utilisez un nom unique comme votre keyAlias. Si vous avez modifié le mot de passe du fichier de clés ou de la clé privée par    défaut (changeit), remplacez le nouveau mot de passe par changeit. L'alias de mot de passe par défaut est s1as.
>Une invite s'affiche pour vous demander votre nom, votre organisation et d'autres informations.
3. Exportez le certificat généré dans le fichier server.cer, en utilisant le format de commande suivant:
```
keytool -export -alias keyAlias
 -storepass changeit
 -file server.cer
 -keystore keystore.jks
```
4. Créez le fichier truststore cacerts.jks et ajoutez le certificat au fichier de clés certifiées, en utilisant le format de commande suivant:
```
keytool -import -v -trustcacerts
 -alias keyAlias
 -file server.cer
 -keystore cacerts.jks
 -keypass changeit
```
>Les informations sur le certificat sont affichées et une invite vous demande si vous souhaitez approuver le certificat.
5. Tapez yes, puis appuyez sur "Enter".
>Des informations similaires aux suivantes sont affichées:
  ```
Certificate was added to keystore
[Saving cacerts.jks]
  ```
6. Pour appliquer vos modifications, redémarrez le Serveur.
7. Pour accéder à l'application hello en tapant l'URL suivante dans votre navigateur:
``
https://localhost:8181/hello
``
