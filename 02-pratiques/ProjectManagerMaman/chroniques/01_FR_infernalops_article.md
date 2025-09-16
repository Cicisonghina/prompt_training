# Nuits InfernalOps : Quand mon bébé devient l'admin sys de mes cauchemars

## 1. Alerte rouge à 2h43

L'incident s'est déclaré à 2h43. Pas de sirène, pas de notification Slack, juste ce cri strident qui traverse l'appartement comme un ping timeout critique. Je me redresse dans le lit, les yeux encore collés de sommeil - ou plutôt des 47 minutes que j'avais réussi à grappiller depuis le dernier réveil- et j'entends dans ma tête cette très reconnaissable musique de boss qui tient en haleine.

Mon premier réflexe ? Checker mon téléphone. Aucune alerte PagerDuty sur mes anciens projets. Juste mon petit administrateur système de 9 mois qui vient d'escalader un incident P0 : "Service sommeil indisponible, intervention immédiate requise".

À côté de moi, mon mari continue de dormir. Profondément. Comme un serveur Windows qui refuse de redémarrer même quand on appuie sur le bouton power. J'essaie de le secouer : "Chéri... le bébé..." Il marmonne quelque chose qui ressemble vaguement à "Mmh d'accord j'y vais" puis retombe dans son coma informatique.

Soupir. *git stash* de ma propre existence, je sors du lit.

## 2. Diagnostic initial : la semaine des Pokémon

Cette nuit-là n'était que la énième itération d'un bug récurrent qui dure depuis plus de dix jours. Le pattern est toujours le même : réveil toutes les 2h maximum, escalade automatique vers moi (qui ai pourtant configuré une rotation d'astreinte avec mon mari), et solution temporaire qui ne tient jamais.

La semaine précédente, première hypothèse diagnostic : rhinopharyngite. Le pédiatre confirme lundi : "C'est une grosse rhino, mais ça ne dure qu'une semaine maximum." Parfait, on a identifié la root cause, le fix va arriver tout seul. 

Mardi, bébé retourne à la crèche. La nuit est épouvantable mais bon, c'est la rhino, "c'est bientôt fini". Mercredi, la situation se dégrade. En plus des réveils constants, nouvelle alerte : fièvre détectée. Jeudi, même scénario.

Vendredi, retour chez la pédiatre pour un post-mortem d'urgence. Verdict : "À la crèche, il a attrapé une laryngite. Un nouveau bug, indépendant du premier."

J'ai regardé la docteure avec cet air que tous les DevOps connaissent bien : celui qu'on a quand le client nous dit "Mais vous aviez dit que c'était réparé !" alors qu'un tout nouveau service vient de tomber.

Apparemment, la crèche, c'est comme un environnement de staging mal isolé : ton code marche, mais dès qu'il entre en contact avec les autres applications, il récupère tous leurs bugs. Mon fils collectionne les virus comme des Pokémon. _Gotta Catch 'Em All_. Et moi, je prie pour qu'il n'y ait plus de pokeball en circulation.

## 3. Mon runbook de survie nocturne

Après des mois d'incidents en production, j'ai développé mes propres procédures d'urgence :

### Procédure standard (70% des cas)
1. **Détection** : Cri → Timer automatique de 30 secondes (parfois il se rendort seul)
2. **Escalade niveau 1** : Tentative de réveil du mari (succès : 20%)
3. **Escalade niveau 2** : Intervention directe de l'admin principal (moi)
4. **Fix temporaire** : Migration vers son lit + déploiement du service "tétée"

### Procédure dégradée (quand papa intervient enfin)
Mon mari a cette capacité fascinante : il peut se traîner hors de notre lit, atterrir dans celui du bébé, et être déjà rendormi avant même que sa tête touche l'oreiller. Comme un serveur qui passe en mode hibernation instantanément. 

Le problème ? Mon bébé me voit manifestement comme un frigo sur pattes. Quand c'est moi qui interviens, il détecte automatiquement la disponibilité du service premium et refuse catégoriquement les solutions de contournement. Papa = mode câlin basique suffisant. Maman = accès direct aux ressources alimentaires requis. Difficile de refuser l'accès quand ton utilisateur principal pleure à 3h du matin et que tu es littéralement son infrastructure critique. Mais ça ne m'aide pas vraiment à implémenter mon projet de sevrage.

### Cas critique : double incident
Le pire scénario, c'est quand les deux systèmes tombent simultanément. Mon grand (27 mois) a un sommeil aussi fragile que le mien - un vrai legacy system sensible aux interférences. Quand il se réveille aussi (souvent à cause d'un "débordement" de couche qui a contaminé son environnement), il faut faire du triage d'urgence.

Priorité 1 : Éviter la propagation de l'incident au deuxième enfant  
Priorité 2 : Restaurer le service "sommeil" du premier  
Résultat : Minimum une heure de câlins avant stabilisation du système. Et moi, impossible de dormir avec lui - mon cerveau reste en mode monitoring.

## 4. Les vraies leçons du DevOps familial

Chez ManoMano, quand j'organisais des GameDays avec plus de 50 participants, je pensais maîtriser la gestion de crise. Erreur fatale. Les vrais incidents de production, c'est chez moi, la nuit, quand tous les systèmes critiques décident de planter en cascade.

**Différences notables entre l'astreinte tech et l'astreinte parentale :**

| Astreinte tech | Astreinte parentale |
|---|---|
| Rotation équipe | Mama-ops 24/7 |
| Runbook documenté | Improvisation totale |
| Post-mortem optionnel | Questionnement existentiel obligatoire |
| Café disponible | Thé froid à volonté |
| Fin d'incident = retour au lit | "Incident" suivant dans 47 minutes |

**Ce que j'ai appris :**

La **patience** n'est pas une soft skill. C'est une ressource système limitée qui se vide à chaque intervention et se recharge très lentement (idéalement pendant les siestes, mais voir conditions d'utilisation).

Le **load balancing** familial ne marche que si tous les membres de l'équipe ont la même sensibilité aux alertes. Spoiler : ce n'est jamais le cas.

Les **incidents récurrents** finissent toujours par se résoudre... mais généralement quand tu as arrêté d'espérer. Et souvent par eux-mêmes, sans que tu comprennes pourquoi.

## 5. Monitoring avancé : métriques qui comptent

Oubliez vos dashboards Grafana. Mes vraies métriques critiques :

- **MTTR** (Mean Time To Recovery) : Temps moyen pour rendormir un bébé (objectif : <20 min, réalité : ça dépend de la lune)
- **Disponibilité sommeil** : Pourcentage de nuit sans incident (SLA actuel : 0%, et c'est optimiste)
- **Alerte fatigue** : Nombre d'interventions avant que maman.exe ne réponde plus
- **Dette technique** : Accumulation de tâches ménagères reportées à cause des incidents nocturnes

## 6. Post-mortem permanent

Alors que j'écris ces lignes, les petits anges dorment bien sagement depuis longtemps... Non je plaisante. Il est 22h, mon thé refroidit à côté de mon clavier (comme toujours), et mon mari essaie héroïquement d'endormir les deux frères dans la chambre d'à côté. J'entends des négociations complexes avec le grand ("Non, on ne va pas voir les camions maintenant") et des tentatives de debug vocal sur le petit ("Chut chut chut... allez...").

Pour la première fois de la journée - et probablement la seule de la nuit - j'ai les mains libres ET l'esprit disponible simultanément. Un miracle d'architecture système que je ne vais pas gâcher. Alors je me demande : est-ce que ça va un jour se stabiliser ?

En tant qu'ex-Chaos Engineer, je devrais apprécier l'imprévisibilité. En théorie, ces incidents nocturnes rendent mon système familial plus résilient. En pratique, ils me rendent juste plus créative dans l'art de fonctionner avec 3h de sommeil cumulé.

Finalement, un bébé qui pleure, c'est comme un utilisateur frustré qui spamme le support sans pouvoir décrire son bug. Ma mission : traduire ces cris en user stories actionnables.

Mais il y a quelque chose de fascinant dans cette expérience : jamais dans ma carrière tech je n'ai eu d'utilisateurs aussi exigeants, aussi imprévisibles, et pourtant aussi... attachants. Quand ton serveur plante, tu le redémarres. Quand ton bébé pleure à 3h, tu le prends dans tes bras et tu réalises que c'est exactement là que tu veux être.

Même épuisée. Même avec un thé froid. Même en sachant que l'alerte suivante arrivera dans quelques heures.

## 7. Prochaine release

La version 2.0 de mon système familial est prévue pour... aucune idée. Les enfants ne respectent jamais les roadmaps, et c'est tant mieux. En attendant, je continue d'itérer, de débugger à la volée, et d'apprendre que la meilleure infrastructure, c'est parfois juste une maman qui sait faire des câlins à 3h du matin.

**Prochainement dans cette série :** "Debug d'une jument stressée : mes premières leçons d'empathie utilisateur" - parce qu'après les bébés, je vais vous raconter comment Vazy m'a appris à comprendre les besoins non-exprimés.

---

*Et vous, c'est quoi votre pire incident de production familiale ? Partagez vos runbooks de survie parentale en commentaire - on est tous dans la même astreinte ! 🍵*

---

**À propos de Cecilia** : Ex-Chaos Engineer chez ManoMano, ex-ingénieure Cloud chez Ubisoft, future Product Owner et maman de deux garçons. Entre GameDays tech et nuits blanches, j'ai découvert que les vrais systèmes critiques portent des pyjamas. Cette série explore comment mes compétences techniques m'aident (ou pas) à survivre à la parentalité. 🍵