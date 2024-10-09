Cette **blueprint** permet de relier un **clavier Zigbee2MQTT** (par exemple le Frient KEPZB-110) à un **panneau de contrôle d'alarme** (comme **Alarmo**) dans **Home Assistant**. Elle assure une synchronisation complète entre l'état du panneau d'alarme et le clavier, permettant ainsi de contrôler l'alarme directement depuis le clavier tout en reflétant les changements d'état effectués depuis Home Assistant.

## 🛠️ Fonctionnalités

- **Synchronisation bidirectionnelle** : Les changements d'état de l'alarme depuis le panneau de contrôle sont reflétés sur le clavier et vice versa.
- **Gestion de plusieurs codes PIN** : Autorise l'utilisation de plusieurs codes PIN pour armer ou désarmer le système d'alarme.
- **Gestion des erreurs** : Envoie des notifications en cas de saisie d'un code PIN invalide et réinitialise le clavier pour éviter le blocage.

## 📋 Configuration

### 📦 Prérequis

- **Home Assistant** installé et configuré.
- **Zigbee2MQTT** intégré à Home Assistant.
- **Alarmo** ou tout autre panneau de contrôle d'alarme compatible avec Home Assistant.
- Un **clavier Zigbee2MQTT** configuré et connecté.

### 🚀 Importation de la Blueprint

#### Automatiquement

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FHowmationFr%2FBlueprint-Sync-Clavier%2Fblob%2Fmain%2Fsync-clavier.yaml)

#### Manuellement

1. **Accéder aux Blueprints** :
   - Allez dans **Configuration** > **Automatisations & Scènes** > **Blueprints**.

2. **Importer la Blueprint** :
   - Cliquez sur **Importer Blueprint**.
   - Collez l'URL du dépôt GitHub où la blueprint est hébergée ou téléversez le fichier YAML directement.
   - Cliquez sur **Importer** pour finaliser l'importation.

### ⚙️ Configuration de l'Automatisation

1. **Créer une Nouvelle Automatisation** :
   - Allez dans **Configuration** > **Automatisations & Scènes** > **Automatisations**.
   - Cliquez sur **Créer une automatisation** > **Utiliser un blueprint**.
   - Sélectionnez **Synchronisation Clavier - Alarme par Howmation**.

2. **Configurer les Entrées** :

   - **Topic MQTT d'état du clavier Zigbee2MQTT** :
     - Exemple : `zigbee2mqtt/Clavier`
   
   - **Topic MQTT de commande du clavier Zigbee2MQTT** :
     - Exemple : `zigbee2mqtt/Clavier/set`
   
   - **Codes PIN** :
     - **Description** : Liste des codes PIN valides pour contrôler le système d'alarme.
     - **Format** : Entrez chaque code PIN sur une nouvelle ligne.
     - **Exemple** :
       ```
       1111
       5555
       8888
       ```
     - **Note** : Assurez-vous que chaque code PIN est correct et correspond à ceux configurés dans votre panneau d'alarme (Alarmo).
   
   - **Panneau de contrôle d'alarme** :
     - Sélectionnez votre entité Alarmo, par exemple `alarm_control_panel.maison`.

3. **Enregistrer l'Automatisation** :
   - Cliquez sur **Enregistrer** pour finaliser la configuration.

## ✅ Vérifications et Tests

1. **Tester les Codes PIN Valides** :
   - Utilisez chaque code PIN défini dans Alarmo depuis le clavier physique (par exemple, `1111` et `5555`).
   - Vérifiez que l'alarme s'arme ou se désarme correctement.
   - Assurez-vous que les LED et les sons du clavier reflètent l'état actuel de l'alarme.

2. **Tester un Code PIN Invalide** :
   - Utilisez un code PIN non valide (par exemple, `8888` si non configuré dans Alarmo).
   - Le clavier devrait recevoir une notification `invalid_code` et émettre un signal sonore ou visuel pour indiquer l'erreur.

3. **Vérifier la Synchronisation** :
   - Changez l'état de l'alarme depuis le panneau de contrôle et assurez-vous que le clavier reflète correctement cet état.
   - Testez à nouveau un code PIN valide après une tentative de code invalide pour vérifier que le clavier fonctionne correctement.

## 🐛 Dépannage

1. **Le clavier ne réagit plus** :
   - **Vérifiez les Logs** :
     - Accédez à **Configuration** > **Journaux** dans Home Assistant pour vérifier les erreurs liées à l'automatisation.
   - **Vérifiez les Messages MQTT** :
     - Utilisez un client MQTT (comme [MQTT Explorer](https://mqtt-explorer.com/)) pour surveiller les messages publiés et reçus sur les topics `mqtt_topic_etat_clavier` et `mqtt_topic_commande_clavier`.

2. **Les actions du clavier ne modifient pas l'état de l'alarme** :
   - **Confirmez les Codes PIN** :
     - Assurez-vous que le code PIN saisi correspond à l'un des codes définis dans la liste `code_pins`.
   - **Vérifiez les Permissions** :
     - Assurez-vous que Home Assistant a les permissions nécessaires pour publier sur les topics MQTT.
   - **Consultez les Logs** :
     - Recherchez des erreurs ou des avertissements liés à l'automatisation ou aux services MQTT.

3. **Les états ne sont pas synchronisés** :
   - **Vérifiez la Connectivité MQTT** :
     - Assurez-vous que Zigbee2MQTT est correctement connecté et fonctionne sans interruptions.
   - **Assurez-vous que les Topics sont Corrects** :
     - Vérifiez que les topics MQTT utilisés dans la blueprint correspondent exactement à ceux configurés dans Zigbee2MQTT.

## 📄 Licence

Ce projet est distribué sous licence **MIT**. Veuillez consulter le fichier [LICENSE](LICENSE) pour plus d'informations.

## 🔗 Ressources supplémentaires

- [Documentation Home Assistant](https://www.home-assistant.io/)
- [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
- [Alarmo - Panneau de contrôle d'alarme pour Home Assistant](https://github.com/nielsfaber/alarmo)

## ❓ Support
Si vous rencontrez des problèmes ou avez des questions supplémentaires, n'hésitez pas à ouvrir une issue sur le dépôt GitHub de la blueprint ou à rejoindre la communauté Home Assistant pour obtenir de l'aide.
