# Mettre à jour le schéma de la base
_Ex : m180206_174412_create_x_appnexus_thirdparty_pixels_table.php_
_Doc : https://github.com/tradelab/v2/wiki/%5BHowTo%5D-Generate-models-with-Gii-tool_
- Créer la table sur la base de dev
- Créer un script de migration à partir d'une table : yii migrate/create {type_de_modif}_{nom_table}_{suffixe} --appconfig=config/aau/console.php
- Compléter ce script avec le schéma de la table
- Exécuter le script de migration : yii migrate/up {nom_script_migration} --appconfig=config/aau/console.php
- Annuler n mises à jour de migration : yii migrate/down {nombre_annulations} --appconfig=config/aau/console.php
