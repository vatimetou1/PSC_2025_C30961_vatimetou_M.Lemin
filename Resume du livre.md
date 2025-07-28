1. Introduction à Python et mise en place de l’environnement
Installation et préparation
L’ouvrage suggère d’utiliser Anaconda, une distribution Python qui :

simplifie la gestion des environnements virtuels indépendants,

contient Python, IPython, Jupyter Notebook, matplotlib, NumPy, SciPy ainsi que l’éditeur Spyder.

Cela permet de ne pas affecter l’installation globale de Python sur la machine, limitant ainsi les conflits potentiels avec d’autres logiciels. En cas de souci, il suffit de supprimer le dossier Anaconda puis de le réinstaller.

Version recommandée
L’ensemble des exemples repose sur Python 3.x, à partir de la version 3.7.

Utilisation de Spyder
Spyder, inclus dans Anaconda, est un environnement de développement intégré pensé pour le calcul scientifique.

Par défaut, l’interface se compose de trois volets :

un éditeur de code,

une console IPython,

un panneau d’aide.

Il est conseillé d’ajouter en haut de chaque fichier :

python
  
  
from numpy import *
from matplotlib.pyplot import *
Cela donne accès directement aux principales fonctions.

Spyder peut afficher un avertissement (triangle jaune) pour certaines pratiques comme from numpy import *, mais ces remarques sont ignorées ici intentionnellement.

IPython et Jupyter Notebook
IPython offre une expérience enrichie par rapport au shell Python traditionnel, avec :

l’aide instantanée (?),

la complétion automatique (Tab),

l’historique des commandes,

les commandes spéciales (%timeit, %run, etc.),

un affichage plus lisible.

Jupyter Notebook permet de rédiger des documents interactifs combinant texte, code et graphiques, parfaits pour :

les devoirs,

les prises de notes,

les présentations.

Pour le démarrer :

bash
  
  
jupyter notebook
Un navigateur s’ouvrira, donnant accès à une interface interactive pour travailler avec Python.

Lancer un script
Depuis IPython :

cd pour changer de répertoire,

run script.py pour exécuter un fichier.

2. Variables et types fondamentaux
Déclaration de variables
Python détecte automatiquement le type d’une variable.

Les noms peuvent contenir des lettres, chiffres et underscores, mais ne doivent pas débuter par un chiffre.

Sensible à la casse (maVar ≠ Mavar).

Types numériques
Entiers (int)
Représente tous les entiers relatifs, sans limite autre que la mémoire disponible.

Nombres à virgule flottante (float)
Approximations de nombres réels.

Exemple :

```python

  
  
6 // 2  # 3
7 // 2  # 3
7 / 2   # 3.5
Précautions à prendre avec les arrondis :

python
  
  
0.4 - 0.3  # 0.10000000000000003
Nombres complexes
Python emploie j pour l’unité imaginaire :

python
  
  
z = 3.5 + 5.2j
z.real       # 3.5
z.imag       # 5.2
z.conjugate()  # (3.5 - 5.2j)
Infini et NaN
python
  
  
from numpy import *
a = exp(1000)  # inf
a - a          # nan
Comparer nan à quoi que ce soit retourne toujours False.

Booléens
True et False sont des entiers spéciaux.

Les opérateurs logiques sont and, or, not.

Comparaisons multiples possibles :

python
  
  
2 < 3 < 5  # True
Les valeurs vides sont évaluées comme False.

Chaînes de caractères
Enfermées entre '...' ou "...", les chaînes multi-lignes utilisent """...""".

Séquences d’échappement utiles :

\n pour saut de ligne,

\t pour tabulation,

\\ pour backslash,

\" pour guillemet.

Chaînes brutes avec r"...".

Manipulations
Concaténation : 'a' + 'b'

Répétition : 'Hi' * 3 → 'HiHiHi'

Comparaison : 'Ana' < 'Arwa'

Fonctions utiles : .split(), .join(), .find()

Formatage :

python
  
  
f"Note : {note:.2f}"
"{} {}".format("Bonjour", "le monde")
3. Structures de données standards
Aperçu général
Python propose plusieurs structures intégrées pour manipuler des groupes de données :

listes : collections ordonnées et modifiables,

tuples : séquences ordonnées mais non modifiables,

dictionnaires : paires clé-valeur sans ordre,

sets : ensembles non ordonnés d’éléments uniques,

arrays NumPy : tableaux multidimensionnels optimisés pour les calculs.

Listes
Définition
python
  
  
L = [10, 20, 30, 40]
Accès via l’indice (dès 0) :

python
  
  
L[0]    # 10
L[-1]   # 40
Découpage (slicing)
python
  
  
L[1:3]    # [20, 30]
L[::2]    # [10, 30]
Modification
python
  
  
L[1] = 99
Fonctions associées
python
  
  
L.append(50)
L.extend([60, 70])
L.insert(2, 25)
L.remove(30)
x = L.pop()
L.sort()
L.reverse()
Compréhensions de liste
python
  
  
[x**2 for x in range(5) if x % 2 == 0]  # [0, 4, 16]
Tuples
Définis avec () :

python
  
  
t = (1, 2, 3)
Accès comme une liste :

python
  
  
t[0]  # 1
Utile pour retourner plusieurs éléments :

python
  
  
def f():
    return 1, 2
a, b = f()
Pour un seul élément :

python
  
  
t = (42,)
Dictionnaires
Définition :

python
  
  
d = {'nom': 'Alice', 'âge': 30}
Accès :

python
  
  
d['nom']
Boucles :

python
  
  
for k in d:
    print(k)
for v in d.values():
    print(v)
for k, v in d.items():
    print(f"{k} : {v}")
Méthodes utiles :

python
  
  
d.get('nom', 'inconnu')
d.pop('âge')
Sets (ensembles)
Uniques et non ordonnés :

python
  
  
s = {1, 2, 3, 3}
Ajout / retrait :

python
  
  
s.add(4)
s.remove(2)
Opérations :

python
  
  
A | B        # union
A & B        # intersection
A - B        # différence
Tableaux NumPy
Optimisés pour le calcul scientifique :

python
  
  
from numpy import array
A = array([[1, 2], [3, 4]])
Accès :

python
  
  
A[1, 0]  # 3
Opérations :

python
  
  
A + A
A * A
Conversions
python
list((1, 2))      # [1, 2]
set([1, 2, 2])    # {1, 2}
tuple("abc")      # ('a', 'b', 'c')