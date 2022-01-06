> [PSR-0](./PSR-0.md) - **PSR-1** - [PSR-3](./PSR-3.md) - [PSR-4](./PSR-4.md) - [PSR-6](./PSR-6.md) - [PSR-7](./PSR-7.md) - [PSR-11](./PSR-11.md) - [PSR-12](./PSR-12.md) - [PSR-13](./PSR-13.md) - [PSR-14](./PSR-14.md) - [PSR-15](./PSR-15.md) - [PSR-16](./PSR-16.md) - [PSR-17](./PSR-0.md) - [PSR-17](./PSR-0.md) - [PSR-18](./PSR-18.md)
> Traduction française non-officielle de [_PSR-1: Basic Coding Standard_](https://www.php-fig.org/psr/psr-1/).

# PSR-1 : standard minimal pour la programmation PHP

_Cette section du standard PSR présente ce qui devrait être considéré comme les éléments fondamentaux requis pour la programmation PHP, afin d’assurer un haut niveau d’interopérabilité entre scripts PHP._

_Les mots-clés "DOIT", "NE DOIT PAS", "REQUIÈRE", "DEVRA", "NE DEVRA PAS", "DEVRAIT", "NE DEVRAIT PAS", "RECOMMANDÉ", "PEUT" et "OPTIONNELLEMENT" [ainsi que leurs formes plurielles et négatives] dans ce document sont à interpréter au sens de la [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)._

## 1. En résumé

- Les fichiers DOIVENT uniquement utiliser les tags `<?php` ou `<?=`.
- Les fichiers DOIVENT uniquement utiliser un encodage UTF-8, sans BOM, en présence de code PHP.
- Les fichiers PEUVENT soit déclarer des symboles (classes, fonctions, constantes, etc.), _soit_ déclencher des effets de bord (par exemple, générer du contenu, changer des paramètres .ini, etc.), mais ils NE DEVRAIENT PAS faire les deux à la fois.
- Les espaces de noms (_namespaces_) et les classes DOIVENT se conformer à un standard PSR de chargement automatique (_autoloading_) : [[PSR-0](./PSR-0.md), [PSR-4](./PSR-4.md)].
- Les noms de classes DOIVENT être déclarés en `PascalCase`.
- Les constantes de classe DOIVENT être déclarées en majuscule avec des underscore (`_`) en tant que séparateurs.
- Les noms des méthodes DOIVENT être déclarées en `camelCase`.

## 2. Les fichiers

### 2.1 Balises PHP

Le code PHP DOIT utiliser les balises ouvrantes/fermantes soit en version longue `<?php ?>` _soit_ en version courte `<?= ?>` ; le code PHP ne DOIT PAS utiliser d’autres versions.

### 2.2 Encodage des caractères

Le code PHP DOIT uniquement utiliser l’encodage UTF-8, sans BOM.

### 2.3 Effets de bord

Un fichier contenant du code PHP DEVRAIT _soit_ déclarer de nouveaux symboles (classes, fonctions, constantes, etc.) et ne pas causer d’effets de bord, _soit_ exécuter de la logique à effets de bord, mais ne DEVRAIT PAS faire les deux à la fois.

L’expression « effet de bord » fait référence à l’exécution de toute logique non directement liée à la déclaration de nouvelles classes, fonctions, constantes, etc. et à l’exception de la simple inclusion du fichier dans un autre.

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

## 3. Espaces de noms et nommage de classes

Les espaces de noms (_namespaces_) et les classes DOIVENT se conformer à un standard PSR de chargement automatique (_autoloading_) : [[PSR-0](./PSR-0.md), [PSR-4](./PSR-4.md)].

Cela signifie que toute classe est placée dans un fichier dédié, et à l’intérieur d’un _namespace_ d’au moins un niveau de profondeur (au niveau du _vendor name_ du projet).

Le nommage des classes DOIT suivre le standard [`PascalCase`](https://techlib.fr/definition/pascalcase.html).

Par exemple :

``` php
<?php
// Valable en PHP 5.3 et plus récent :
namespace Vendor\Model;

class Foo
{
}
```

Le code écrit pour la version 5.2 ou plus ancienne DEVRAIT utiliser la convention du « pseudo-espace de nom » (_pseudo-namespacing_) basée sur le préfixe `Vendor_` pour les noms de classe :

``` php
<?php
// Valable en PHP 5.2.x ou plus ancien :
class Vendor_Model_Foo
{
}
```
