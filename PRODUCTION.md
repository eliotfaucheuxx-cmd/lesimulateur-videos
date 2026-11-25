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
Voix off : fr-BE-GerardNeural, débit +15 %, hauteur normale — choix de l'utilisateur (24/11) pour TOUTE la suite du projet.
Ne pas en changer sans sa demande.

## Étapes
1. Installation selon le RUNBOOK (si pas déjà fait dans l'espace de travail). Voix edge-tts à travers le proxy :
   dans tts.py, avant d'importer edge_tts : `import certifi; certifi.where=lambda: '/root/.ccr/ca-bundle.crt'`,
   puis `import ssl, edge_tts.communicate as ec; ec.ssl_ctx = ssl.create_default_context(cafile='/root/.ccr/ca-bundle.crt')`,
   et `proxy=os.environ.get('HTTPS_PROXY')` dans edge_tts.Communicate. Ne jamais désactiver la vérification TLS.
2. Ménage : posts Buffer de « My organization » (id 6b05639be08716fac2351d25). Pour chaque vidéo du dépôt dont TOUS les posts
   (TikTok et YouTube) sont « sent », supprimer le .mp4 (git rm, commit, push) en gardant sources.md.
3. Sujet : NN = plus grand pNN du dépôt ou du kit + 1. Premier sujet du tableau du doc sans dossier, dont le décor existe
   (Paris : Trocadéro, tour Eiffel, Champ-de-Mars, Seine, ville haussmannienne) et qui respecte la règle CONCEPTS.
   Décor neuf requis (Mont-Saint-Michel, Marseille, pont de Normandie) → sujet sauté. Sinon inventer un « Et si… ? » à Paris.
4. Recherche + script : 180–230 mots, structure en 5 temps du doc, durée finale 61–66 s (plus d'une minute : condition du programme de rémunération TikTok), chiffres vérifiés → pNN/sources.md.
5. Production selon le RUNBOOK : voix, episode.js (modèle p02), planche 40 images (2 tours de correction max), rendu complet,
   son (−14 LUFS), sous-titres, encodage, contrôle final (scintillement, raccord de boucle, chiffres écran = voix = sources).
6. Échec d'un contrôle après 2 tours → rien n'est déposé ; une phrase à l'utilisateur dans la conversation, puis stop.
7. Dépôt : pNN/pNN_<sujet-court>.mp4 (< 95 Mo) + pNN/sources.md ; ajouter la ligne du concept dans concepts.md ;
   commit (lignes d'attribution de la session), push sur main.
   URL : https://raw.githubusercontent.com/eliotfaucheuxx-cmd/lesimulateur-videos/main/pNN/<fichier>.mp4
8. Deux BROUILLONS Buffer (create_post, saveToDraft: true, schedulingType: automatic) :
   - TikTok 6b0563f78541f09ecb879c61 : text = titre + 4–5 hashtags ; metadata.tiktok = {title, isAiGenerated: false}.
   - YouTube 6b05642b8541f09ecb879e92 : text = 1–2 phrases citant les sources + hashtags dont #shorts ;
     metadata.youtube = {type: "short", title, categoryId: "28", isAiGenerated: false, madeForKids: false, privacy: "public"}.
   Titre « Question courte ? » + 1–2 émojis. Vérifier que Buffer a lu la vidéo (durationMs présent).
9. Kit : republier l'artefact (publish_files, même slug, base_version lue) avec pNN/ (episode.js, script.txt, subs_cfg.json,
   sources.md, words.json) et les améliorations du moteur ; au plus une leçon dans RUNBOOK.md.
10. Livraison DANS LA CONVERSATION : SendUserFile (la vidéo) + message court : titre, durée, légende TikTok, description
    YouTube, chiffres et sources, et « Réponds « go » pour la publier. »
    Puis PushNotification (message court, ex. « Vidéo pNN prête : <titre> — réponds go pour la publier »),
    pour que l'utilisateur soit prévenu sur son téléphone. Même chose en cas d'échec d'un contrôle.
11. Sur « go » : edit_post des deux brouillons (mode: addToQueue, saveToDraft: false), puis donner les horaires prévus.
    Corrections demandées → corriger, redéposer, mettre à jour les brouillons, redemander un « go ».

Budget ou temps insuffisant → livrer ce qui est prêt, sans brouillon pour une vidéo incomplète, et dire ce qui manque.
