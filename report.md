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

## Semaine 3

### Réponse

Temps estimé : 45 minutes

Temps passé : 1h40

#### Notes

`computed` = `ref`+ `watch`

Générique : pour que la fonction puisse prendre différents types et comprendre ce qu'elle doit retourner.

```
function doubler<T>(value: T): Bleu<T> {
  if (typeof value === "string") {
    return value + value;
  } else {
  return value \* 2;
  }
}

interface QuestionText<T> {
  value: T
}

doubler("qwe") // "qweqwe"
doubler(3) // 6
doubler(5)
```

```
const answer = computed<string>(() => {
  return Object.values(props.answer).sort().toString()
})
```

-> utiliser computed pour les réponses correctes au lieu de vérifier la condition dans watch pour éviter que answer recalculé à chaque que l'utilisateur change de valeur.

~~`answer="[2, 3]"`~~ `:answer="['2', '3']"` -> pour que ce soit interpreté comme une liste de strings et pas un seul string

#### Question

À quoi sert l'option immediate: true dans le watch ? Que se passe-t-il si on l'enlève ou si on met immediate: false ?

A mettre à jour les `correctAnswers` quand les variables dedans changent.

### Score

Temps estimé : 45 minutes

Temps passé : 15 minutes

#### Notes

Anciennes parties enlevées

```
function submit(event: Event): void {
  event.preventDefault()
  const count = ref<number>(0)

  const n_questions = 3
  if (q1.value === 'a11') {
    count.value += 1
  }
  if (
    Object.values(q2.value).sort().toString() ===
    ['a21', 'a24'].sort().toString()
  ) {
    count.value += 1
  }
  if (q3.value === 'a32') {
    count.value += 1
  }
  if (filled.value) {
    alert(`Score : ${count.value}/${n_questions}`)
    if (count.value === n_questions) {
      alert(`Bravo !`)
    }
  }
}
```

```
<button
      class="btn btn-primary"
      :class="{ disabled: !filled }"
      type="submit"
    >
      Terminer
    </button>
```

`<form @submit="submit">`

## Semaine 4

### Etats

Temps estimé : 30 minutes

Temps passé : 45 minutes

#### Notes

état, c'est fill et empty ou correct et wrong ?
peut avoir deux états ?

#### Questions

```
model.value =
  value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;
```

=

```
if (value.value === props.answer) {
  model.value = QuestionState.Correct
} else {
  model.value = QuestionState.Wrong
}
```

Donc on pourrait aussi écrire

```
model.value = newValue === null ? QuestionState.Empty : QuestionState.Fill
```

à la place de

```
if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
```

### Boutons

Temps estimé : 30 minutes

Temps passé : 30 minutes

#### Notes

C'est quoi la différence entre `<button type="submit">` et `<button @click="submit">` ?

Nommer la variable `newModel` au lieu de `newValue` dans watch model serait plus logique ?

- `watch` sur `value` : actualiser la valeur de model quand value change
  - Quand l'utilisateur input une valeur -> l'état devient Fill
- `watch` sur `model` : actualiser la valeur de value quand model change
  - Quand on appelle la fonction reset, on change le model en Empty et on veut actualiser la valeur à la valeur de défaut
  - Quand on appelle la fonction submit, on change le model en Submit et on veut actualiser la valeur à Correct ou Wrong

model : état

value : input de l'utilisateur

- `Empty` : la question n'a pas été répondue.
- `Fill` : la question a été répondue, mais pas été soumise pour correction.
- `Submit` : la question a été soumise pour correction, mais pas encore corrigée.
- `Correct` : la question est corrigée et la réponse est juste.
- `Wrong` : la question est corrigée et la réponse est fausse.

### Réponses immuables

Temps estimé : 5 minutes

Temps passé : 5 minutes
