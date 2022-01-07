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
