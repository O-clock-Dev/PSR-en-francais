> [PSR-0](./PSR-0.md) - [PSR-1](./PSR-1.md) - [PSR-3](./PSR-3.md) - **PSR-4** - [PSR-6](./PSR-6.md) - [PSR-7](./PSR-7.md) - [PSR-11](./PSR-11.md) - [PSR-12](./PSR-12.md) - [PSR-13](./PSR-13.md) - [PSR-14](./PSR-14.md) - [PSR-15](./PSR-15.md) - [PSR-16](./PSR-16.md) - [PSR-17](./PSR-0.md) - [PSR-17](./PSR-0.md) - [PSR-18](./PSR-18.md)
> Traduction française non-officielle de [_PSR-4: Autoloader_](https://www.php-fig.org/psr/psr-4/).

# PSR-4 : chargement automatique

_Les mots-clés "DOIT", "NE DOIT PAS", "REQUIÈRE", "DEVRA", "NE DEVRA PAS", "DEVRAIT", "NE DEVRAIT PAS", "RECOMMANDÉ", "PEUT" et "OPTIONNELLEMENT" [ainsi que leurs formes plurielles et négatives] dans ce document sont à interpréter au sens de la [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)._

## 1. En résumé

Cette section du standard PSR décrit une spécification concernant le chargement automatique (_autoloading_) de classes à partir de chemins de fichiers. Cette spécification est totalement interopérable, et peut donc être utilisée en complément de toute autre spécification de chargement automatique, y compris la PSR-0 [<abbr title="note de traduction">ndt</abbr>: dépréciée depuis]. La PSR-4 décrit également où placer les fichiers qui seront chargés automatiquement conformément à la spécification.

## 2. Spécification

1. Le terme « classe » désigne toute classe, interface, trait ou structure similaire.
2. Le nom complet (« pleinement qualifié », _fully qualified_) d’une classe a la forme `\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>`, de sorte que :
    1. le nom complet de la classe DOIT appartenir à un espace de nommage de niveau racine, aussi appelé _vendor namespace_ ;
    2. le nom complet de la classe PEUT appartenir à un ou plusieurs sous-espaces de nommage ;
    3. le nom complet de la classe DOIT se terminer par le nom de la classe elle-même ;
    4. le caractère underscore (`_`) n’a aucun sens particulier lorsqu’utilisé au sein du nom complet de la classe ;
    5. les caractères alphabétiques PEUVENT être librement combinés dans leur version majuscule et minuscule au sein du nom complet de la classe ;
    6. tout nom de classe DOIT ensuite être référencé en respectant la casse de la déclaration.
3. Lorsqu’un fichier correspondant à une nom complet de classe est chargé :
    1. il doit exister, dans le système de fichier, au moins un « dossier de base » dont le nom correspond exactement à une suite contiguë d’espaces de nommage (un ou plusieurs), autrement dit un espace de nommage « préfixe » car situé au début du nom complet de la classe, et ce en faisant abstraction du séparateur tout à gauche du préfixe ;
    2. la série contiguë de sous-espaces de nommage après le préfixe correspond à un sous-dossier d’un dossier de base, à l’intérieur duquel chaque séparateur présent dans le nom complet correspond à un nouveau niveau hiérarchique de sous-dossier. Le nommage des sous-dossiers DOIT respecter la casse des sous-espaces de nommage ;
    3. le nom final de la classe elle-même correspond à un fichier d’extension `.php`. Le nom du fichier DOIT respecter la casse du nom de la classe.
4. Les implémentations de ce mécanisme de chargement automatique NE DOIVENT PAS lancer d’exception, NE DOIVENT PAS déclencher d’erreur de quelque niveau que ce soit, et NE DEVRAIENT PAS retourner de valeur.

## 3. Exemples

Le tableau ci-dessous présente différents cas de figure, avec la mise en relation entre un chemin de fichier et le nom complet de classe, l’espace de nommage « préfixe » et le dossier de base.

| Nom complet de classe | Espace de nom. préfixe | Dossier de base | Chemin résultant |
|-----------------------|------------------------|-----------------|------------------|
| \Acme\Log\Writer\File_Writer | Acme\Log\Writer | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php |
| \Aura\Web\Response\Status | Aura\Web | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |
| \Symfony\Core\Request | Symfony\Core | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php |
| \Zend\Acl | Zend | /usr/includes/Zend/ | /usr/includes/Zend/Acl.php |

Pour des exemples d’implémentation de cette spécification de chargement automatique, veuillez consulter [ces fichiers](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md). Les exemples d’implémentation NE DOIVENT PAS être considérées comme faisant partie de la spécification et PEUVENT être modifiées à tout moment.
