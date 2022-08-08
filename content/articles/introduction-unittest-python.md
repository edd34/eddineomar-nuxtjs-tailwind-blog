---
title: Les tests en Python avec unittest
description: Introduction à la librairie unittest en Python
category:
  - Architectures logicielles
author: Eddine Omar
date: 2022-05-14T10:28:00.00Z
draft: false
image: https://unsplash.com/photos/D9Zow2REm8U/download?ixid=MnwxMjA3fDB8MXxhbGx8fHx8fHx8fHwxNjU5NzE2MDQ4&force=true&w=640
---

# Introduction
Comme dans tout projet logiciel sérieux, afin d'augmenter la qualité de celui-ci, il est nécessaire de mettre en place des tests automatisés et de les exécuter automatiquement. Cela permet de s'assurer que les développements futurs ne vont pas casser la base de code actuelle. Mettre en place des tests unitaires dans la base de code actuelle permettra de s'assurer que les features principales de notre projet sont fonctionnelles.

Découvrons ensemble la librairie [unittest](https://docs.python.org/3/library/unittest.html) de Python !

# Unittest
Unittest est un framework de test inclus dans la bibliothèque standard de Python, c'est-à-dire qu'il n'est pas nécessaire de l'installer en tant que package externe.

## Le code de démarrage avec unittest

```python
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_fail(self):
      # test will fail
        self.assertTrue(False)

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)



if __name__ == '__main__':
    unittest.main()

```
Cet exemple de code couvre ce dont vous avez le plus besoin de connaître lors de votre usage quotidien de la librairie.

## Lancement du test
Pour lancer les tests, il suffit de se placer à la racine du projet et d'exécuter la commande :
```bash
python -m unittest -v
```
Le paramètre `-v` permettra d'avoir plus de verbosité sur la console.

Cela fournira le résultat suivant avec le paramètre `-v`
```bash
❯ python -m unittest -v
test_fail (test_module1.TestStringMethods) ... FAIL
test_isupper (test_module1.TestStringMethods) ... ok
test_split (test_module1.TestStringMethods) ... ok
test_upper (test_module1.TestStringMethods) ... ok

======================================================================
FAIL: test_fail (test_module1.TestStringMethods)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "~/path/to/test_folder/test_module1.py", line 14, in test_fail
    self.assertTrue(False)
AssertionError: False is not true

----------------------------------------------------------------------
Ran 4 tests in 0.000s

FAILED (failures=1)
```
Cela fournira le résultat suivant sans le paramètre `-v
`
```bash
❯ python3 -m unittest
F...
======================================================================
FAIL: test_fail (test_module1.TestStringMethods)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "~/path/to/test_folder/test_module1.py", line 14, in test_fail
    self.assertTrue(False)
AssertionError: False is not true

----------------------------------------------------------------------
Ran 4 tests in 0.000s

FAILED (failures=1)
```

Il est préférable utiliser le paramètre `-v` lorsque les tests sont lancés sur votre propre machine. Dans un pipeline CI/CD (Gitlab CI, Github Actions, Jenkins ou autre) il sera préférable de ne pas utiliser le paramètre -v.

## setUp et tearDown

Il existe deux méthodes optionnelles qu'il convient de connaître et qui s'avèrent extrêment utile. Il s'agit des méthodes **setUp** (*signifie mettre en place*) et **tearDown** (*signifie démolir*) :
 * `setup` permet de définir du code qui va être exécuté avant chaque test
 * `tearDown` permet de définir du code qui va être exécuté après chaque test

Durant les tests, on utilisera setUp et tearDown afin de par exemple configurer des dossiers, mettre le projet ou la base de donnée dans un état connu avant les tests etc...

Voici un exemple avec l'utilisation de setUp et tearDown :

```python
import unittest

class TestStringMethods(unittest.TestCase):
    def setUp(self):
        print("setup")
    def tearDown(self):
        print("tearDown")
    def test_upper(self):
        print("test_upper")
        self.assertEqual("foo".upper(), "FOO")
    def test_isupper(self):
        print("test_isupper")
        self.assertTrue("FOO".isupper())
        self.assertFalse("Foo".isupper())


if __name__ == "__main__":
    unittest.main()

```

Après lancement des tests en mode verveux avec `python -m unittest -v`, nous avons cet affichage sur console :
```bash
test_isupper (test_module1.TestStringMethods) ... setup
test_isupper
tearDown
ok
test_upper (test_module1.TestStringMethods) ... setup
test_upper
tearDown
ok

----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
```

NB : Remarquez que les méthodes setUp et tearDown sont utilisées avant et après chaque test case.

## Les asserts
Les asserts sont des méthodes qui sont utilisées pour vérifier (ou affirmer) ou non la validité d'un test. Voici un exemple d'utilisation d'assert :

```python
import unittest

class SimpleTest(unittest.TestCase):
    def test1(self):
       self.assertEqual(4 + 5,9)
    def test2(self):
       self.assertNotEqual(5 * 2,10)
    def test3(self):
       self.assertTrue(4 + 5 == 9,"The result is False")
    def test4(self):
       self.assertTrue(4 + 5 == 10,"assertion fails")
    def test5(self):
       self.assertIn(3,[1,2,3])
    def test6(self):
       self.assertNotIn(3, range(5))

if __name__ == '__main__':
   unittest.main()

```
Une liste exhaustive des assert est présentées sur ce [https://docs.python.org/3/library/unittest.html#assert-methods](https://docs.python.org/3/library/unittest.html#assert-methods)

# Points à retenir

 * Le nom d'un fichier de test, d'un test suite et d'un test case doit commencer par "test_"
 * Un test case est crée lorsqu'une classe hérite de `unittest.TestCase`
 * setUp et tearDown sont utilisés respectivement avec chaque et après chaque test case
 * pour lancer les tests unitaires : `python -m unittest -v`


# Sources :
* [unittest - Unittest testing framework](https://docs.python.org/3/library/unittest.html)

------------------------------------------