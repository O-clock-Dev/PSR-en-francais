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

Lorsqu’une classe mobilise une liste d’interfaces avec `implements` (ou lorsqu’une interface mobilise une liste d’autres interfaces avec `extends` [ndt: cf. [exemple #3](https://www.php.net/manual/fr/language.oop5.interfaces.php)]), ces listes PEUVENT être réparties sur plusieurs lignes, à raison d’une interface maximum par nouvelle ligne, y compris le premier item de la liste, chaque ligne étant indentée d’un seul niveau.

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

### 4.2 Utilisation de traits

Le mot-clé `use` permettant de mobiliser un trait à l’intérieur d’une classe DOIT être placé sur la ligne qui suit immédiatement l’accolade ouvrante :

``` php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

Chaque trait importé dans une classe DOIT être placé sur sa propre ligne, et chaque inclusion DOIT correspondre à sa propre instruction `use` :

``` php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;
use Vendor\Package\SecondTrait;
use Vendor\Package\ThirdTrait;

class ClassName
{
    use FirstTrait;
    use SecondTrait;
    use ThirdTrait;
}
```

Quand une classe ne contient qu’une seule instruction et qu’il s’agit d’un import de trait avec `use`, alors l’accolade fermante de la classe DOIT être placée sur sa propre ligne, immédiatement après le `use` :

``` php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

Sinon, il DOIT y avoir une ligne vide après le dernier `use` :

``` php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;

    private $property;
}
```

Lorsque vous utilisez les opérateurs `insteadof` et `as`, ils DOIVENT être mis en œuvre de la manière suivante (y compris en ce qui concerne l’indentation, les espaces et les sauts de ligne) :

``` php
<?php

class Talker
{
    use A;
    use B {
        A::smallTalk insteadof B;
    }
    use C {
        B::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

### 4.3 Propriétés et constantes

Toute propriété DOIT être associée à une visibilité.

Pour tout projet codé avec une version de PHP supportant la visibilité des constantes (version 7.1 et plus récente), toute constante DOIT être associée à une visibilité.

Le mot-clé `var` ne DOIT PAS être utilisé pour déclarer une propriété.

Il ne DOIT PAS y avoir plus d’une déclaration de propriété par instruction.

Les nommage des propriétés ne DOIT PAS donner de sens particulier au caractère underscore (`_`) concernant la visibilité protégée ou privée. Autrement dit, un préfixe `_` n’a aucun sens particulier.

Il DOIT y avoir un espace entre la déclaration de type et le nom de la propriété.

Une déclaration de propriété peut dès lors ressemble à ceci :

``` php
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

### 4.4 Méthodes et fonctions

Toute méthode DOIT être associée à une visibilité.

Les nommage des méthodes ne DOIT PAS donner de sens particulier au caractère underscore (`_`) concernant la visibilité protégée ou privée. Autrement dit, un préfixe `_` n’a aucun sens particulier.

Les noms de méthodes et de fonctions ne DOIVENT PAS être suivis d’un espace. L’accolade ouvrante DOIT être placée sur sa propre ligne, et l’accolade fermante DOIT être placée sur la ligne suivant immédiatement la fin du corps de la méthode ou fonction. Il ne DOIT PAS y avoir d’espace après la parenthèse ouvrante et avant la parenthèse fermante.

Une déclaration de méthode ressemble au code suivant (notez en particulier la position des parenthèses, virgules, espaces et accolades) :

``` php
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // corps de la méthode
    }
}
```

Une déclaration de fonction ressemble au code suivant (notez en particulier la position des parenthèses, virgules, espaces et accolades) :

``` php
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // corps de la fonction
}
```

### 4.5 Paramètres des méthodes et fonctions

La liste des paramètres ne DOIT PAS contenir d’espace _avant_ les virgules séparatrices, mais DOIT contenir un unique espace _après_ chacune des ces virgules.

Les paramètres de méthodes et de fonctions recevant une valeur par défaut DOIVENT être positionnés en fin de liste :

``` php
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // corps de la méthode
    }
}
```

Une liste de paramètres PEUT être répartie sur plusieurs lignes, chacune étant indentée d’un seul niveau. Dans ce cas, le premier item de la liste doit lui aussi être positionné sur sa propre ligne, et la liste décomposée à raison d’un argument par ligne.

Lorsqu’une liste de paramètres est ainsi réparties sur plusieurs lignes, la parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur leur propre ligne, avec un unique espace entre les deux caractères :

``` php
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // corps de la méthode
    }
}
```

Si le type de la valeur de retour est déclaré, il DOIT y avoir un unique espace après le caractère deux-point (`:`) et avant la déclaration du type. Le caractère `:` et la déclaration de type DOIVENT être positionnés sur la même ligne que la parenthèse fermante de la liste des paramètres, et ceci toujours sans mettre d’espace entre la parenthèse et `:` :

``` php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
```

Les déclarations de types _nullable_ ne DOIVENT PAS contenir d’espace entre le point d’interrogation (`?`) et le type :

``` php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

Lorsque l’opérateur de référence `&` est utilisé avant un paramètre, il ne DOIT PAS y avoir d’espace après l’opérateur (ce qui est illustré par l’exemple ci-dessus).

Il ne DOIT PAS y avoir d’espace entre les trois petits points signalant un comportement variadique, et le nom du paramètre-collecteur :

``` php
public function process(string $algorithm, ...$parts)
{
    // processing
}
```

Lorsque l’opérateur de référence est combiné avec le token variadique, il ne DOIT PAS y avoir d’espace entre les deux :

``` php
public function process(string $algorithm, &...$parts)
{
    // processing
}
```

### 4.6 `abstract`, `final` et `static`

Si présentes, les déclarations `abstract` et `final` DOIVENT précéder la déclaration de visibilité.

Si présentes, la déclaration `static` DOIT être précédée de la déclaration de visibilité.

``` php
<?php

namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // corps de la méthode
    }
}
```

### 4.7 Appels de méthodes et fonctions

Lors d’un appel à une méthode ou à une fonction, il ne DOIT PAS y avoir d’espace entre le nom de la méthode ou fonction, et la parenthèse ouvrante ; il ne DOIT PAS y avoir d’espace après la parenthèse ouvrante ; il ne DOIT PAS y avoir d’espace avant la parenthèse fermante. Au niveau de la liste des arguments, il ne DOIT PAS y avoir d’espace avant les virgules séparatrices, et il DOIT y avoir un unique espace après chacune de ces virgules :

``` php
<?php

bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

La liste des arguments d’appel PEUT être répartie sur plusieurs lignes, chacune étant indentée d’un seul niveau. Dans ce cas, le premier item de la liste doit lui aussi être positionné sur sa propre ligne, et la liste décomposée à raison d’un argument par ligne. Il arrive qu’un unique argument soit syntaxiquement réparti sur plusieurs lignes (comme c’est parfois le cas des fonctions ou tableaux anonymes pour un callback), mais cela n’est pas équivalent au fait de répartir une _liste_ d’arguments sur plusieurs lignes :

``` php
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
<?php
```

``` php
somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) {
    return 'Hello ' . $app->escape($name);
});
```

## 5. Structures de contrôle

Les règles stylistiques générales concernant les structures de contrôles sont les suivantes :

- il DOIT y avoir un unique espace après le mot-clé de la structure de contrôle
- il ne DOIT PAS y avoir d’espace après la parenthèse ouvrante
- il ne DOIT PAS y avoir d’espace avant la parenthèse fermante
- il DOIT y avoir un unique espace entre la parenthèse fermante et l’accolade ouvrante
- le code de la structure de contrôle DOIT être indenté, d’un seul niveau
- le code de la structure de contrôle DOIT débuter sur la nouvelle ligne immédiatement en-dessous de l’accolade ouvrante
- l’accolade fermante DOIT être placée sur la nouvelle ligne immédiatement en-dessous du code de la structure de contrôle

Le corps de toute structure de contrôle DOIT être délimité par des accolades. Cela contribue à standardiser visuellement la façon dont sont codées ces structures, et participe de minimiser les chances d’introduire des erreurs lors du rajout de nouvelles lignes dans la structure.

### 5.1 `if`, `elseif`, `else`

Une structure `if` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèses, espaces et accolades, ainsi que le fait que les mots-clés `elseif` et `else` sont positionnés sur la même ligne que l’accolade fermante du bloc-logique précédent) :

``` php
<?php

if ($expr1) {
    // bloc du if
} elseif ($expr2) {
    // bloc du elseif
} else {
    // bloc du else;
}
```

Le mot-clé `elseif` DEVRAIT être utilisé en lieu et place de `else if`, de sorte que tous les mots-clés mobilisés au sein d’une structure de contrôle soient composés d’un seul mot naturel/visuel.

Les expressions placées entre les parenthèses PEUVENT être réparties sur plusieurs lignes, à raison d’une expression par nouvelle ligne indentée. Dans ce cas, chaque expression y compris la première DOIVENT être placées sur une ligne dédiée. La parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur une ligne dédiée, avec un unique espace entre ces deux caractères. Les opérateurs booléens placés entre des conditions réparties sur plusieurs lignes DOIVENT toujours être positionnés, _soit_ au début des lignes, _soit_ à la fin des lignes, mais pas un mélange des deux :

``` php
<?php

if (
    $expr1
    && $expr2
) {
    // bloc du if
} elseif (
    $expr3
    && $expr4
) {
    // bloc du elseif
}
```

### 5.2 `switch`, `case`

Une structure `switch` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèse, espaces et accolades ; les déclarations `case` DOIVENT être indentées d’un niveau relativement au mot-clé `switch`, et le mot-clé `break` [ou tout autre mot-clé de terminaison] DOIT être indenté de la même quantité que les blocs `case` ; tout `case` non-vide résultant une cascade volontaire vers le prochain cas non-vide doit l’indiquer explicitement avec un commentaire du type `// no break`) :

``` php
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

Les expressions placées entre les parenthèses PEUVENT être réparties sur plusieurs lignes, à raison d’une expression par nouvelle ligne indentée. Dans ce cas, chaque condition y compris la première DOIVENT être placées sur une ligne dédiée. La parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur une ligne dédiée, avec un unique espace entre ces deux caractères. Les opérateurs booléens placés entre des conditions réparties sur plusieurs lignes DOIVENT toujours être positionnés, _soit_ au début des lignes, _soit_ à la fin des lignes, mais pas un mélange des deux :

``` php
<?php

switch (
    $expr1
    && $expr2
) {
    // corps de la structure
}
```

### 5.3 `while`, `do while`

Une structure `while` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèses, espaces et accolades) :

``` php
<?php

while ($expr) {
    // corps de la structure
}
```

Les expressions placées entre les parenthèses PEUVENT être réparties sur plusieurs lignes, à raison d’une expression par nouvelle ligne indentée. Dans ce cas, chaque condition y compris la première DOIVENT être placées sur une ligne dédiée. La parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur une ligne dédiée, avec un unique espace entre ces deux caractères. Les opérateurs booléens placés entre des conditions réparties sur plusieurs lignes DOIVENT toujours être positionnés, _soit_ au début des lignes, _soit_ à la fin des lignes, mais pas un mélange des deux :

``` php
<?php

while (
    $expr1
    && $expr2
) {
    // corps de la structure
}
```

De manière similaire, une structure `do while` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèses, espaces et accolades) :

``` php
<?php

do {
    // structure body;
} while ($expr);
```

Les expressions placées entre les parenthèses PEUVENT être réparties sur plusieurs lignes, à raison d’une expression par nouvelle ligne indentée. Dans ce cas, chaque condition y compris la première DOIVENT être placées sur une ligne dédiée. La parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur une ligne dédiée, avec un unique espace entre ces deux caractères. Les opérateurs booléens placés entre des conditions réparties sur plusieurs lignes DOIVENT toujours être positionnés, _soit_ au début des lignes, _soit_ à la fin des lignes, mais pas un mélange des deux :

``` php
<?php

do {
    // structure body;
} while (
    $expr1
    && $expr2
);
```

### 5.4 `for`

Une structure `for` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèses, espaces et accolades) :

``` php
<?php

for ($i = 0; $i < 10; $i++) {
    // bloc du for
}
```

Les expressions placées entre les parenthèses PEUVENT être réparties sur plusieurs lignes, à raison d’une expression par nouvelle ligne indentée. Dans ce cas, chaque condition y compris la première DOIVENT être placées sur une ligne dédiée. La parenthèse fermante et l’accolade ouvrante DOIVENT être positionnées ensemble sur une ligne dédiée, avec un unique espace entre ces deux caractères. Les opérateurs booléens placés entre des conditions réparties sur plusieurs lignes DOIVENT toujours être positionnés, _soit_ au début des lignes, _soit_ à la fin des lignes, mais pas un mélange des deux :

``` php
<?php

for (
    $i = 0;
    $i < 10;
    $i++
) {
    // bloc du for
}
```

### 5.5 `foreach`

Une structure `foreach` ressemble à l’exemple ci-dessous (notez en particulier la position des parenthèses, espaces et accolades) :

``` php
<?php

foreach ($iterable as $key => $value) {
    // bloc du foreach
}
```
