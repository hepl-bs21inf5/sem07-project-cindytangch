# Projet

Raccourcis VScode : Cmd + Shift + P

`npm run dev`

## Syntaxe

Déclaration variables :

`const count = ref<number>(0)`

`const q1 = ref<string | null>(null)`

`const filled = computed<boolean>(() => ...,)`

Opérateurs logiques :

`===`, `!==`, `&&`, `||`, `!`

## Semaine 1

### Vue.js

Temps estimé : 10 minutes

Temps passé : 10 minutes

### Bootstrap

Temps estimé : 15 minutes

Temps passé : 15 minutes

### Quiz

Temps estimé : 1h30

Temps passé : 2h

Fichier : `QuizForm.Vue`

#### Notes

Quand on appuie sur Terminer, on passe à la prochaine question ?

Un bouton après chaque question ?

Score : compteur / nombre total de questions

Comment faire un compteur avec `const`?

function reset : juste remettre les values à null ?

icons -> App.vue, `<i class="..."></i>`, https://icons.getbootstrap.com/

#### Questions

`main.ts`: importer les librairies externes (bootstrap) et internes (autres fichiers du repo)

`main.css`: personaliser les styles (couleurs, ...)

`App.vue`: html de la structure globale

> `router/index.ts` : ??

`AboutView.vue` : html de la page "about"

`HomeView.vue` : html de la page "home"

`QuizForm.vue` : le fonctionnement du quiz sur la page "home"

> - Quelles sont les similarités et les différences entre `ref` et `computed` ?
>   - `ref` est fixe et `computed`varie ?
>   - Comment implémenter le compteur ?
>   - _Ici, on peut utiliser un let pour la variable._

- Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?
  - Appel de la fonction `submit`

> - Qu'est-ce qu'un `v-model` ?
>   - `v-model` peut être utilisé sur un composant pour implémenter une liaison à double sens.
>   - https://fr.vuejs.org/guide/components/v-model
>   - _ref est une variable "classique", computed est une variable qui dépend d'autres variables._

- À quoi sert le `:class="{ disabled: !filled }"` ?
  - On ne peut pas appuyer sur le bouton Terminer si pas toutes les questions sont remplies.

## Semaine 2

### QuestionRadio

Temps estimé : 45 minutes

Temps passé : 55 minutes

#### Notes

Dans quel fichier il faut importer `QuestionRadio.vue`?

expressions JavaScript (interprétées)

`\` avant `'`

des fois VScode ne trouve pas le fichier à importer et le souligne en rouge mais si le programme marche c'est ok

Attention, il faut garder le `<form @submit="submit">`pour appeler la fonction submit.

Dans `<script>` ce sont plus ou moinss les inputs et dans `<template>`ce sont les outputs.

#### Questions

Quelle est la différence entre un prop et un modèle (v-model) ?

### QuestionText

Temps estimé : 30 minutes

Temps passé : 35 minutes

#### Question

Comment rendre la propriété placeholder optionnelle ?

- enlever `q4.value !== null` dans le booléen `filled`

### API

Temps estimé : 30 minutes

Temps passé : 15 minutes

### QuestionCheckbox (bonus)

Temps estimé : 30 minutes

Temps passé : 1 heure

#### Notes

Comment comparer deux tableaux ?

`if (Object.values(q2.value).sort().toString() === ['a21', 'a24'].sort().toString())`

changer la déclaration du type : `const model = defineModel<string[]>()`
