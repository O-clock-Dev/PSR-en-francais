> [PSR-0](./PSR-0.md) - [PSR-1](./PSR-1.md) - [PSR-3](./PSR-3.md) - [PSR-4](./PSR-4.md) - [PSR-6](./PSR-6.md) - [PSR-7](./PSR-7.md) - [PSR-11](./PSR-11.md) - **PSR-12** - [PSR-13](./PSR-13.md) - [PSR-14](./PSR-14.md) - [PSR-15](./PSR-15.md) - [PSR-16](./PSR-16.md) - [PSR-17](./PSR-0.md) - [PSR-17](./PSR-0.md) - [PSR-18](./PSR-18.md)
> Traduction française non-officielle de [_PSR-12: Extended Coding Style_](https://www.php-fig.org/psr/psr-12/).

# PSR-12 : guide de style

_Les mots-clés "DOIT", "NE DOIT PAS", "REQUIÈRE", "DEVRA", "NE DEVRA PAS", "DEVRAIT", "NE DEVRAIT PAS", "RECOMMANDÉ", "PEUT" et "OPTIONNELLEMENT" [ainsi que leurs formes plurielles et négatives] dans ce document sont à interpréter au sens de la [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)._

## 1. En résumé

Cette spécification étend et remplace la désormais dépréciée PSR-2 (_Coding Style Guide_), et suppose que le standard [PSR-1](./PSR-1.md) (_Basic Coding Standard_) est suivi.

Tout comme la PSR-2, le but de cette spécification est de réduire la friction cognitive qui peut apparaître lorsqu’un développeur scanne visuellement le code produit par d’autres personnes. La spécification se propose d’atteindre ce but en énumérant un certain nombre de règles communes relatives au formattage du code PHP. Cette PSR ambitionne de servir de référence pour les outils de formattage, pour les porteurs de projet et pour les développeurs qui sont amenés à changer régulièrement de projets. Dans ces situations où des auteurs variés sont amenés à collaborer sur de multiples projets, il est très pratique d’avoir de telles lignes directrices stables. Aussi, le réel bénéfice de ce guide n’est pas tant les règles en elles-mêmes, que le fait de les partager.

La PSR-2 a été acceptée en 2012, et depuis, PHP en tant que langage a beaucoup évolué, ce qui a eu des implications concernant son formattage. Même si la PSR-2 était très complète concernant les fonctionnalités disponibles à l’époque de son écriture, ce n’était pas le cas concernant les nouvelles fonctionnalités, qui étaient de fait sujettes à interprétation. Cette nouvelle PSR se donne donc pour objectif de clarifier la PSR-2, en prenant en compte le nouveau contexte du langage, plus moderne, et en incorporant les nouvelles fonctionnalités que ne traitait pas l’ancienne PSR.

### Précédentes versions du langage

Dans la suite de ce document, toute instruction PEUT être ignorée si elle n’existe pas dans la version de PHP utilisée dans votre contexte de projet.

### Exemple

Ci-dessous, un exemple regroupant certaines des règles de la spécification :

``` php
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // corps de la méthode
    }
}
```

## 2. Généralités

### 2.1 Standards basiques

Le code DOIT respecter toutes les règles de la [PSR-1](./PSR-1.md).

Le terme « PascalCase » dans la PSR-1 DOIT être compris au sens d’une recommendation syntaxique où la première lettre de chaque mot est en majuscule, y compris la première lettre du premier mot.

### 2.2 Fichiers

Tout fichier PHP DOIT uniquement utiliser la terminaison de ligne de type Unix LF.

Tout fichier PHP DOIT se terminer par une ligne non-vide, elle-même terminée par un unique caractère LF.

La balise fermante `?>` DOIT être omise des fichiers ne contenant que du code PHP.

### 2.3 Lignes

Il ne DOIT PAS y avoir de limite de longueur de ligne imposée par l’éditeur de texte (_hard limite_).

La valeur de toute limite de longueur de ligne suggérée par l’éditeur de texte (_soft limit_) DOIT être de 120 caractères.

Les lignes ne DEVRAIENT PAS dépasser 80 caractères ; les lignes plus longues que cela DEVRAIENT être découpées en plusieurs morceaux répartis sur les lignes suivantes, chacune de ces lignes ne dépassant pas 80 caractères.

Il ne DOIT PAS y avoir d’espaces typographiques (_trailing whitespaces_) à l’extrémité finale des lignes.

Des lignes vides internes PEUVENT être ajoutées dans le but d’améliorer la lisibilité et pour mettre en évidence des blocs thématiques de code, sauf si cette pratique est explicitement proscrite.

Il ne DOIT pas y avoir plus d’une instruction par ligne.

### 2.4 Indentation

Le code DOIT être indenté en utilisant 4 espaces pour chaque niveau supplémentaire d’indentation, et les tabulations ne DOIVENT PAS être utilisées pour indenter.

### 2.5 Mots-clés et types

Tous les mots-clés réservés et les types de PHP DOIVENT être écrits en minuscule.

Tout nouveau type ou mot-clé qui sera ajouté dans les futures versions de PHP DOIVENT l’être en minuscule.

Seules les formes courtes des types DOIVENT être utilisées, par ex. `bool` et non `boolean`, `int` et non `integer`, etc.

## 3. Déclarations, espaces de nommage et imports

L’en-tête d’un fichier PHP peut contenir plusieurs blocs. Lorsque présents, chaque bloc DOIT être séparé par une ligne vide, en ne DOIT PAS contenir de ligne vide. Les blocs DOIVENT être ordonnés comme listé ci-dessous, étant entendu que les blocs inutiles dans un certain contexte peuvent simplement être omis :

- Balise d’ouverture `<?php`
- Docblock général du fichier
- Une ou plusieurs instructions de déclaration
- Déclaration de l’espace de nommage du fichier
- Une ou plusieurs instructions d’import de classe(s) utilisant `use`
- Une ou plusieurs instructions d’import de fichier(s) utilisant `use`
- Une ou plusieurs instructions d’import de constante(s) utilisant `use`
- Le reste du code PHP

Lorsqu’un fichier contient un mélange de code PHP et HTML, tout ou partie des blocs listés ci-dessus peuvent très bien être utilisés. Dans ce cas, ils DOIVENT être placés en tête du fichier, même dans le cas où le « reste du code » ne consiste qu’en une balise fermante `?>` puis un mélange de HTML et de PHP.

Lorsque la balise ouvrante `<?php` constitue la toute première ligne du fichier, elle DOIT être placée sur une ligne dédiée, sans aucune autre instruction, sauf dans le cas où le fichier ne contiendrait que du balisage HTML placé en-dehors des balises ouvrante et fermante de PHP.

Les instructions d’imports ne DOIVENT JAMAIS commencer avec un antislash, rapport au fait qu’elles doivent toujours correspondre à un nom complet.

L’exemple suivant donne une idée de tous les types de blocs admissibles :

``` php
<?php

/**
 * Ce fichier contient des exemples des règles stylistiques pour coder en PHP.
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar est un exemple de classe PHP.
 */
class FooBar
{
    // ... plus de code PHP ...
}
```

La composition d’espaces de nommage ne DOIT PAS dépasser deux niveaux de profondeur. Voici par conséquent le maximum autorisé :

``` php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

et un exemple de ce qui n’est pas autorisé :

``` php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

Lorsque vous souhaitez activer le typage strict dans un fichier contenant du balisage HTML placé en-dehors des balises ouvrantes et fermantes de PHP, cette déclaration de [directive d’exécution](https://www.php.net/manual/fr/control-structures.declare.php) DOIT être placée sur la première ligne du fichier et contenir une balise ouvrante, la déclaration elle-même, et une balise fermante.

Par exemple :

``` php
<?php declare(strict_types=1) ?>
<html>
<body>
    <?php
        // ... code PHP supplémentaire ...
    ?>
</body>
</html>
```

L’instruction de déclaration ne DOIT PAS contenir d’espace et DOIT être exactement `declare(strict_types=1)` (avec éventuellement le terminateur `;`).

Les déclarations de directive d’exécution de type bloc sont autorisées et DOIVENT dans ce cas être formattées comme suit (notez la position des accolades et la présence d’espaces) :

``` php
declare(ticks=1) {
    // du code
}
```

## 4. Classes, propriétés et méthodes

Le terme « classe » désigne toute classe, interface ou trait.

Toute accolade fermante ne DOIT PAS être suivie d’un commentaire ou d’une instruction qui serait placée sur la même ligne.

Lorsque vous instanciez une nouvelle classe, des parenthèses DOIVENT être présentes, même dans le cas où aucun argument n’est passé au constructeur :

``` php
new Foo();
```

### 4.1 `extends` et `implements`

Les mots-clés `extends` et `implements` DOIVENT être déclarés sur la même ligne que la déclaration du nom de la classe.

L’accolade ouvrante d’une classe DOIT être placée sur sa propre ligne ; l’accolade fermante DOIT être placée sur sa propre ligne après le corps de la classe.

Toute accolade ouvrante doit être placée sur sa propre ligne et ne DOIT PAS être précédée ou suivie par une ligne vide.

Toute accolade fermante doit être placée sur sa propre ligne et ne DOIT PAS être précédée par une ligne vide.

``` php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constantes, propriétés et méthodes
}
```

Lorsqu’une classe mobilise une liste d’interfaces avec `extends` (ou lorsqu’une interface mobilise une liste d’autres interfaces avec `extends` [ndt: cf. [exemple #3](https://www.php.net/manual/fr/language.oop5.interfaces.php)]), ces listes PEUVENT être réparties sur plusieurs lignes, à raison d’une interface maximum par nouvelle ligne, y compris le premier item de la liste, chaque ligne étant indentée d’un seul niveau.

``` php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constantes, propriétés et méthodes
}
```
