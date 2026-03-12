#  Compte Rendu — TP n°4 :  JavaScript

**École Normale Supérieure de l'Enseignement Technique de Mohammedia**  
**Master SDIA — Technologies du Web & Web Sémantique**

---

##  Objectifs

Ce TD a pour but d'expérimenter les constructions de base du langage JavaScript :

- Types simples et déclarations de variables
- Instructions de contrôle (`if`, `else`)
- Itérations (`while`, `for`)
- Fonctions et logique algorithmique

La syntaxe JavaScript étant proche du langage C, ce TD sert de transition naturelle vers la programmation web côté client.

---

## Exercice 1 — Conversion de températures

### Énoncé
Écrire une fonction `degreC` qui convertit une température de degrés Fahrenheit en degrés Celsius à partir de la formule :

```
tempC = (5/9) * (tempF - 32)
```

### Solution

```javascript
function degreC(tempF) {
  let tempC = (5 / 9) * (tempF - 32);
  console.log(`Cette température équivaut à ${tempC.toFixed(1)} degrés Celsius`);
}

// Exemples d'exécution
degreC(0.0);   // → -17.8 degrés Celsius
degreC(60.0);  // → 15.6 degrés Celsius
```

### Résultats attendus

| Entrée (°F) | Sortie (°C) |
|------------|------------|
| 0.0        | -17.8      |
| 60.0       | 15.6       |

---

## Exercice 2 — Conversion de durées

### Énoncé
Écrire une fonction `hjms` qui convertit un nombre de secondes en jours, heures, minutes et secondes.

### Solution

```javascript
function hjms(totalSecondes) {
  let jours   = Math.floor(totalSecondes / 86400);
  let reste   = totalSecondes % 86400;
  let heures  = Math.floor(reste / 3600);
  reste       = reste % 3600;
  let minutes = Math.floor(reste / 60);
  let secondes = reste % 60;

  console.log(`Cette durée équivaut à ${jours} jours ${heures} heures ${minutes} minutes ${secondes} secondes`);
}

// Exemples
hjms(235789); // → 2 jours 17 heures 29 minutes 49 secondes
hjms(567231); // → 6 jours 13 heures 33 minutes 51 secondes
```

---

## Exercice 2-bis — Conversion de durées (version améliorée)

### Énoncé
Améliorer `hjms` pour que :
- Les valeurs nulles n'apparaissent pas dans l'affichage
- Les valeurs égales à 1 soient au singulier (sans « s »)

### Solution

```javascript
function hjms(totalSecondes) {
  let jours    = Math.floor(totalSecondes / 86400);
  let reste    = totalSecondes % 86400;
  let heures   = Math.floor(reste / 3600);
  reste        = reste % 3600;
  let minutes  = Math.floor(reste / 60);
  let secondes = reste % 60;

  let result = "Cette durée équivaut à ";
  if (jours > 0)    result += `${jours} ${jours === 1 ? "jour" : "jours"} `;
  if (heures > 0)   result += `${heures} ${heures === 1 ? "heure" : "heures"} `;
  if (minutes > 0)  result += `${minutes} ${minutes === 1 ? "minute" : "minutes"} `;
  if (secondes > 0) result += `${secondes} ${secondes === 1 ? "seconde" : "secondes"}`;

  console.log(result.trim());
}

// Exemple
hjms(3621); // → 1 heure 21 secondes
```

---

## Exercice 3 — Classer 3 nombres

### Énoncé
Écrire un programme `troisNombres` qui affiche 3 nombres dans l'ordre croissant.

### Solution

```javascript
function troisNombres(a, b, c) {
  let nums = [a, b, c].sort((x, y) => x - y);
  console.log(`Les nombres dans l'ordre croissant : ${nums[0]} ${nums[1]} ${nums[2]}`);
}

// Exemple
troisNombres(14, 10, 17); // → 10 14 17
```

---

## Exercice 4 — Affichage de motifs (escaliers)

### Énoncé
Afficher un motif triangulaire d'étoiles de taille donnée.

### Solution — a) avec `while`

```javascript
function triangle1(taille) {
  let i = 1;
  while (i <= taille) {
    console.log("*".repeat(i));
    i++;
  }
}
```

### Solution — b) avec `for`

```javascript
function triangle2(taille) {
  for (let i = 1; i <= taille; i++) {
    console.log("*".repeat(i));
  }
}

// Exemple pour taille = 7 :
// *
// **
// ***
// ****
// *****
// ******
// *******
```

---

## Exercice 4-bis — Affichage de motifs (pyramides)

### Énoncé
Afficher une pyramide centrée d'étoiles.

### Solution

```javascript
function pyramide(taille) {
  for (let i = 1; i <= taille; i++) {
    let etoiles = 2 * i - 1;
    let espaces = taille - i;
    console.log(" ".repeat(espaces) + "*".repeat(etoiles));
  }
}

// Exemple pour taille = 7 :
//       *
//      ***
//     *****
//    *******
//   *********
//  ***********
// *************
```

---

## Exercice 5 — Tester si un nombre est premier

### Énoncé
Écrire un programme `Premier` qui teste si un entier positif est un nombre premier.

### Solution

```javascript
function Premier(n) {
  if (n < 2) {
    console.log(`${n} n'est pas un nombre premier`);
    return;
  }
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      console.log(`${n} n'est pas un nombre premier, il est divisible par ${i}`);
      return;
    }
  }
  console.log(`${n} est un nombre premier`);
}

// Exemples
Premier(7);  // → 7 est un nombre premier
Premier(25); // → 25 n'est pas un nombre premier, il est divisible par 5
```

---

## Exercice 6 — Suite de Fibonacci

### Énoncé
La suite de Fibonacci : `u0 = 0`, `u1 = 1`, `u(n+1) = u(n) + u(n-1)`

### Solution — a) `Fibo1` : nième terme

```javascript
function Fibo1(n) {
  let a = 0, b = 1;
  for (let i = 0; i < n; i++) {
    [a, b] = [b, a + b];
  }
  console.log(`Le terme u${n} de la suite de Fibonacci est : ${a}`);
}
```

### Solution — b) `Fibo2` : premier terme supérieur à une valeur

```javascript
function Fibo2(valeur) {
  let a = 0, b = 1, rang = 1;
  while (b <= valeur) {
    [a, b] = [b, a + b];
    rang++;
  }
  console.log(`Le premier terme supérieur à ${valeur} est u${rang} = ${b}`);
}
```

---

## Exercice 7 — Valeur approchée de la racine carrée

### Énoncé
Calculer √A par la méthode de récurrence de Héron :

```
u(n+1) = (1/2) * (u(n) + A / u(n))
```

On cherche le premier terme `u(n)` tel que `|u(n)² - A| < 10⁻⁶`.

### Solution

```javascript
function Raca1(A) {
  let u = A / 2;
  while (Math.abs(u * u - A) >= 1e-6) {
    u = 0.5 * (u + A / u);
  }
  console.log(`Valeur approchée de la racine carrée = ${u}`);
}

// Exemple
Raca1(19.23); // → Valeur approchée de la racine carrée = 4.385202389856321
```

---

##  Conclusion

Ce TD a permis de mettre en pratique les bases fondamentales de JavaScript :

- **Fonctions** : déclaration, paramètres, retour de valeurs
- **Boucles** : `while` et `for` pour les itérations et les motifs
- **Conditions** : `if/else` pour la classification et les tests
- **Arithmétique** : opérations sur les entiers (modulo, division entière) et les réels (approximations)
- **Algorithmes classiques** : conversion d'unités, tri, test de primalité, suite récurrente, méthode numérique

Ces constructions constituent le socle de tout développement JavaScript, aussi bien côté navigateur que côté serveur (Node.js).
