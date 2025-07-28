 Chapitre 4 – Algèbre linéaire avec NumPy
4.1 – Introduction aux tableaux NumPy
L’algèbre linéaire, qui manipule des vecteurs et des matrices, est un pilier des calculs numériques. NumPy fournit les outils essentiels pour gérer ces structures.

4.1.1 – Vecteurs et matrices
On commence par importer :
from numpy import *

Un vecteur peut être créé avec :
v = array([1., 2., 3.])

Opérations de base : multiplication par un scalaire, combinaison linéaire, multiplication élément par élément, produit scalaire avec dot() ou @.

Exemple :

```python

  
  
2 * v, v / 2, v1 + 3*v2
dot(v1, v2), v1 @ v2, v1 * v2
Matrices = listes de listes :
M = array([[1., 2.], [0., 1.]])

Transformation :

Ligne : v.reshape((1, 3))

Colonne : v.reshape((3, 1))

4.1.2 – Indexation et découpage
Comme les listes Python, mais en multidimension :

python
  
  
v[0], M[1, 0], v[1:], M[1:]
v[0] = 10
v[:2] = [0, 1]
4.1.3 – Opérations d’algèbre linéaire
Produit scalaire ou matriciel :
dot(M, v) ou M @ v

Système linéaire :

python
  
  
from numpy.linalg import solve
x = solve(A, b)
4.2 – Fondements mathématiques
4.2.1 – Tableaux vus comme fonctions
Un vecteur peut être vu comme une fonction d’indice.

Une matrice peut être vue comme une fonction à deux variables (ligne, colonne).

4.2.2 – Opérations élément par élément
En NumPy, les opérations s’appliquent point par point :

python
  
  
A * B  # multiplication élément par élément
4.2.3 – Forme et dimensions
Scalaire : ()

Vecteur : (n,)

Matrice : (m, n)

Tenseur : (d1, d2, d3, ...)

python
  
  
array.shape
array.ndim
4.2.4 – Produit dot : vue réduction
Vecteur · vecteur → scalaire

Matrice · vecteur → vecteur

Matrice · matrice → matrice

python
  
  
M @ v
4.3 – Le type ndarray de NumPy
4.3.1 – Attributs clés
Attribut	Signification
.shape	Dimensions
.dtype	Type des données
.strides	Décalage mémoire entre éléments

python
  
  
A = array([[1, 2, 3], [3, 4, 6]])
A.shape, A.dtype, A.strides
4.3.2 – Créer un tableau
python
  
  
V = array([1., 2., 1.], dtype=float)
Sans dtype, il est automatiquement détecté.

Attention aux conversions silencieuses :

python
  
  
a = array([1, 2])
a[0] = 0.5  # sera tronqué à 0
4.4 – Accès aux éléments
python
  
  
M[0, 0], M[-1, 0]
M[1:3, :]
Les slices sont des vues, donc toute modification modifie aussi l’original.

python
  
  
v = array([1., 2., 3.])
v1 = v[:2]
v1[0] = 0.
Règles générales (extraits de tableaux) :
Type d’accès	Résultat
i, j	scalaire
i, :	ligne
:, j	colonne
slice, slice	matrice

4.5 – Construction de tableaux
python
  
  
zeros((2,2)), ones((3,3)), full((2,2), 5)
diag([1,2,3]), identity(3)
arange(5), linspace(0, 1, 5)
4.6 – Forme et transformation
python
  
  
v.reshape(2, 3)
v.reshape(2, -1)
A.T  # transposé
4.7 – Empilement de tableaux
python
  
  
hstack([v1, v2]), vstack([v1, v2])
concatenate([a1, a2], axis=0)
4.8 – Fonctions sur tableaux
Fonctions universelles
python
  
  
cos(array([0, pi])), array([1, 2]) ** 2
Fonctions personnalisées :
python
  
  
@vectorize
def step(x):
    return 1 if x >= 0 else 0
Fonctions d’agrégation :
python
  
  
sum(A), sum(A, axis=0), sum(A, axis=1)
4.9 – Résolution avec scipy.linalg
LU :

python
  
  
LU, piv = scipy.linalg.lu_factor(A)
x = scipy.linalg.lu_solve((LU, piv), b)
SVD :

python
  
  
U, S, VT = scipy.linalg.svd(A)
x = VT.T @ ((U.T @ b) / S)
Fonctions utiles : inv, pinv, eig, norm, qr, cholesky, solve, lstsq

4.10 – Bilan du chapitre
Tableaux NumPy = base pour vecteurs et matrices.

Utilisation des outils scipy.linalg pour des calculs performants.

Prépare le terrain pour les manipulations avancées du chapitre 5.

🧩 Chapitre 5 – Techniques avancées avec les tableaux
5.1 – Vues et copies
python
  
  
v = M[0, :]
v[-1] = 0.0  # M modifié aussi
N = array(M.T)  # copie réelle
5.2 – Comparaison de tableaux
Comparaison élément par élément :

python
  
  
A == B, (A == B).all()
allclose(A, B)
Opérateurs à utiliser : &, |, ~ au lieu de and, or, not

5.3 – Indexation par booléens
python
  
  
M[M > 2] = 0
B = M > 2
M[B] = [10, 20]
where(condition, a, b) ou where(condition) (indices)

5.4 – Performances et vectorisation
Boucles lentes → préférer les opérations NumPy :

python
  
  
A[1:-1,1:-1] = (A[:-2,1:-1] + A[2:,1:-1] + A[1:-1,:-2] + A[1:-1,2:]) / 4
5.5 – Broadcasting
Permet les opérations entre tableaux de tailles différentes :

python
  
  
C = arange(2).reshape(-1,1)
R = arange(2).reshape(1,-1)
C + R  # matrice 2x2
Exemples 

M * coeff.reshape(-1, 1) pour les lignes

M * coeff pour les colonnes

🔳 Chapitre 6 – Matrices creuses (sparse)
6.1 – Introduction
Stockage mémoire optimisé

Utilisé dans les problèmes à grande échelle

scipy.sparse : module dédié

6.2 – Types de formats
CSR : compressé par ligne

CSC : compressé par colonne

LIL : utile pour construction/modification

6.3 – Générer des matrices creuses
python
  
  
sp.eye(n), sp.spdiags(...), sp.rand(m,n)
6.4 – Fonctions disponibles
Conversion : .tocsr(), .toarray()

Produit : .dot()

Fonctions math : s’appliquent sur .data

6.5 – Récapitulatif
Comprendre les vues = code efficace

Matrices creuses = indispensables en calculs scientifiques

scipy.sparse est la référence pour leur manipulation 