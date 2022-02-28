# NOM DU PROJET (nom non-définitif :wink:)

## 1. Présentation
Sur la dernière décennie, le nombre d'organismes de formation, de cursus spécialisés et autres [MOOC / POOC / SPOC...](https://www.journaldunet.com/management/formation/1180044-mooc-cooc-spoc-sooc-quelles-differences/) a littéralement explosé, mettant le [SOOC](https://www.journaldunet.com/management/formation/1180044-mooc-cooc-spoc-sooc-quelles-differences/) dans le milieu de la formation. En parallèle, leur audience a, elle aussi, été multipliée par des chiffres que beaucoup d'autres secteurs rêveraient de pouvoir afficher.
Pourtant, entre les suites e-Learning d'entreprise (LMS, LcMS, modules "Training" de SIRH...) et quelques rares alternatives un peu trop fouillées comme [Moodle](https://moodle.org/) (plutôt destiné aux universités & Co, _in fine_), il n'existe que très peu de plateformes faisant la part belle au _peer-learning_ et à toute la richesse qu'il peut apporter, lorsqu'il est bien utilisé, mis en place et animé.

Du coup, notre projet est [simple, basique](https://www.youtube.com/watch?v=2bjk26RwjyU) (cace-dédi à Orel' !) : concevoir, instancier, coder et vous proposer une plateforme à la THP... Mais réalisée par des alumni et proposable en marque blanche à des entreprises ou institutions de formation souhaitant déployer à l'échelle le "Distant Peer-Learning" ou DPL (Et PAF ! Un nouvel acronyme dans le paysage audiovisuel français...Blague télévisuelle inside :tv:). 
Ne voyez là aucune vélléité à la [Iznogoud](https://www.dargaud.com/bd/iznogoud/iznogoud-tome-1-le-grand-vizir-iznogoud-bda5018560) mais plutôt une envie forte et partagée de notre _core team_ d'explorer le sujet "plateforme web d'apprentissage" :wink: plutôt qu'un clône de LBC, Kayak & Co. 

## 2. Parcours utilisateur
Le parcours d'un(e) "apprenant(e)" :princess: :bowtie:, globalement, vous le connaissez puisque vous le vivez encore présentement au quotidien : 
- Découverte, via une landing page assortie d'une recherche à filtres, des thématiques, des cursus liés, des modalités pédagogiques et administratives, des conditions tarifaires, etc.
- Inscription (tu sais, le fameux bouton "Sign Up" suivi de ce satané formulaire hyper long et toujours identique à remplir... :wink:) 
- Connexion (là, on est plus sur le "Sign in" :smile:, moins douloureux et qui permet enfin d'accéder au contenu de formation tant convoité)
- Depuis un "dashboard / tableau de bord" de l'apprenant(e), l'utilisateur(trice) peut s'inscrire à certains curriculums, choisir (ou suivre de force) les thèmes qui l'intéressent, passer des quizz en fin de "cours", progresser... ou essayer encore :  
  
[!["Do you want to play again?"](https://img.youtube.com/vi/dqhSpIpOFco/mqdefault.jpg)](https://youtu.be/dqhSpIpOFco?t=18s).  
  
Mais, au-delà du (de la) moussaillon(ne), il faut imaginer qu'une énorme part de la plateforme, et donc du code lié, va devoir faciliter la gestion quotidienne de la plateforme par un(e) ou plusieurs administrateur(trice)s :sunglasses: :neckbeard: : 
- des contenus de formation 
- des inscriptions
- et - évidemment - des apprenants... Ces emm*****eur(euse)s... Empécheur(se)s de tourner en rond, qui n'arrêtent pas de poser des questions, remonter des bugs ou demander de nouvelles fonctionnalités qu'ils (elles) n'utiliseront pas.

## 3. Concrètement et techniquement

### 3.1. En synthèse
1. Côté technique :  
  + Une BD postgreSQL parce que c'est quand même un DBMS à la fois puissant et robuste :muscle:.  
  + Un back-end basé sur Rails... Pas le plus robuste des frameworks qu'on ait vu, pour le coup, mais avec du bon quand même et, surtout, une communauté qui l'alimente en gems sans cesse renouvelées et :heavy_plus_sign: / :heavy_minus_sign: maintenues :bug:.  
  + Un front avec un peu de Bootstrap mais aussi une superbe sur-couche pour ne pas ressembler à toutes les apps Meta.  
  + Une pincée de Javascript, assurément, pour ajouter de la vie dans la plateforme et éviter les échanges de formulaires et validations un peu _relous_ à base de routage HTTP.
2. Sur le pan "business" et processus :  
  + Des pages "infomerciales", avec les cursus proposés, les tarifs, la philosophie de la plateforme, les tarifs, des contacts, les infos sur la team...
  + Quelques exemples de contenus pédagogiques (légers, hein, on a pas 10 mois devant nous !), développés pour l'occasion ou inspirés d'existants intéressants
  + Un système de souscription (inscription et paiement, le cas échéant) puis de connexion donnant des accès particuliers aux membres  
  + En symétrie, côté "back-office", un tableau de configuration et gestion, dédié aux administrateur(trice)s (_e.g._ création de modules de formation, organisation des modules en cursus, gestion des apprenants, de leur progression, de leurs évaluations...) ; en sus, quelques infos utiles au pilotage (ex. nombres d'apprenants par typologie de contenu, par niveau d'avancement, par cursus... Mais aussi, des "données économiques" : chiffre d'affaire global, par cursus...)  

### 3.2. Base de données
_"Décris ici comment tu vois la base de données de l'application ?"_
Bien pensée, bien remplie, évidemment : pourquoi cette question :smile: ?

Plus sérieusement, le modèle central n'est pas trop compliqué et devrait vous rappeler quelque chose :
- Des "users" :
  - certains seront spécialisés en "apprenants" (_i.e._ users inscrits), 
  - d'autres seront juste des "prospects" (_i.e._ infos récupérées via la landing page et que nous ne manquerons pas de spammer avec des offres commerciales bienveillantes :japanese_ogre:)
  - d'autres encore auront un rôle de "référent / enseignant" (à voir comment on l'utilisera par la suite...)
  - enfin, un petit nombre d'élu(e)s bénéficieraient de l'enviable statut d'administrateur(trice) : le "God Mode" de la plateforme, en quelques sortes :sunglasses:.
- Des contenus pédagogiques structurés en cours / modules / cursus ou quelque chose d'approchant
- Des inscriptions qui feront le lien :link: entre certains des utilisateurs évoqués et leurs apprentissages
- Des évaluations, une pour chaque 'user' sur chaque 'cours' de chaque 'module' de chaque 'curriculum' (structure non-contractuelle :wink:)
- A cela pourrait sûrement s'ajouter quelques "vérues", du genre _like_ et commentaires à propos des cours

### 3.3. Front
Déjà détaillé plus haut, en 3.1 : du Bootstrap revampé, du javascript (vanilla), de belles images avec un camaïeu top hype, une navigation intuitive et le tour est joué !

### 3.4. Backend
Hormis Rails et les quelques gems Ruby / RoR déjà étudiées ("devise" pour le sessionning, "dotenv-rails" pour gérer d'éventuelles infos sensibles à stocker, "stripe" pour... permettre les paiements via Stripe, quelque chose pour un éventuel _chat_ entre élèves, etc.) on a pas encore achevé de réfléchir jusqu'à quel point on pourrait / voudrait / saurait / aura le temps de _pimper_ notre PLP... Pardon, _Peer Learning Platform_.

### 3.5. Nos besoins techniques
En gros, on a déjà un noyau d'équipe (un "seed" :wink:) constitué de :
  - **Wilfried PAILLOT**, _The Code Gardener_. Il cultive le code comme on chérit un bonzaï :deciduous_tree: ou on bouture des orchidées rares :hibiscus:, le fait grandir :seedling: et sait tout faire pousser :cherry_blossom: :ear_of_rice: :blossom: :palm_tree:  :corn: :mushroom:, en particulier du PHP, du Ruby et du Bootstrap. La légende dit qu'il peut coder des algos hyper stylés sur des arbres N-aires rien qu'en en effleurant les :fallen_leaf:.
  - **Yassine ROCHD**, _The Cypher_. Notre "homme du chiffre", expert en _Private Equity_ :money_with_wings: :rocket: , en _Real Estate_ :house: et, à ses heures perdues, body builder émérite autant que _daily coder_ pour le front desk des Rotschild, JP Morgan & Co. Quand il n'est pas dans les travaux de l'une de ses nombreuses résidences secondaires :house_with_garden:, il se balade dans les couloirs du Corail :train: Paris - Toulouse dont il affectionne la voiture bar(-chart) :bar_chart:.
  - **David NGUYEN**, _The Librarian_. Une véritable encyclopédie vivante du code :closed_book: :green_book: :blue_book: :orange_book: :notebook: :ledger: :notebook_with_decorative_cover: :books:, le [Leo Getz](https://getyarn.io/yarn-clip/5b79e150-5544-465e-b6cc-29b6012f8a43) de la syntaxe ; la seule documentation qui parle et, en même temps, a assez de détente pour te mettre une trempe au volley :soccer: (OK... c'est un ballon de foot mais y'a pas d'emoji "Volley" dans la bibliothèque Markdown :cry:)
  - **Jean-Baptiste VIDAL**, _The Amstrad Mastermind_. Il est tombé dans le code quand il était tout petit (:heart:[CPC 6128](https://fr.wikipedia.org/wiki/Amstrad_CPC_6128):heart:). Depuis, il n'a pas beaucoup grandi et a dû faire une désyntox' :syringe: de 15 ans "no code" :broken_heart:. Depuis quelques semaines, THPix, le druide du _peer-learning_ lui a permis de reprendre quelques lampées de prog', _The Librarian_ lui a trouvé 1 ou 2 sites de docs sympas sur [Ruby Guides](https://www.rubyguides.com/2020/03/rails-scaffolding/) et, jusqu'ici, hormis quelques _scaffoldings_ un peu trop sauvages, tout va bien...

:warning: Une fois ça dit, il faudra voir le "qui fait quoi" dans l'équipe plus précisément mais :
- On attend de confirmer si David participerait au projet ou pas, sachant qu'il a fait partie de l'aventure THP dès le début
- Le but est que tout le monde mette bien la main à la patte, sans trop rester sur une spécialité ou un domaine déjà (trop) maîtrisé.
Du coup, nous envisageons renforcer l'équipe d':one: ou :two: bonnes âmes qui pourraient complémenter notre :sparkles: Dream Team :sparkles:, tout simplement :relaxed:.

## 4. La version minimaliste mais fonctionnelle qu'il faudra avoir livré la première semaine
Tout ça reste à préciser mais on peut imaginer, au bout de ces quelques jours, d'avoir, en plus d'une "landing page", les pages et fonctionnalités de base de consultation, modification (selon le type de profil), création (idem) et suppression (idem²) des principaux "objets" du modèles : 
- quelques pages d'info et d'accroche, lorsqu'on est pas connecté ; par exemple : cursus & tarifs, contact, équipe...
- les "users" des différents types (apprenants, admins)
- les cours assemblés de façon arborescente, en modules et/ou cursus
- les sessions / promotions qui regroupent des modules / cours sur une période donnée et rassemblent des users inscrits
- le système de mails d'information / confirmation qui va avec tout ça
- un tableau de bord pour :
  - l'apprenant qui résume les modules suivis, les cours réussis, l'accès au catalogue de formation... 
  - l'administateur qui centralise des informations et chiffres en lien avec les apprenants, les chiffres de participation par cours/modules, 

Le tout avec un look acceptable... Alors, ça vous parle ? Partant(e)s ?

## 5. La version que l'on présenterait aux jury
En plus de finaliser les fonctionnalités et le look du MVP de la semaine 1, on pourrait discuter d'ajouts comme : 
- une messagerie interne (instantanée type _chat_ ou asynchrone type forum) ; éventuellement aves une logique de messages privés vs. publics
- des commentaires et/ou likes sur les éléments de cours (avec une possibilité de revue par les administrateurs ?), 
- des évaluations (individuelles, via des quizz) ; le tout obligeant possiblement à / offrant de repasser le test quelques heures après un raté (ex. <80% de bonnes réponses individuelles)
- de l'authoring / CMS simple pour saisir le contenu des cours (au format MD, par exemple),

- des indicateurs de pilotage et/ou [KPIs](https://fr.wikipedia.org/wiki/Indicateur_cl%C3%A9_de_performance), à destinations des apprenants (ex. temps moyen constaté pour achever un module) et/ou des administrateurs (ex. nombre d'inscrits, etc.).

## 6. Fonctionnalités "bonus" (en suspens)
- Rendre les évaluations plus uniquement individuelles mais "par les pairs" avec des "barrières" adaptées (ex. 80% d'appréciations positives par le ou les correcteurs)
- Logique de "sessions / promotions" plutôt que d'inscription à la volée et individuelle
- Ajouts d'autres types d'utilisateurs (_e.g._ mentors) avec des fonctionnalités particulières.

## 7. Notre mentor
_"Qui est ton mentor ?"_  
Alors là... Vu le sujet, on pensait humblement s'appuyer sur Félix et/ou Guillaume, voire les deux. Puis on s'est dit qu'ils étaient peut-être un tantinet occupé par autre chose. Nous sommes donc en recherche active :eyes: :telescope: :mag: d'un(e) mentor qui serait, comme nous, intéressé(e) par cette thématique "Learning" !

## 99. Le mot de la fin
Que tu sois moussaillon(ne) - candidat(e) ou pas à nous rejoindre -, pirate, corsaire ou membre du staff, nous sommes preneurs de ton avis, tes suggestions, etc. N'hésite donc pas à nous aborder (et pas saborder, hein...) sur Discord pour nous donner ton avis, ta vision, des idées, etc !