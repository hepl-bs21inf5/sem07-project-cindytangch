# Projet

Raccourcis VScode : Cmd + Shift + P

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

- Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?
  - Appel de la fonction `submit`

> - Qu'est-ce qu'un `v-model` ?

>  - `v-model` peut être utilisé sur un composant pour implémenter une liaison à double sens.
>  - https://fr.vuejs.org/guide/components/v-model

- À quoi sert le `:class="{ disabled: !filled }"` ?
  - On ne peut pas appuyer sur le bouton Terminer si pas toutes les questions sont remplies.
