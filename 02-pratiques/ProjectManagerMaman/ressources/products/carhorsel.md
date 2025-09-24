# Carhorsel

Nous avons pensé à carhorsel en partant du constat que la plus grosse perte de temps pour les saddle fitter est la prise de rdv et l'organisation des tournées surtout en cherchant à optimiser les trajets.
Pour ce projet, je suis la CEO et je me suis chargée de toute l'analyse, recueil du besoin ainsi que des questionnaires utilisateurs et recherches business + UX (maquette figma et développement du front), alors que mon mari a un rôle de CTO et a fait les choix d'architecture et le développement de tout le produit.

## Prise de rdv

Cavalier cherche un professionnel exerçant le métier M pour son cheval Ch situé à l'écurie E dans la ville V.
Il se connecte à son compte.
Il se rend sur la page de recherche et selectionne le métier recherché ainsi que le cheval pour lequel il effectue la recherche (un cavalier peut avoir plusieurs chevaux à plusieurs endroits différents). Si une tournée susceptible de l'intéresser est disponible, elle apparait dans les suggestions tout en haut. Sinon les professionnels se déplaçantdans le secteur apparaissent par ordre de distance à l'écurie. Si un professionnel a déjà été consulté par le cavalier ou fait partie de ses favoris, il est mis en avant dans les résultats de recherche.
2 possibilités :
- Une tournée correspond à ses besoins : le cavalier s'inscrit à la tournée et attend la connfirmation du pro.
- Aucune tournée ne correspond : le cavalier choisit un professionnel et demande un rdv avec lui. Il précise ses préférences horaires et peut ajouter des disponibilités/indisponibilités ponctuelles. Le rdv sera généralement pris à partir d'une semaine après la demande (réglable) sauf pour les rdv "urgence" que le pro doit autoriser.

La demande de rdv passe par le scheduler qui cherche à optimiser les journées et trajets pour les rdv du professionnel, avant d'être proposé au professionnel. Le pro voit une nouvelle tâche "vérifier le rdv" apparaitre dans son application, reçoit une notification push et un récapitulatif des tâches à effectuer une fois par jour par email. 
Le cavalier reçoit un récapitulatif de la demande par email (il n'a pas encore rdv).

Le scheduler propose un créneau au professionnel.
Le professionnel est relancé régulièrement (quotidiennement jusqu'à validation du rdv).
Lorsque le rdv est validé par le pro, le cavalier est informé par email, notification push et sur l'application.

Le rdv peut être annulé jusqu'à 72h avant la date (paramètre avancé).
Un rappel de rdv est envoyé par email au cavalier une semaine avant, trois jours avant (spécifiant que c'est le dernier délai pour annuler), ainsi que la veille du rdv. Le jour J une notification push s'affiche 2h avant le RDV.
Le professionnel reçoit chaque soir un mail récapitulatif avec les tâches à réaliser ainsi que le planning pour le lendemain. Une fois par semaine, il reçoit un mail récapitulatif pour la semaine.
A tout moment le professionnel peut consulter les tâches et les rdv depuis l'application.

Afin de valider la prise de rdv et d'éviter les annulations de dernière minute, le professionnel peut demander l'empreinte bancaire. Il peut aussi se faire payer la séance directement depuis l'application.

Le jour du rdv, le professionnel a accès à une page récapitulant le trajet et les rdv de la journée. En cliquant sur trajet, il est automatiquement envoyé dans son application gps par defaut. En cas de retard, un bouton permet d'informer automatiquement le client suivant.

## Scheduler

### Description business

Le scheduler est le cœur de notre produit, ce qui nous différencie de nos concurrents. Il apporte de l'intelligence à la prise de RDV en facilitant l'organisation et la planification des tournées du professionnel. Le but est d'optimiser automatiquement les trajets et les journées du professionnel en tenant compte des demandes des clients.

### Intérêt
La prise de RDV et l'organisation d'une tournée est l'une des tâches administratives les plus chronophages pour le professionnel du bien-être équin ambulant. Classiquement, le déroulé est le suivant :
1) Le client contacte le professionnel par téléphone, message ou email afin de demander des disponibilités.(temps estimé 5-10min
)
2) Le professionnel répond et propose des créneaux si compatibilité avec sa zone de déplacement et ses rdv déjà prévus. Ceci suppose une recherche quant à la localisation de l'écurie, une vérification dans le calendrier quant à la proximité avec d'autres RDV déjà fixés et la vérification de la possibilité d'ajouter éventuellement un RDV dans le planning pré-établi. (temps estimé 5-30min)
3a) Un créneau est disponible : le professionnel répond au client avec une proposition. (temps estimé 5-10min)
4a) Le client valide ou non la proposition. (temps estimé 5-10min)
3b) Aucun créneau n'est disponible : les raisons sont multiples mais souvent c'est parce que le professionnel ne se déplace à cette distance qu'à partir d'un certain nombre de clients. Il propose alors au client de chercher des cavaliers intéressés par cette tournée afin de l'organiser. Il publie une proposition sur ses réseaux par exemple, et demande au client de faire de même. Ils se laissent un délai de X jours avant de se tenir au courant de l'évolution de la situation. (temps estimé 20min-1h)
4b) Le professionnel propose un créneau au client.(temps estimé 5-10min)
5b) Le client valide ou non la proposition. (temps estimé 5-10min)

D'éventuelles boucles sont possibles en (a) ou (b). Sans boucle, en moyenne, un professionnel passe entre 20min et 1h à fixer un RDV simple, ou entre 40 min et 2h pour un RDV dont la tournée est à organiser.

Avec le scheduler, le déroulé est le suivant :
1) Le client désire le professionnel désiré et communique ses besoins et ses disponibilités. 
2) Le scheduler tente de planifier le RDV dans le planning du professionnel, en tenant compte des contraintes temporelles et géographiques.
3a) Un créneau est disponible : le scheduler propose la planification au professionnel pour qu'il valide ce RDV.(temps estimé 1-10min)
4a) Un message est envoyé au client avec la proposition de RDV.
3b) Aucun créneau n'est disponible : le scheduler prépare une publication pour les réseaux afin de mettre en avant une future tournée ; la tournée est mise en avant sur la page de recherche de l'application et le client est tenu au courant régulièrement de l'avancée de l'organisation.
temps estimé 1-2 min
4b) Le nombre de clients minimum pour la tournée est atteint. Le professionnel valide la proposition du scheduler.(temps estimé 1-15 min)
5) Le client valide ou non la proposition.

D'éventuelles boucles sont possibles en (a) ou (b). Sans boucle,en moyenne, un professionnel passe en 2 et 17 minutes à fixer un RDV avec l'application.

Juste avec la fonctionnalité du scheduler, le professionnel gagne entre 1h18min et 1h43min pour planifier un RDV.

Echanges 
CAS SIMPLE CLIENT (C) - SCHEDULER (S) - PROFESSIONNEL(P)
C--> S : Le client fait une demande de RDV et communique ses disponibilités.
S--> S : Le scheduler cherche un créneau possible dans l'agenda du professionnel.
S--> P : Le scheduler envoie le créneau au professionnel.
P--> S : Le professionnel valide la proposition.
S--> C : Le RDV est proposé au client.
C--> S : Le client valide le RDV.
S--> S : Le scheduler met à jour l'agenda du professionnel.

CAS COMPLEXE CLIENT (C) - SCHEDULER (S) - PROFESSIONNEL(P)
L'écurie se situe à une certaine distance du professionnel.
C--> S : Le client fait une demande de RDV et communique ses disponibilités.

## Modèle économique

Sur abonnement des professionnels. Tarif de base 40€HT/mois (basé sur une analyse de la concurrence + des tarifs de secrétaires/assistantes). Possibilité d'enrichir l'offre avec des services complémentaires et donc d'abonnement premium (par exemple lors de l'ajout de la llm, la tarification sera probabalement à revoir pour compenser les coûts, ou bien la possibilité de paiement en ligne)





