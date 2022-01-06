> Traduction française non-officielle de [PSR-1: Basic Coding Standard](https://www.php-fig.org/psr/psr-1/).

# Standard minimal pour la programmation PHP

Cette section du standard PSR présente ce qui devrait être considéré comme les éléments fondamentaux requis pour la programmation PHP, afin d’assurer un haut niveau d’interopérabilité entre scripts PHP.

Les mots-clés "DOIT", "NE DOIT PAS", "REQUIÈRE", "DEVRA", "NE DEVRA PAS", "DEVRAIT", "NE DEVRAIT PAS", "RECOMMANDÉ", "PEUT" et "OPTIONNELLEMENT" [ainsi que leurs formes plurielles et négatives] dans ce document sont à interpréter au sens de la [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## Présentation

- Les fichiers DOIVENT utiliser uniquement les tags `<?php` ou `<?=`.
- Les fichiers DOIVENT utiliser uniquement un encodage UTF-8, sans BOM, en présence de code PHP.
- Les fichiers PEUVENT soit déclarer des symboles (classes, fonctions, constantes, etc.), _soit_ déclencher des effets de bord (par exemple, générer du contenu, changer des paramètres .ini, etc.), mais ils NE DEVRAIENT PAS faire les deux à la fois.
- Les espaces de noms (_namespaces_) et les classes DOIVENT se conformer à un standard PSR de chargement automatique (_autoloading_) : [[PSR-0](./PSR-0.md), [PSR-4](./PSR-4.md)].
- Les noms de classes DOIVENT être déclarés en `CamelCase`.
- Les constantes de classe DOIVENT être déclarées en majuscule avec des underscore (`_`) en tant que séparateurs.
- Les noms des méthodes DOIVENT être déclarées en camelCase.
