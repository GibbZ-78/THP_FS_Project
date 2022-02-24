# NOM DU PROJET (non-définitif)

## 1. Présentation
Le nombre d'organismes de formation, de cursus spécialisés et autres [MOOC / POOC / SPOC...](https://www.journaldunet.com/management/formation/1180044-mooc-cooc-spoc-sooc-quelles-differences/) ont explosé sur la dernière décennie. En parallèle, leur audience a, elle aussi, été multipliée par des chiffres que beaucoup d'autres secteurs rêveraient d'avoir.
Pourtant, entre les plateformes e-Learning d'entreprise (LMS, LcMS, modules "Training" de SIRH...) et quelques autres options un peu trop fouillées comme [Moodle](https://moodle.org/) (plutôt destiné aux universités & Co, _in fine_), il n'existe que très peu de plateformes en [marque blanche](https://fr.wikipedia.org/wiki/Marque_blanche), encore moins faisant la part belle au _peer-learning_ et à toute la richesse qu'il eut apporter, lorsqu'il est bien utilisé et mis en place.

Du coup, notre projet est [simple, basique](https://www.youtube.com/watch?v=2bjk26RwjyU) (Merci, Orel' !) : concevoir, instancier, coder et vous proposer une plateforme à la THP... Mais réalisée par des alumni et proposable en marque blanche à des entreprises ou institutions comme THP. 
Aucune vélléité à la [Iznogoud](https://www.dargaud.com/bd/iznogoud/iznogoud-tome-1-le-grand-vizir-iznogoud-bda5018560) mais une envie forte et partagée de notre _core team_ d'explorer le sujet "plateforme web d'apprentissage" :wink:. 

## 2. Parcours utilisateur
Le parcours "apprenant" :bowtie:, globalement, vous le connaissez puisque vous le vivez encore présentement : 
- Découverte, via une landing page assortie d'une recherche à filtres, des cursus, des thématiques, des modalités pédagogiques et administratives, etc.
- Inscription (tu sais, le fameux bouton "Sign Up / Inscription" suivi de ce satané formulaire hyper long à remplir... :wink:) 
- Connexion (là, on est plus sur le "Sign in / Connexion" :smile:), moins douloureux et qui permet enfin d'accéder au contenu de formation
- Depuis un "dashboard / tableau de bord" de l'apprenant, l'utilisateur peut s'inscrire à certains curriculums, choisir (ou suivre de force) les thèmes qui l'intéressent, passer des quizzs en fin de "cours", progresser... ou essayer encore.

Mais, au-delà du (de la) moussaillon(ne), il faut imaginer qu'une énorme part de la plateforme, et donc du code lié, va devoir faciliter la gestion quotidienne de la plateforme par un(e) ou plusieurs administrateur(trice)s :sunglasses:, des contenus de formation et - évidemment - des apprenants... Ces emm*****eur(euse)s... Empécheur(se)s de tourner en rond, qui n'arrêtent pas de poser des questions, remonter des bugs ou demander de nouvelles fonctionnalités qu'ils (elles) n'utiliseront pas.

## 3. Concrètement et techniquement

### 3.1. En synthèse
1. Côté technique : 
  1. Une BD postgreSQL parce que c'est quand même un DBMS à la fois puissant et robuste :muscle:.
  2. Un back-end basé sur Rails... Pas le plus robuste des frameworks qu'on ait vu, pour le coup, mais avec du bon quand même et, surtout, une communauté qui l'alimente en gems sans cesse renouvelées et :heavy_plus_sign: / :heavy_minus_sign: maintenues :bug:.
  3. Un front avec un peu de Bootstrap mais aussi une superbe sur-couche pour ne pas ressembler à toutes les apps Meta.
  4. Une pincée de Javascript, assurément, pour ajouter de la vie dans la plateforme et éviter les validations un peut trop lourde à base de routage HTTP
2. Sur le pan "business" et processus :
  1. Quelques exemples de contenus pédagogiques, développés (ou repiqués :shipit:) pour l'occasion
  2. Un système de souscription (inscription et paiement, le cas échéant) puis de connexion donnant des accès particuliers aux membres
  3. En symétrie, côté "back-office", un tableau de configuration et gestion, dédié aux administrateur(trice)s (_e.g._ création de modules de formation, organisation des modules en cursus, gestion des apprenants, de leur progression, de leurs évaluations...) ; en sus, quelques infos utiles au pilotage (ex. nombres d'apprenants par typologie de contenu, par niveau d'avancement, par cursus... Mais aussi, des "données économiques" : chiffre d'affaire global, par cursus...)

### 3.2. Base de données
Bien pensée, bien remplie, évidemment : pourquoi cette question :smile: ?

Plus sérieusement, le modèle central n'est pas trop compliqué et devrait vous rappeler quelque chose :
- Des "users" :
  - certains seront spécialisés en "apprenants" (_i.e._ users inscrits), 
  - d'autres seront juste des "prospects" (_i.e._ infos récupérées via la landing page et que nous ne manquerons pas de spammer avec des offres commerciales bienveillantes :japanese_ogre:)
  - d'autres encore auront un rôle de "référent / enseignant" (à voir comment on l'utilisera par la suite...)
  - enfin, un petit nombre d'élu(e)s bénéficieraient de l'enviable statut d'administrateur(trice) : le God mode de la plateforme, en quelques sortes :sunglasses:.
- Des contenus pédagogiques structurés en cours / modules / cursus
- Des inscriptions qui feront le lien entre certains des utilisateurs évoqués et leurs apprentissages
- A cel s'ajouter sûrement quelques "vérues", du genre _like_ et commentaires à propos des cours

### 3.3. Front
Déjà détaillé plus haut, en 3.1 : du Bootstrap revampé, du javascript (vanilla), de belles images avec un camaïeu top hype, et le tour est joué !

### 3.4. Backend
Hormis Rails et les quelques gems Ruby / RoR déjà étudiées ("devise" pour lle sessionning, "dotenv-rails" pour gérer d'éventuelles infos sensibles à stocker, "stripe" pour... permettre les paiements via Stripe, etc.) on a pas encore réfléchi jusqu'à quel point on pourrait / voudrait / saurait _pimper_ notre PLP... Pardon, _Peer Learning Platform_ mais on compte sur toi pour nous y aider. A ça et sur plein d'autres trucs ! C'est de la définition initiale du besoin et de la cible (ambitieuse mais raisonnable) que découleront les recherches et choix des "technos" à déployer.

### 3.5. Nos besoins techniques
En gros, on a déjà un noyau d'équipe (un "seed" :wink:) constitué de :
- Wilfried PAILLOT, _The Gardener Coder_ (et vice-versa) qui cultive le code, le fait grandir et sait tout faire pousser, en particulier du PHP, du Ruby et du Bootstrap
- Yassine ROCHD, _The cypher_, notre "homme du chiffre", expert en _Private Equity_, en _Real Estate_ et, à ses heures perdues, body builder émérite et codeur Ruby pour le plaisir
- David NGUYEN, _The Librarian_, une véritable encyclopédie vivante du code, le [Leo Getz](https://getyarn.io/yarn-clip/5b79e150-5544-465e-b6cc-29b6012f8a43) de la syntaxe ; la seule documentation qui parle et, en même temps, a assez de détente pour te mettre une trempe au volley :soccer: (OK... c'est un ballon de foot mais y'a pas d'emoji "Volley" dans la bibliothèque Markdown :cry:)

## 4. La version minimaliste mais fonctionnelle qu'il faut avoir livré la première semaine
Tout ça reste à définir mais on peut imagine, au bout de ces quelques jours, d'avoir, en plus d'une "landing", les pages et fonctionnalités de base de consultation, modification (selon le type de profil), création (idem) et suppression (idem²) des principaux "objets" du modèles : 
- les "users" des différents types
- les cours assemblés en modules et/ou cursus
- les inscriptions des premiers aux seconds
- 1 ou 2 pages d'info (lorsqu'on est pas connecté, par exemple)
- 1 tableau de bord de l'apprenant et celui d'administration

Le tout avec un look acceptable... ça vous irait comme ça ?

## 5. La version que l'on présentera aux jury
En plus de finaliser les fonctionnalités et le look du MVP de la semaine 1, on pourrait discuter d'ajouts comme

## 6. Notre mentor
Qui est ton mentor ?
