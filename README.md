# Mon Jour — app Apple Watch (watchOS 10+, SwiftUI)

Fusion de Dicton du Jour, Horoscope du Jour et Daily Puzzle en une seule app :
3 rubriques par jour, une série (jours où les 3 sont faites), complications de cadran.

## Arborescence

```
Shared/   → cocher les DEUX cibles (app Watch + extension widget)
  Theme.swift, DayKey.swift, L10n.swift, DailyContent.swift, DailyStore.swift
App/      → cible app Watch
  MonJourApp.swift, HomeView.swift, DictonView.swift, HoroscopeView.swift,
  PuzzleView.swift, ResultView.swift
Widget/   → cible extension widget
  MonJourWidget.swift
```

## Mise en place dans Xcode

1. **Nouveau projet** › watchOS › App, « Watch-only App ».
   Nom : Mon Jour · Bundle ID : `com.michel.garlandat.monjour` · Interface SwiftUI · cible watchOS 10.0.
2. Supprimer `ContentView.swift` et le fichier `…App.swift` générés, puis glisser `App/` et `Shared/`
   dans le projet (« Copy items if needed », cible Watch App cochée).
3. **File › New › Target › Widget Extension** (watchOS). Nom : `MonJourWidget`,
   décocher « Include Configuration App Intent ». Supprimer le fichier Swift généré
   et ajouter `Widget/MonJourWidget.swift` à cette cible.
4. Sélectionner chaque fichier de `Shared/` › inspecteur › Target Membership :
   cocher **Mon Jour Watch App** et **MonJourWidgetExtension**.
5. **Signing & Capabilities**, sur les deux cibles : `+ Capability` › **App Groups** ›
   `group.com.michel.garlandat.monjour`. C'est ce qui permet à la complication de lire la série.
6. Build sur la montre ou le simulateur, puis ajouter la complication depuis l'édition du cadran.

## À remplacer avant soumission

- `DailyContent.dictonsFR/EN` : coller les tableaux de Dicton du Jour (idéalement 365 entrées).
- `horoscopeFR/EN` : textes de Horoscope du Jour. Les 12 phrases actuelles sont des exemples.
- `answersFR/EN` : liste longue de mots de 5 lettres (sans accents, majuscules).
- `allowedFR/EN` : mots de 5 lettres extraits des dictionnaires de Lettres Rami
  (accents retirés), puis passer `strictDictionary = true`.

## Comportement

- Le contenu change à minuit (index du jour depuis le 1er janvier 2026, puzzle n° = index + 1).
- Le puzzle reste dans la langue où il a été commencé, même si on change de drapeau.
- Série : +1 si les 3 rubriques sont faites et que la veille l'était aussi ; sinon on repart à 1.
- Mot mystère : la couronne fait défiler A→Z dans la case active, on touche une case pour la sélectionner,
  ⌫ efface, → passe à la case suivante, « Valider » apparaît quand les 5 lettres sont remplies.

## Note pour la revue App Store (Resolution Center / App Review Information)

> Mon Jour regroupe en une seule app des fonctions précédemment soumises séparément
> (Dicton du Jour, Horoscope du Jour). Conformément aux guidelines 4.2 et 4.3, nous avons
> consolidé ces contenus dans une expérience quotidienne unique : dicton, horoscope et un
> jeu de mots joué à la Digital Crown, avec suivi de série et complications de cadran.
> Les anciennes fiches seront retirées.

Code non compilé ici (environnement Linux) : premier build à vérifier dans Xcode.
