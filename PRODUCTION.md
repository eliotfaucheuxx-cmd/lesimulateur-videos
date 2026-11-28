# Le Simulateur — consigne de production quotidienne

Tout se passe dans UNE seule conversation Claude (celle où l'utilisateur a mis en place la chaîne).
Chaque matin, un rappel programmé arrive dans cette conversation : Claude fabrique UNE vidéo,
la poste dans la conversation et attend le « go » de l'utilisateur, ici même.

## Règles absolues (priment sur tout)
- Jamais de publication publique sans un « go » explicite de l'utilisateur pour CETTE vidéo.
  Avant le « go » : uniquement des BROUILLONS Buffer (saveToDraft: true). Une vidéo ignorée n'est jamais publiée d'office.
  Si plusieurs vidéos attendent, un « go » sans précision vaut pour la plus récente ; en cas de doute, demander laquelle.
- Chaque chiffre dit ou affiché est vérifié sur le web (WebSearch + WebFetch, 2 sources si possible), noté avec son lien
  dans pNN/sources.md. Un calcul simulé est présenté comme une simulation.
- Pas de violence graphique : destruction d'objets, de bâtiments, de paysages ; des gens qui se protègent, tombent,
  se relèvent ; jamais de sang, de blessure ni de victime.
- Charte texte v2 (Anton + Montserrat Black ; zones A y190–290 / B y380–820 / sous-titres karaoké majuscules en bas ;
  rien à droite de x 900 ni sous y 1450 ; blanc, jaune #FFD60A, rouge #FF3B30, vert #30D158).
- Pas de personnage ni de marque protégés.
- Étiquette IA (décision de l'utilisateur, 24/11 — remplace la règle « contenu IA coché » du doc) : NE PAS cocher la case
  « contenu IA » (isAiGenerated: false sur TikTok et YouTube). Les règles des plateformes ne l'exigent que pour un contenu
  réaliste qu'on pourrait prendre pour de vraies images ; notre 3D stylisée et une voix de synthèse générique n'en sont pas.
  EXCEPTION : si une vidéo devient assez réaliste pour être prise pour de vraies images (ou imite une vraie personne),
  cocher la case et le signaler à l'utilisateur dans la livraison.
- Une vidéo avec un défaut connu (sol qui tremble, image noire, trou, texte hors zone, chiffre sans source) n'est PAS déposée.
- CONCEPTS : jamais deux fois le même concept (même phénomène + même question). Une parenté est permise
  (ex. deux vidéos sur l'espace), une copie avec juste un autre lieu ne l'est pas. Liste dans concepts.md, à lire avant
  de choisir et à compléter après chaque vidéo. Refaire un concept = seulement avec l'accord de l'utilisateur.

## Sources de vérité
1. Artefact « Kit Le Simulateur », slug 68626a03-5140-4b21-b2ff-e1207f43f01e : moteur, RUNBOOK.md (à suivre à la lettre),
   épisodes modèles (p02 = référence validée). Copie de travail installée dans /home/claude/kit (moteur « rendu v2 » :
   nuages, dalles, pelouse, façades variées, lumière chaude — garder ces réglages par défaut). Si elle manque, récupérer
   tous les fichiers avec list_files + read_file(paths=[…]).
2. Doc « Le Simulateur — plan de production des vidéos » https://claude.ai/artifact/TzguHDrj5Atto8nFPSH6ZY (outils Claude Docs) :
   concept, structure en 5 temps, charte, tableau « Prochains épisodes proposés ». Publication = Buffer + ce dépôt (pas Metricool).
3. Ce dépôt (eliotfaucheuxx-cmd/lesimulateur-videos, main), cloné dans /home/claude/lesimulateur-videos.
   S'il manque : add_repo (push), clone --depth 1 avec un long délai, register_repo_root.

## Voix
Voix off : fr-BE-GerardNeural, hauteur normale — choix de l'utilisateur (24/11) pour TOUTE la suite du projet.
Débit +25 % depuis le 27/11 (« plus rapide le ton ») : `python3 tts.py pNN/script.txt pNN fr-BE-GerardNeural +25%`.

## TON v4 (demande de l'utilisateur, 27/11) — prime sur tout le reste du style
« Un peu moins scientifique, plus rythmé, plus de plans et d'animations, moins de texte hyper technique,
plus rapide le ton et les scènes, plus de trucs un peu WTF dans la réflexion. »
- Ton : copain qui raconte un truc dingue, pas prof. Phrases de 4 à 12 mots. Zéro jargon (pas de « atmosphère standard »,
  « limite de Roche », « hPa », « orthodromique »…) : on dit l'effet, pas le nom du phénomène.
- Chiffres : toujours vérifiés (sources.md complète comme avant), mais à l'écran et à la voix seulement 3 ou 4 chiffres
  forts, arrondis, traduits en comparaisons du quotidien (« 27 tours Eiffel », « plus froid qu'un congélateur »,
  « ton souffle ne sert plus à rien »). Les précisions techniques restent dans sources.md et la description YouTube.
- WTF : au moins 3 conséquences absurdes mais vraies ou plausibles (pigeons, métro, baguette, chats, touristes, voisins,
  Wi-Fi…), une par palier, et un retournement final qu'on n'attend pas. Chercher l'angle « attends… quoi ? ».
- Rythme : un plan toutes les 1,5–2,5 s (≈ 30 plans par vidéo), jamais 4 s sur le même cadrage ; mouvements de caméra
  francs (travellings, zooms, plans subjectifs, réactions de la foule) ; une animation qui bouge à chaque plan.
- Texte à l'écran : 1 à 3 mots en gros (le chiffre ou le mot choc), pas de phrases ; plus de panneaux explicatifs ou de
  schémas chargés ; un mini-schéma seulement s'il se comprend en 1 seconde.
- LISIBILITÉ (retour de l'utilisateur après p06, 28/11 : « le rythme est mieux, mais on comprend pas trop le sens ;
  plus simple à suivre, qui évolue, avec le même système ; on voit et explique le concept de fin au premier plan ») :
  · PREMIER PLAN = LA FIN : on montre l'image finale ET la voix dit clairement la conclusion en une phrase
    (ex. « Ça, c'est Paris sous 30 mètres d'eau. Voilà comment on en arrive là. »). Le spectateur sait où on va.
  · UN SEUL FIL qui évolue : une seule chose qui grandit (une seule mesure, un seul objet, un seul lieu repère).
    Pas de changement de sujet en cours de route (p06 mélangeait hauteur, poids et longueur : à éviter).
  · Un plan REPÈRE qui revient à chaque palier (même cadrage, ex. le Trocadéro face à la tour) pour voir l'évolution.
  · Un COMPTEUR unique toujours visible (petit, en haut) qui monte de palier en palier.
  · Chaque palier = une phrase simple : ce qu'on voit + le chiffre + la conséquence WTF. 4 à 5 paliers maximum.
  · Le rythme reste rapide (≈ 30 plans), mais les plans d'un palier montrent tous la même chose sous plusieurs angles.
- Sujets : préférer les idées absurdes et concrètes (« Et si tous les Parisiens sautaient en même temps ? »,
  « Et si la Seine se vidait d'un coup ? », « Et si un pigeon faisait la taille de la tour Eiffel ? »,
  « Et si Paris tournait 10 fois plus vite ? », « Combien de baguettes pour remplir la tour Eiffel ? »).
Ne pas en changer sans sa demande.

## Étapes
1. Installation selon le RUNBOOK (si pas déjà fait dans l'espace de travail). Voix edge-tts à travers le proxy :
   dans tts.py, avant d'importer edge_tts : `import certifi; certifi.where=lambda: '/root/.ccr/ca-bundle.crt'`,
   puis `import ssl, edge_tts.communicate as ec; ec.ssl_ctx = ssl.create_default_context(cafile='/root/.ccr/ca-bundle.crt')`,
   et `proxy=os.environ.get('HTTPS_PROXY')` dans edge_tts.Communicate. Ne jamais désactiver la vérification TLS.
2. Ménage : posts Buffer de « My organization » (id 6b05639be08716fac2351d25). Pour chaque vidéo du dépôt dont le post YouTube
   est « sent » (TikTok ne passe plus par Buffer), supprimer le .mp4 (git rm, commit, push) en gardant sources.md.
3. Sujet : NN = plus grand pNN du dépôt ou du kit + 1. Premier sujet du tableau du doc sans dossier, dont le décor existe
   (Paris : Trocadéro, tour Eiffel, Champ-de-Mars, Seine, ville haussmannienne) et qui respecte la règle CONCEPTS.
   Décor neuf requis (Mont-Saint-Michel, Marseille, pont de Normandie) → sujet sauté. Sinon inventer un « Et si… ? » à Paris.
   FORMATS EN ROTATION (RUNBOOK §0, v3) : A « Quelle taille / combien… ? » · B « Et si [phénomène] à Paris ? » ·
   C « À l'échelle » (objet géant ou minuscule comparé à Paris). Jamais deux fois de suite le même format :
   lire la lettre de la dernière ligne de concepts.md et choisir un sujet d'un autre format.
4. Recherche + script (TON v4) : 210–240 mots à +25 %, structure en 5 temps du doc ; 1re phrase = la question avec le LIEU et un CHIFFRE ou
   un enjeu concret, dite avant 0,5 s ; annoncer tôt le nombre de paliers (promesse ouverte) ; dernière phrase = question
   binaire qui renvoie au début (boucle) ; durée finale 61–66 s (plus d'une minute : condition du programme de rémunération TikTok), chiffres vérifiés → pNN/sources.md.
5. Production selon le RUNBOOK : voix, episode.js (modèle p04 : caméra via engine/shots.js, zoom d'ouverture),  planche 40 images (2 tours de correction max), rendu complet,
   son (−14 LUFS), sous-titres, encodage, contrôle final (scintillement, raccord de boucle, chiffres écran = voix = sources)
   + `python3 dbg/hook.py pNN` : tout doit être OK (sinon c'est un défaut connu → étape 6).
6. Échec d'un contrôle après 2 tours → rien n'est déposé ; une phrase à l'utilisateur dans la conversation, puis stop.
7. Dépôt : pNN/pNN_<sujet-court>.mp4 (< 95 Mo) + pNN/sources.md ; ajouter la ligne du concept dans concepts.md
   (avec sa lettre de format [A]/[B]/[C]) ;
   commit (lignes d'attribution de la session), push sur main.
   URL : https://raw.githubusercontent.com/eliotfaucheuxx-cmd/lesimulateur-videos/main/pNN/<fichier>.mp4
8. TikTok = PUBLICATION MANUELLE PAR L'UTILISATEUR (décision du 25/11 : le compte neuf n'a eu aucune vue via Buffer, et 0 souci
   en publiant à la main). Ne JAMAIS créer de post TikTok dans Buffer. Préparer seulement la légende TikTok : la question
   telle qu'on la taperait dans la recherche TikTok (mots du titre ET de la 1re phrase dite), une phrase d'accroche avec le
   chiffre le plus fort, puis 4–5 hashtags (#paris #science #etsi + 1–2 du sujet). TikTok indexe voix, sous-titres et légende.
   UN BROUILLON Buffer YouTube (create_post, saveToDraft: true, schedulingType: automatic) :
   - YouTube 6b05642b8541f09ecb879e92 : text = 1–2 phrases citant les sources + hashtags dont #shorts ;
     metadata.youtube = {type: "short", title, categoryId: "28", isAiGenerated: false, madeForKids: false, privacy: "public"}.
   Titre « Question courte ? » (≤ 60 caractères, mots-clés au début) + 1 émoji à la fin. Vérifier que Buffer a lu la vidéo (durationMs présent).
9. Kit : republier l'artefact (publish_files, même slug, base_version lue) avec pNN/ (episode.js, script.txt, subs_cfg.json,
   sources.md, words.json) et les améliorations du moteur ; au plus une leçon dans RUNBOOK.md.
10. Livraison DANS LA CONVERSATION : SendUserFile (la vidéo, display attach, pour qu'il puisse la télécharger et la poster sur
    TikTok) + message court, qui commence par une ligne de suivi des vidéos
    déjà publiées (vues YouTube via list_posts includeMetrics ; les vidéos TikTok postées à la main ne sont pas visibles depuis Buffer) ; ensuite : titre, durée, légende TikTok, description
    YouTube, chiffres et sources ; la légende TikTok dans un bloc de code (facile à copier) avec le rappel « publie-la toi-même sur
    TikTok, idéalement entre 18 h et 21 h, case « contenu IA » décochée, couverture = la 1re image (la question) » ; et « Réponds « go » pour la mettre en file sur YouTube. »
    Puis PushNotification (message court, ex. « Vidéo pNN prête : <titre> — réponds go pour la publier »),
    pour que l'utilisateur soit prévenu sur son téléphone. Même chose en cas d'échec d'un contrôle.
11. Sur « go » : edit_post du brouillon YouTube (mode: addToQueue, saveToDraft: false), puis donner l'horaire prévu.
    Corrections demandées → corriger, redéposer, mettre à jour les brouillons, redemander un « go ».

Budget ou temps insuffisant → livrer ce qui est prêt, sans brouillon pour une vidéo incomplète, et dire ce qui manque.
