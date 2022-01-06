> Traduction française non-officielle de [PSR-1: Basic Coding Standard](https://www.php-fig.org/psr/psr-1/).

# Standard minimal pour la programmation PHP

Cette section du standard PSR présente ce qui devrait être considéré comme les éléments fondamentaux requis pour la programmation PHP, afin d’assurer un haut niveau d’interopérabilité entre scripts PHP.

Les mots-clés "DOIT", "NE DOIT PAS", "REQUIÈRE", "DEVRA", "NE DEVRA PAS", "DEVRAIT", "NE DEVRAIT PAS", "RECOMMANDÉ", "PEUT" et "OPTIONNELLEMENT" [ainsi que leurs formes plurielles et négatives] dans ce document sont à interpréter au sens de la [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## 1. Présentation

- Les fichiers DOIVENT uniquement utiliser les tags `<?php` ou `<?=`.
- Les fichiers DOIVENT uniquement utiliser un encodage UTF-8, sans BOM, en présence de code PHP.
- Les fichiers PEUVENT soit déclarer des symboles (classes, fonctions, constantes, etc.), _soit_ déclencher des effets de bord (par exemple, générer du contenu, changer des paramètres .ini, etc.), mais ils NE DEVRAIENT PAS faire les deux à la fois.
- Les espaces de noms (_namespaces_) et les classes DOIVENT se conformer à un standard PSR de chargement automatique (_autoloading_) : [[PSR-0](./PSR-0.md), [PSR-4](./PSR-4.md)].
- Les noms de classes DOIVENT être déclarés en `CamelCase`.
- Les constantes de classe DOIVENT être déclarées en majuscule avec des underscore (`_`) en tant que séparateurs.
- Les noms des méthodes DOIVENT être déclarées en camelCase.

## 2. Les fichiers

### 2.1 Balises PHP

Le code PHP DOIT utiliser les balises ouvrantes/fermantes soit en version longue `<?php ?>` _soit_ en version courte `<?= ?>` ; le code PHP ne DOIT PAS utiliser d’autres versions.

### 2.2 Encodage des caractères

Le code PHP DOIT uniquement utiliser l’encodage UTF-8, sans BOM.

### 2.3 Effets de bord

Un fichier contenant du code PHP DEVRAIT _soit_ déclarer de nouveaux symboles (classes, fonctions, constantes, etc.) et ne pas causer d’effets de bord, _soit_ exécuter de la logique à effets de bord, mais ne DEVRAIT PAS faire les deux à la fois.

L’expression « effet de bord » fait référence à l’exécution de toute logique non directement liée à la déclaration de nouvelles classes, fonctions, constantes, etc. et en excluant la simple inclusion du fichier dans un autre.

Les « effets de bord » inclus, mais ne sont pas limités à : la génération de contenu/sortie, l’utilisation explicite de `require` ou `include`, la connexion à des services tiers, la modification de paramètres .ini, l’émission d’erreur ou d’exceptions, la modification de variables globales ou statiques, les opérations de lecture ou d’écriture sur un fichier, etc.

L’exemple ci-dessous montre ce qu’il faut éviter, à savoir un mélange de déclarations et d’effets de bord :

``` php
<?php
// effet de bord : modification d’un paramètre .ini
ini_set('error_reporting', E_ALL);

// effet de bord : chargement d’un fichier
include "file.php";

// effet de bord : génération de contenu en sortie
echo "<html>\n";

// déclaration
function foo()
{
    // corps de la fonction
}
```

L’exemple ci-dessous montre ce qu’il faut privilégier, à savoir un fichier avec des déclarations mais pas d’effets de bord :

``` php
<?php
// déclaration
function foo()
{
    // corps de la fonction
}

// une logique conditionnelle est une déclaration, pas un effet de bord
if (! function_exists('bar')) {
    function bar()
    {
        // corps de la fonction
    }
}
```

