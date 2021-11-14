---
title: Stockage côté client
slug: Learn/JavaScript/Client-side_web_APIs/Client-side_storage
tags:
  - API
  - Apprendre
  - Codage
  - Débutant
  - Guide
  - IndexedDB
  - JavaScript
  - Storage
translation_of: Learn/JavaScript/Client-side_web_APIs/Client-side_storage
original_slug: Apprendre/JavaScript/Client-side_web_APIs/Client-side_storage
---
<p>{{LearnSidebar}}</p>

<div>{{PreviousMenu("Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}</div>

<div></div>

<p>Les navigateurs web modernes permettent aux sites web de stocker des données sur l'ordinateur de l'utilisateur — avec sa permission — puis de les récupérer au besoin. Cela permet d'enregistrer des données pour du stockage à long terme, de sauvegarder des documents ou des sites hors-ligne, de conserver des préférences spécifiques à l'utilisateur et plus encore. Cet article explique les fondamentaux pour y parvenir.</p>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="row">Prérequis:</th>
   <td>Notions de bases de JavaScript (voir <a href="/fr/docs/Learn/JavaScript/First_steps">premiers pas</a>, <a href="/fr/Apprendre/JavaScript/Building_blocks">les briques JavaScript</a>, <a href="/fr/docs/Learn/JavaScript/Objects">les objets JavaScript</a>), les <a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Introduction">notions de base des APIs côté client</a></td>
  </tr>
  <tr>
   <th scope="row">Objectif:</th>
   <td>Apprendre à utiliser les APIs de stockage côté client pour stocker des données de l'application.</td>
  </tr>
 </tbody>
</table>

<h2 id="Stockage_côté_client">Stockage côté client ?</h2>

<p>Ailleurs dans la zone d'apprentissage de MDN, nous avons parlé de la différence entre les <a href="/fr/docs/Learn/Server-side/First_steps/Client-Server_overview#Static_sites">sites statiques</a> et les <a href="/fr/docs/Learn/Server-side/First_steps/Client-Server_overview#Dynamic_sites">sites dynamiques</a> — ces derniers stockent des données <a href="/fr/docs/Learn/Server-side">côté serveur</a> en utilisant une base de données. Ensuite, ils exécutent du code pour récupérer les données et les insérer dans des templates de page statique. Finalement, le HTML résultant est envoyé au client, qui est alors affiché par le navigateur de l'utilisateur.</p>

<p>Le stockage côté client fonctionne sur des principes similaires, mais pour une utilisation différente. Le stockage côté client repose sur des APIs JavaScript qui permettent de stocker des données sur la machine de l'utilisateur et de les récupérer au besoin. Cela peut se révéler utile dans différents cas comme :</p>

<ul>
 <li>Personnaliser les préférences du site (par exemple, afficher des widgets personnalisés selon le choix de l'utilisateur, changer le thème du site ou la taille de la police).</li>
 <li>Enregistrer les activités sur le site (comme le contenu d'un panier d'achat d'une session précédente, ou encore se souvenir si l'utilisateur s'est déjà connecté).</li>
 <li>Sauvegarder des données et ressources localement pour pouvoir accéder au site plus rapidement ou même sans connexion réseau.</li>
 <li>Sauvegarder des documents générés par l'application pour une utilisation hors ligne.</li>
</ul>

<p>Souvent, le stockage côté client et côté serveur sont utilisés ensemble. Par exemple, vous pouvez télécharger à partir d'une base de données côté serveur une série de fichiers mp3 utilisés par un site web (comme un jeu ou une application de musique) vers une base de données côté client et ainsi pouvoir les lire quand vous le voulez. Avec cette stratégie, l'utilisateur n'a à télécharger le fichier qu'une seule fois — les visites suivantes, ils sont récupérés à partir de la base de données locale.</p>

<div class="note">
<p><strong>Note :</strong> La quantité de données que l'on peut stocker à l'aide des APIs de stockage côté client est limitée (limite par API et limite globale), la limite exacte dépend du navigateur et des configurations. Voir <a href="/fr/docs/Web/API/API_IndexedDB/Browser_storage_limits_and_eviction_criteria">Limites de stockage du navigateur et critères d'éviction</a> pour plus d'informations.</p>
</div>

<h3 id="À_lancienne_les_cookies">À l'ancienne : les cookies</h3>

<p>Le concept de stockage côté client existe depuis longtemps. Au début du web, les sites utilisaient des <a href="/fr/docs/Web/HTTP/Cookies">cookies</a> pour stocker des informations et personnaliser l'expérience utilisateur. C'est la méthode de stockage côté client la plus couramment utilisée et la plus ancienne.</p>

<p>De par leur histoire, les cookies souffrent d'un certain nombre de problèmes — tant techniques qu'au niveau de l'expérience utilisateur. Ces problèmes sont suffisamment importants pour imposer un message d'information aux utilisateurs habitant en Europe lors de leur première visite si le site utilise des cookies pour stocker des informations sur eux. Cela est dû à une loi de l'Union Européenne connue sous le nom de <a href="/fr/docs/Web/HTTP/Cookies#EU_cookie_directive">directive Cookie</a>.</p>

<p><img alt="" src="cookies-notice.png"></p>

<p>Pour ces raisons, nous ne verrons pas dans cet article comment utiliser les cookies. Entre le fait qu'ils sont dépassés, les <a href="/fr/docs/Web/HTTP/Cookies#Security">problèmes de sécurité</a> qu'ils présentent et l'incapacité de stocker des données complexes, les cookies ne sont pas la meilleure manière pour stocker des données. Il y a de meilleures alternatives, modernes, permettant de stocker des données variées sur l'ordinateur de l'utilisateur.</p>

<p>Le seul avantage des cookies est qu'ils sont supportés par des navigateurs anciens : si votre projet requiert le support de navigateurs obsolètes (comme Internet Explorer 8 et inférieur), les cookies peuvent se révéler utiles. Pour la plupart des projets, vous ne devriez pas avoir besoin d'y recourir.</p>

<div class="note">
<p><strong>Note :</strong> Pourquoi existe-t-il encore de nouveaux sites crées à l'aide de cookies? Principalement de par les habitudes des développeurs, l'utilisation de bibliothèques anciennes qui utilisent encore des cookies et l'existence de nombreux sites web fournissant des formations et références dépassées pour apprendre à stocker des données.</p>
</div>

<h3 id="La_nouvelle_école_Web_Storage_et_IndexedDB">La nouvelle école : Web Storage et IndexedDB</h3>

<p>Les navigateurs modernes ont des APIs beaucoup plus efficaces et faciles d'utilisation pour stocker des données côté client.</p>

<ul>
 <li>L'<a href="/fr/docs/Web/API/Web_Storage_API">API Web Storage</a> fournit une syntaxe très simple pour stocker et récupérer des données de petite taille, basé sur un système de clé/valeur. C'est utile lorsque vous avez besoin de stocker des données simples, comme le nom de l'utilisateur, le fait qu'il soit connecté ou non, la couleur à utiliser pour l'arrière-plan de l'écran, etc.</li>
 <li>L'<a href="/fr/docs/Web/API/API_IndexedDB">API IndexedDB</a> fournit au navigateur un système de base de données complet pour stocker des données complexes. C'est utile pour des choses allant de simples sauvegardes côté client (texte) au stockage de données complexes tels que des fichiers audio ou vidéo.</li>
</ul>

<p>Vous en apprendrez plus sur ces APIs ci-dessous.</p>

<h3 id="Le_futur_lAPI_Cache">Le futur : l'API Cache</h3>

<p>Certains navigateurs modernes prennent en charge la nouvelle API {{domxref("Cache")}}. Cette API a été conçue pour stocker les réponses HTTP de requêtes données et est très utile pour stocker des ressources du site afin qu'il soit accessible sans connexion réseau par exemple. Le cache est généralement utilisé avec l'<a href="/fr/docs/Web/API/Service_Worker_API">API Service Worker</a>, mais ce n'est pas obligatoire.</p>

<p>L'utilisation du Cache et des Service Workers est un sujet avancé, nous ne le traiterons pas en détail dans cet article, nous ne montrerons qu'un simple exemple dans la section {{anch("Stockage hors-ligne de ressources")}} plus bas.</p>

<h2 id="Stocker_des_données_simples_—_web_storage">Stocker des données simples — web storage</h2>

<p>L'<a href="/fr/docs/Web/API/Web_Storage_API">API Web Storage</a> est très facile à utiliser — on stocke une simple paire clé/valeur de données (limité aux données scalaires) et on les récupére au besoin.</p>

<h3 id="Syntaxe_basique">Syntaxe basique</h3>

<p>Nous allons vous guider pas à pas :</p>

<ol>
 <li>
  <p>Tout d'abord, ouvez notre template vide de <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/web-storage/index.html">web storage sur GitHub</a> dans un nouvel onglet.</p>
 </li>
 <li>
  <p>Ouvrez la console JavaScript de votre navigateur.</p>
 </li>
 <li>
  <p>Toutes les données du web storage sont contenues dans deux structures de type objet : {{domxref("Window.sessionStorage", "sessionStorage")}} et {{domxref("Window.localStorage", "localStorage")}}. Le premier conserve les données aussi longtemps que le navigateur est ouvert (elles sont perdues lorsque le navigateur est fermé) et le second conserve les données même après que le navigateur ait été fermé puis ré-ouvert. Nous allons utiliser le second dans cet article car il est généralement plus utile.</p>

  <p>La méthode {{domxref("Storage.setItem()")}} permet de sauvegarder des données dans le storage — elle prend deux paramètres : le nom de l'entrée à enregistrer et sa valeur. Essayez de taper ce qui suit dans votre console JavaScript (changez le nom et la valeur si vous le voulez !) :</p>

  <pre class="brush: js">localStorage.setItem('name','Chris');</pre>
 </li>
 <li>
  <p>La méthode {{domxref("Storage.getItem()")}} prend un paramètre — le nom de l'entrée que vous voulez récupérer — et retourne la valeur de l'entrée. Maintenant, tapez ces lignes dans votre console JavaScript :</p>

  <pre class="brush: js">var myName = localStorage.getItem('name');
myName</pre>

  <p>En tapant la deuxième ligne, vous devriez voir que la variable <code>myName</code> contient la valeur de l'entrée <code>name</code>.</p>
 </li>
 <li>
  <p>La méthode {{domxref("Storage.removeItem()")}} prend un paramètre — le nom de l'entrée de vous voulez supprimer — et supprime l'entrée du web storage. Tapez les lignes suivantes dans votre console JavaScript :</p>

  <pre class="brush: js">localStorage.removeItem('name');
var myName = localStorage.getItem('name');
myName</pre>

  <p>La troisième ligne devrait maintenant retourner <code>null</code> — l'entrée <code>name</code> n'existe plus dans le web storage.</p>
 </li>
</ol>

<h3 id="Les_données_persistent_!">Les données persistent !</h3>

<p>Une caractéristique clé du web storage est que les données persistent entre les différents chargements de page (et même lorsque le navigateur est arrêté dans le cas du <code>localStorage</code>). Regardons ça en action :</p>

<ol>
 <li>
  <p>Ouvrez notre template vide une fois de plus, mais cette fois dans un navigateur différent de celui dans lequel vous avez ouvert ce tutoriel. Cela rendra la suite plus facile.</p>
 </li>
 <li>
  <p>Tapez ces lignes dans la console JavaScript du navigateur que vous venez d'ouvrir :</p>

  <pre class="brush: js">localStorage.setItem('name','Chris');
var myName = localStorage.getItem('name');
myName</pre>

  <p>Vous devriez voir que l'entrée <code>name</code> est bien là.</p>
 </li>
 <li>
  <p>Maintenant, fermez le navigateur et ouvrez-le de nouveau.</p>
 </li>
 <li>
  <p>Entrez les lignes suivantes :</p>

  <pre class="brush: js">var myName = localStorage.getItem('name');
myName</pre>

  <p>Vous devriez voir que la valeur est toujours accessible, quand bien même le navigateur a été redémarré.</p>
 </li>
</ol>

<h3 id="Stockage_séparé_pour_chaque_domaine">Stockage séparé pour chaque domaine</h3>

<p>Il existe un système de stockage distinct pour chaque domaine (chaque adresse web chargée dans le navigateur a accès à son propre storage et pas aux autres). Vous verrez que si vous chargez deux sites web (disons google.com et amazon.com) et essayez de stocker un élément, il ne sera pas disponible sur l'autre site.</p>

<p>C'est plutôt logique — imaginez les problèmes de sécurité qui se poseraient si les sites web pouvaient voir les données d'un autre !</p>

<h3 id="Un_exemple_plus_impliqué">Un exemple plus impliqué</h3>

<p>Appliquons cette nouvelle connaissance pour écrire un exemple, cela vous donnera une idée de la façon dont le web storage peut être utilisé. Notre exemple permettra d'envoyer un nom, à la suite de quoi la page sera mise à jour pour donner un accueil personnalisé. Cet état persistera également après un rechargement de la page ou redémarrage du navigateur, puisqu'il sera stocké dans le web storage.</p>

<p>Le HTML de l'exemple est disponible à <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/web-storage/personal-greeting.html">personal-greeting.html</a> — il s'agit d'un site web très simple avec entête, contenu et pied de page, ainsi qu'un formulaire pour entrer votre nom.</p>

<p><img alt="" src="web-storage-demo.png"></p>

<p>Nous allons construire cet exemple pas à pas, cela vous permettra de comprendre comment ça marche.</p>

<ol>
 <li>
  <p>D'abord, copiez notre fichier <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/web-storage/personal-greeting.html">personal-greeting.html</a> dans un nouveau répertoire sur votre ordinateur.</p>
 </li>
 <li>
  <p>Ensuite, créez un fichier <code>index.js</code> dans le même répertoire que le fichier HTML — le fichier HTML inclut ce script (voir ligne 40).</p>
 </li>
 <li>
  <p>Nous allons commencer par récupérer les références de tous les éléments HTML qu'on manipulera dans cet exemple — nous les créons en tant que constantes car ces références n'ont pas besoin d'être modifiées au cours de l'exécution de l'application. Ajoutez les lignes suivantes à votre fichier JavaScript:</p>

  <pre class="brush: js">// créer les constantes nécessaires
const rememberDiv = document.querySelector('.remember');
const forgetDiv = document.querySelector('.forget');
const form = document.querySelector('form');
const nameInput = document.querySelector('#entername');
const submitBtn = document.querySelector('#submitname');
const forgetBtn = document.querySelector('#forgetname');

const h1 = document.querySelector('h1');
const personalGreeting = document.querySelector('.personal-greeting');</pre>
 </li>
 <li>
  <p>Ensuite, on doit ajouter un gestionnaire d'événement pour empêcher le formulaire d'être véritablement soumis lorsque le bouton de soumission est cliqué, puisque ce n'est pas le comportement que l'on veut. Ajoutez le bout de code suivant à la suite de du code précédent :</p>

  <pre class="brush: js">// Empêcher le form d'être soumis
form.addEventListener('submit', function(e) {
  e.preventDefault();
});</pre>
 </li>
 <li>
  <p>Maintenant, on doit ajouter un gestionnaire d'événement pour gérer le clic sur le bouton "Say hello" (dire bonjour). Les commentaires expliquent ce que chaque instruction fait, mais, en substance, on prend le nom que l'utilisateur a entré dans le champs texte et on l'enregistre dans le web storage avec <code>setItem()</code>. Ensuite, on exécute une fonction appelée <code>nameDisplayCheck()</code> qui se charge de mettre à jour le contenu du site web. Ajoutez ceci au bas de votre code :</p>

  <pre class="brush: js">// exécuter la fonction quand le bouton 'Say hello' est cliqué
submitBtn.addEventListener('click', function() {
  // stocker le nom entré dans le web storage
  localStorage.setItem('name', nameInput.value);
  // exécuter nameDisplayCheck() pour afficher la
  // page personnalisée et changer le formulaire
  nameDisplayCheck();
});</pre>
 </li>
 <li>
  <p>On doit maintenant gérer l'événement lorsque le bouton "Forget" (oublier) est cliqué — il est affiché une fois que le bouton "Say hello" a été cliqué (les deux boutons permettent de basculer d'un état à l'autre). Dans cette fonction, on supprime l'élément <code>name</code> du web storage en utilisant <code>removeItem()</code>, puis on exécute <code>nameDisplayCheck()</code> pour mettre à jour l'affichage. Ajoutez ceci au bas de votre code :</p>

  <pre class="brush: js">// exécuter la fonction quand le bouton 'Forget' est cliqué
forgetBtn.addEventListener('click', function() {
  // supprimer l'item name du web storage
  localStorage.removeItem('name');
 // exécuter nameDisplayCheck() pour afficher la
 // page personnalisée et changer le formulaire
  nameDisplayCheck();
});</pre>
 </li>
 <li>
  <p>Il est maintenant temps de définir la fonction <code>nameDisplayCheck()</code> elle-même. Ici, on vérifie si l'élément <code>name</code> est stocké dans le web storage en utilisant <code>localStorage.getItem('name')</code> comme condition. S'il existe, la valeur retournée sera évaluée à <code>true</code>; sinon, comme <code>false</code>. S'il existe, on affiche un message d'accueil personnalisé et le bouton "Forget" du formulaire, tout en masquant le bouton "Say hello" du formulaire. Sinon, on affiche un message d'accueil générique et le bouton "Say hello". Encore une fois, mettez les lignes suivantes au bas de votre code :</p>

  <pre class="brush: js">// définit la fonction nameDisplayCheck()
function nameDisplayCheck() {
  // vérifie si l'élément 'name' est stocké dans le web storage
  if(localStorage.getItem('name')) {
    // Si c'est le cas, affiche un accueil personnalisé
    let name = localStorage.getItem('name');
    h1.textContent = 'Welcome, ' + name;
    personalGreeting.textContent = 'Welcome to our website, ' + name + '! We hope you have fun while you are here.';
    // cache la partie 'remember' du formulaire et affiche la partie 'forget'
    forgetDiv.style.display = 'block';
    rememberDiv.style.display = 'none';
  } else {
    // Sinon, affiche un accueil générique
    h1.textContent = 'Welcome to our website ';
    personalGreeting.textContent = 'Welcome to our website. We hope you have fun while you are here.';
    // cache la partie 'forget' du formulaire et affiche la partie 'remember'
    forgetDiv.style.display = 'none';
    rememberDiv.style.display = 'block';
  }
}</pre>
 </li>
 <li>
  <p>Dernier point, mais non des moindres, on exécute la fonction <code>nameDisplayCheck()</code> à chaque fois que la page est chargée. Si on ne le faisait pas, l'accueil personnalisé ne serait pas affiché après qu'on ait rafraichit la page. Ajoutez ce qui suit au bas de votre code :</p>

  <pre class="brush: js">document.body.onload = nameDisplayCheck;</pre>
 </li>
</ol>

<p>Notre exemple est terminé — bien joué ! Il ne vous reste plus qu'à enregistrer votre code et tester votre page HTML dans un navigateur. Vous pouvez voir notre <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/web-storage/personal-greeting.html">version terminée en direct ici</a> (ou le <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/web-storage/index.js">code JavaScript terminé</a>).</p>

<div class="note">
<p><strong>Note :</strong> Vous pouvez trouver un exemple un peu plus complexe dans l'article <a href="/fr/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API">Utiliser l'API de stockage web</a>.</p>
</div>

<div class="note">
<p><strong>Note :</strong> Dans la ligne <code>&lt;script src="index.js" defer&gt;&lt;/script&gt;</code> de notre version finie, l'attribut <code>defer</code> spécifie que le contenu de l'élément {{htmlelement("script")}} ne doit pas s'exécuter avant que la page ait fini de charger.</p>
</div>

<h2 id="Stocker_des_données_complexes_—_IndexedDB">Stocker des données complexes — IndexedDB</h2>

<p>L'<a href="/fr/docs/Web/API/IndexedDB_API">API IndexedDB</a> (parfois abrégé IDB) est un système de base de données complet disponible dans le navigateur. Vous pouvez y stocker des données complexes, les types ne sont pas limités à des valeurs simples de type chaînes ou nombres. Vous pouvez stocker des vidéos, des images et à peu près tout ce que vous voulez, dans une instance IndexedDB.</p>

<p>Cependant, cela a un coût : IndexedDB est beaucoup plus complexe à utiliser que l'API Web Storage. Dans cette section, nous ne ferons qu'égratigner la surface de ce qu'IndexedDB peut faire, mais nous vous en donnerons assez pour débuter.</p>

<h3 id="Un_exemple_de_stockage_de_notes">Un exemple de stockage de notes</h3>

<p>Nous allons voir un exemple qui vous permettra de stocker des notes dans votre navigateur, les voir et les supprimer, quand vous le souhaitez. Vous apprendrez à le construire par vous-même au fur et à mesure des explications et cela vous permettra de comprendre les parties fondamentales d'IDB.</p>

<p>L'application ressemble à ceci :</p>

<p><img alt="" src="idb-demo.png"></p>

<p>Chaque note a un titre et une description, chacun éditables individuellement. Le code JavaScript que nous allons voir ci-dessous contient des commentaires détaillés pour vous aider à comprendre ce qu'il se passe.</p>

<h3 id="Pour_commencer">Pour commencer</h3>

<ol>
 <li>Tout d'abord, copiez les fichiers <code><a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/indexeddb/notes/index.html">index.html</a></code>, <code><a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/indexeddb/notes/style.css">style.css</a></code>, et <code><a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/indexeddb/notes/index-start.js">index-start.js</a></code> dans un nouveau répertoire sur votre ordinateur.</li>
 <li>Jetez un coup d'oeil aux fichiers.
  <ul>
   <li>Vous verrez que le HTML est assez simple : un site web avec une entête et un pied de page, ainsi qu'une zone de contenu principal contenant un emplacement pour afficher les notes et un formulaire pour en ajouter.</li>
   <li>Le CSS fournit un style simple pour rendre plus clair ce qu'il se passe.</li>
   <li>Le fichier JavaScript contient cinq constantes déclarées — des références à l'élément {{htmlelement("ul")}} dans lequel seront affichées les notes, les {{htmlelement("input")}} title et body, le {{htmlelement("form")}} lui-même, et un {{htmlelement("button")}}.</li>
  </ul>
 </li>
 <li>Renommez votre fichier JavaScript en <code>index.js</code>. Vous êtes maintenant prêt pour y ajouter du code.</li>
</ol>

<h3 id="Configuration_initiale_de_la_base_de_données">Configuration initiale de la base de données</h3>

<p>Voyons maintenant la première chose à faire, mettre en place la base de données.</p>

<ol>
 <li>
  <p>À la suite des déclarations de constantes, ajoutez les lignes suivantes :</p>

  <pre class="brush: js">// Objet db pour stocker la BDD ouverte
let db;</pre>

  <p>Ici, on déclare une variable appelée <code>db</code> — on l'utilisera plus tard pour stocker un objet permettant d'accéder à la base de données. On l'utilisera à plusieurs endroits, on l'a donc déclaré globablement ici pour faciliter les choses.</p>
 </li>
 <li>
  <p>Ensuite, ajoutez ce qui suit au bas de votre code :</p>

  <pre class="brush: js">window.onload = function() {

};</pre>

  <p>On écrira tout notre code dans le gestionnaire d'événement <code>window.onload</code>, appelé quand l'événement {{event("load")}} de la fenêtre est chargé, pour s'assurer qu'on n'essaiera pas d'utiliser IndexedDB avant que l'application ne soit complètement chargée (ça ne marcherait pas sinon).</p>
 </li>
 <li>
  <p>À l'intérieur de <code>window.onload</code>, ajoutez ce qui suit :</p>

  <pre class="brush: js">// Ouvrir la BDD; elle sera créée si elle n'existe pas déjà
// (voir onupgradeneeded)
let request = window.indexedDB.open('notes', 1);</pre>

  <p>Cette ligne crée une requête <code>request</code> pour ouvrir la version <code>1</code> de la base de données appelée <code>notes</code>. Si elle n'existe pas déjà, on devra la créer via un gestionnaire d'événement.</p>

  <p>Vous verrez très souvent ce format dans IndexedDB. Les opérations de base de données prennent du temps et on ne veut pas suspendre le navigateur le temps de récupérer le résultat, les opérations sur la base de données sont donc {{Glossary("asynchronous", "asynchrones")}} — ce qui signifie qu'au lieu d'arriver immédiatement, elles se produiront à un moment ultérieur et un événement sera déclenché lorsque cela arrivera.</p>

  <p>Pour gérer cela dans IndexedDB, on crée d'abord une requête (que vous pouvez appeler comme vous le voulez — on l'appelle <code>request</code> pour que ce soit plus explicite). On utilise ensuite des gestionnaire d'événement pour exécuter du code lorsque les requêtes sont terminées, échouent, etc, ce que l'on va voir ci-dessous.</p>

  <div class="note">
  <p><strong>Note :</strong> Le numéro de version est important. Si vous voulez mettre à jour votre base de données (par exemple, pour modifier la structure de la table), vous devez ré-exécuter votre code avec un numéro de version supérieur et spécifier le schéma de la base de données avec le gestionnaire d'événement <code>onupgradeneeded</code>. Nous ne verrons pas la mise à jour de base de données dans ce tutoriel.</p>
  </div>
 </li>
 <li>
  <p>Maintenant, ajoutez les gestionnaires d'événement suivants, juste en dessous des lignes précédentes — toujours à l'intérieur de <code>window.onload</code> :</p>

  <pre class="brush: js">// la base de données n'a pas pu être ouverte avec succès
request.onerror = function() {
  console.log('Database failed to open');
};

// la base de données a été ouverte avec succès
request.onsuccess = function() {
  console.log('Database opened successfully');

  // Stocke la base de données ouverte dans la variable db. On l'utilise par la suite
  db = request.result;

  // Exécute la fonction displayData() pour afficher les notes qui sont dans la BDD
  displayData();
};</pre>

  <p>Le gestionnaire d'événement {{domxref("IDBRequest.onerror", "request.onerror")}} s'exécutera si la requête échoue. Cela vous permet de gérer le problème si cela arrive. Dans notre exemple, on affiche simplement un message dans la console JavaScript.</p>

  <p>Le gestionnare d'événement {{domxref("IDBRequest.onsuccess", "request.onsuccess")}}, d'autre part, s'exécutera si la requête aboutit, que la base de données a été ouverte avec succès. Lorsque cela arrive, la propriété {{domxref("IDBRequest.result", "request.result")}} contient alors un objet représentant la base de données ouverte, qui nous permet de la manipuler. On stocke cette valeur dans la variable <code>db</code> qu'on a crée plus tôt pour pouvoir l'utiliser ensuite. On exécute également une fonction appelée <code>displayData()</code>, qu'on définira plus tard — elle affiche les données de la base de données dans le {{HTMLElement("ul")}}. On l'exécute dès à présent pour que les notes en base de données soient affichées dès que la page est chargée.</p>
 </li>
 <li>
  <p>Pour en finir avec cette section, on ajoute le gestionnaire d'événement qui est  probablement le plus important, {{domxref("IDBOpenDBRequest.onupgradeneeded", "request.onupdateneeded")}}. Il est exécuté si la base de données n'a pas déjà été créée ou si on veut ouvrir la base de données avec un numéro de version supérieur à celle qui existe (pour faire une mise à jour). Ajoutez le code suivant en dessous de votre gestionnaire précédent :</p>

  <pre class="brush: js">// Spécifie les tables de la BDD si ce n'est pas déjà pas fait
request.onupgradeneeded = function(e) {
  // Récupère une référence à la BDD ouverte
  let db = e.target.result;

  // Crée un objectStore pour stocker nos notes (une table)
  // Avec un champ qui s'auto-incrémente comme clé
  let objectStore = db.createObjectStore('notes', { keyPath: 'id', autoIncrement:true });

  // Définit les champs que l'objectStore contient
  objectStore.createIndex('title', 'title', { unique: false });
  objectStore.createIndex('body', 'body', { unique: false });

  console.log('Database setup complete');
};</pre>

  <p>C'est ici qu'on définit le schéma (la structure) de notre base de données; c'est à dire l'ensemble des champs (ou colonnes) qu'il contient.</p>

  <ol>
   <li>
    <p>On récupère une référence à la base de données existante depuis <code>e.target.result</code> (la propriété <code>result</code> de la cible de l'événement, c'est à dire l'objet <code>request</code>). C'est l'équivalent de la ligne <code>db = request.result;</code> du gestionnaire d'événement <code>onsuccess</code>, mais on doit le faire de cette manière ici puisque le gestionnaire d'événement <code>onupgradeneeded</code> est exécuté avant <code>onsuccess</code> — la valeur de <code>db</code> n'est pas encore disponible.</p>
   </li>
   <li>
    <p>Ensuite, on utilise {{domxref("IDBDatabase.createObjectStore()")}} pour créer un object store (un container pour une collection d'objets) à l'intérieur de notre base de données. C'est l'équivalent d'une table dans un système de base de données traditionnel. On lui a donné le nom <code>notes</code>, et un champs <code>id</code> avec <code>autoIncrement</code> — pour chaque nouvelle entrée dans cette table, une valeur auto-incrementée sera attributée au champ <code>id</code> sans que le développeur n'ait à le définir. Le champ <code>id</code> est la clé de l'object store: il sera utilisé pour identifier de manière unique les entrées, permettant de les mettre à jour ou les supprimer.</p>
   </li>
   <li>
    <p>On crée deux autres index (champs) en utilisant la méthode {{domxref("IDBObjectStore.createIndex()")}}: <code>title</code> (qui contiendra le titre de chaque note), et <code>body</code> (qui contiendra la description de chaque note).</p>
   </li>
  </ol>
 </li>
</ol>

<p>Avec ce simple schéma de base de données en place, on va pouvoir ajouter des entrées à la base de données, des objets qui ressembleront à ça :</p>

<pre class="brush: js">{
  title: "Acheter du lait",
  body: "Lait de vache et de soja.",
  id: 8
}</pre>

<h3 id="Ajouter_des_données_à_la_base_de_données">Ajouter des données à la base de données</h3>

<p>Maintenant, voyons comment ajouter des entrées dans la base de données. On le fera en utilisant le formulaire de notre page.</p>

<ol>
 <li>
  <p>À la suite du gestionnaire d'événement précédent (mais toujours dans <code>window.onload</code>), ajoutez la ligne suivante — elle définit un gestionnaire d'événement <code>onsubmit</code> pour exécuter la fonction <code>addData()</code> quand le formulaire est soumis (que le {{htmlelement("button")}} envoyer est pressé et que les champs du formulaire sont valides) :</p>

  <pre class="brush: js">// Créer un gestionnaire onsubmit pour appeler la fonction addData() quand le formulaire est soumis
form.onsubmit = addData;</pre>
 </li>
 <li>
  <p>Maintenant, définissons la fonction <code>addData()</code>. Ajoutez ce qui suit après la ligne précédente :</p>

  <pre class="brush: js">// Définit la fonction addData()
function addData(e) {
  // empêcher le formulaire d'être soumis vers le serveur
  e.preventDefault();

  // récupérer les valeurs entrées dans les champs du formulaire
  // et les stocker dans un objet qui sera inséré en BDD
  let newItem = { title: titleInput.value, body: bodyInput.value };

  // ouvrir une transaction en lecture/écriture
  let transaction = db.transaction(['notes'], 'readwrite');

  // récupérer l'object store de la base de données qui a été ouvert avec la transaction
  let objectStore = transaction.objectStore('notes');

  // demander l'ajout de notre nouvel objet à l'object store
  var request = objectStore.add(newItem);
  request.onsuccess = function() {
    // vider le formulaire, pour qu'il soit prêt pour un nouvel ajout
    titleInput.value = '';
    bodyInput.value = '';
  };

  // attendre la fin de la transaction, quand l'ajout a été effectué
  transaction.oncomplete = function() {
    console.log('Transaction completed: database modification finished.');

    // mettre à jour l'affichage pour montrer le nouvel item en exécutant displayData()
    displayData();
  };

  transaction.onerror = function() {
    console.log('Transaction not opened due to error');
  };
}</pre>

  <p>C'est assez complexe, voyons ça pas à pas :</p>

  <ol>
   <li>
    <p>On exécute {{domxref("Event.preventDefault()")}} sur l'objet événement pour empêcher le formulaire d'être véritablement soumis (cela provoquerait une actualisation de la page et gâcherait l'expérience utilisateur).</p>
   </li>
   <li>
    <p>On crée un objet représentant une entrée à ajouter dans la base de données, en le remplissant avec les valeurs des champs du formulaire. Notez qu'on n'a pas besoin d'inclure explicitement une valeur <code>id</code> — comme nous l'avons précédemment expliqué, il est auto-rempli.</p>
   </li>
   <li>
    <p>On ouvre une transaction en lecture/écritre (<code>readwrite</code>) sur l'object store <code>notes</code> en utilisant la méthode {{domxref("IDBDatabase.transaction()")}}. Cet object transaction va nous permettre d'accéder à l'object store, pour ajouter une nouvelle entrée par exemple.</p>
   </li>
   <li>
    <p>On récupère l'object store de la transaction avec la méthode {{domxref("IDBTransaction.objectStore()")}} et on le stocke dans la variable <code>objectStore</code>.</p>
   </li>
   <li>
    <p>On ajoute un nouvel enregistrement à la base de données en utilisant {{domxref("IDBObjectStore.add()")}}. Cela crée une requête, sur le même principe qu'on a déjà vu.</p>
   </li>
   <li>On ajoute des gestionnaires d'événement à <code>request</code> et <code>transaction</code> pour exécuter du code aux points importants de leur cycle de vie :
    <ul>
     <li>Quand la requête a réussit, on efface les champs du formulaire — pour pouvoir ajouter une nouvelle note</li>
     <li>Quand la transaction est terminé, on réexécute la fonction <code>displayData()</code> — pour mettre à jour l'affichage de notes sur la page.</li>
    </ul>
   </li>
  </ol>
 </li>
</ol>

<h3 id="Afficher_les_données">Afficher les données</h3>

<p>Nous avons déjà appelé <code>displayData()</code> deux fois dans notre code, nous allons maintenant définir cette fonction. Ajoutez ce qui suit à votre code, en dessous de la définition de la fonction précédente :</p>

<pre class="brush: js">// Définit la fonction displayData()
function displayData() {
  // Vide le contenu de la liste à chaque fois qu'on la met à jour
  // Si on ne le faisait pas, des duplicats seraient affichés à chaque ajout
  while (list.firstChild) {
    list.removeChild(list.firstChild);
  }

  // Ouvre l'object store puis récupère un curseur - qui va nous permettre d'itérer
  // sur les entrées de l'object store
  let objectStore = db.transaction('notes').objectStore('notes');
  objectStore.openCursor().onsuccess = function(e) {
    // Récupère une référence au curseur
    let cursor = e.target.result;

    // S'il reste des entrées sur lesquelles itérer, on exécute ce code
    if(cursor) {
      // Crée un li, h3, et p pour mettre les données de l'entrée puis les ajouter à la liste
      let listItem = document.createElement('li');
      let h3 = document.createElement('h3');
      let para = document.createElement('p');

      listItem.appendChild(h3);
      listItem.appendChild(para);
      list.appendChild(listItem);

      // Récupère les données à partir du curseur et les met dans le h3 et p
      h3.textContent = cursor.value.title;
      para.textContent = cursor.value.body;

      // Met l'ID de l'entrée dans un attribut du li, pour savoir à quelle entrée il correspond
      // Ce sera utile plus tard pour pouvoir supprimer des entrées
      listItem.setAttribute('data-note-id', cursor.value.id);

      // Crée un bouton et le place dans le li
      let deleteBtn = document.createElement('button');
      listItem.appendChild(deleteBtn);
      deleteBtn.textContent = 'Delete';

      // Définit un gestionnaire d'événement pour appeler deleteItem() quand le bouton supprimer est cliqué
      deleteBtn.onclick = deleteItem;

      // Continue l'itération vers la prochaine entrée du curseur
      cursor.continue();
    } else {
      // Si la liste est vide, affiche un message "Aucune note n'existe"
      if(!list.firstChild) {
        let listItem = document.createElement('li');
        listItem.textContent = 'No notes stored.';
        list.appendChild(listItem);
      }
      // Il n'y a plus d'entrées dans le curseur
      console.log('Notes all displayed');
    }
  };
}</pre>

<p>Encore une fois, pas à pas :</p>

<ol>
 <li>
  <p>D'abord on vide le contenu de l'élément {{htmlelement("ul")}}, pour pouvoir le remplir avec le contenu mis à jour. Si on ne le faisait pas, on obtiendrait une énorme liste de contenus dupliqués à chaque mise à jour.</p>
 </li>
 <li>
  <p>Ensuite, on récupère une référence à l'object store <code>notes</code> en utilisant {{domxref("IDBDatabase.transaction()")}} et {{domxref("IDBTransaction.objectStore()")}} comme nous l'avons fait dans <code>addData()</code>, mais en chaînant ces deux instructions en une seule ligne.</p>
 </li>
 <li>
  <p>L'étape suivante consiste à utiliser la méthode {{domxref("IDBObjectStore.openCursor()")}} pour ouvrir un curseur — une construction qui peut être utilisée pour itérer sur les entrées d'un object store. On chaîne un gestionnaire d'événement <code>onsuccess</code> à la fin de cette opération pour rendre le code plus concis — dès que le curseur est récupéré, le gestionnaire est exécuté.</p>
 </li>
 <li>
  <p>On récupère une référence au curseur lui-même (un objet {{domxref("IDBCursor")}}) avec <code>cursor = e.target.result</code>.</p>
 </li>
 <li>
  <p>Ensuite, on vérifie si le curseur contient une entrée de l'object store (<code>if(cursor){ ... }</code>) — si c'est le cas, on crée des éléments du DOM, les remplit avec les données de l'entrée, et les insère dans la page (à l'intérieur de l'élément <code>&lt;ul&gt;</code>). On inclut un bouton de suppression, qui, quand il est cliqué, supprime l'entrée en cours en appelant la fonction <code>deleteItem()</code> — que nous allons voir dans la section suivante.</p>
 </li>
 <li>
  <p>À la fin du bloc <code>if</code>, on utilise la méthode {{domxref("IDBCursor.continue()")}} pour avancer le curseur à la prochaine entrée dans l'object store et réexécuter le bloc. S'il reste une autre entrée sur laquelle itérer, elle sera à son tour insérée dans la page, <code>continue()</code> sera exécuté à nouveau, et ainsi de suite.</p>
 </li>
 <li>
  <p>Quand il n'y a plus d'enregistrements à parcourir, le curseur retourne <code>undefined</code>, et le bloc <code>else</code> sera donc exécuté à la place. Ce bloc vérifie si des notes ont été insérées dans le <code>&lt;ul&gt;</code> — si ce n'est pas le cas, on insère un message indiquant qu'il n'existe aucune note.</p>
 </li>
</ol>

<h3 id="Supprimer_une_note">Supprimer une note</h3>

<p>Come nous avons vu ci-dessus, lorsque le bouton supprimer est cliqué, la note correspondante est supprimée. Cette action est réalisée par la fonction <code>deleteItem()</code>, que l'on définit ainsi :</p>

<pre class="brush: js">// Définit la fonction deleteItem()
function deleteItem(e) {
  // Récupère l'id de l'entrée que l'on veut supprimer
  // On doit le convertir en nombre avant d'essayer de récupérer l'entrée correspondante dans IDB
  // les clés sont sensibles à la casse
  let noteId = Number(e.target.parentNode.getAttribute('data-note-id'));

  // Ouvre une transaction et supprime la note ayant l'id récupéré ci-dessus
  let transaction = db.transaction(['notes'], 'readwrite');
  let objectStore = transaction.objectStore('notes');
  let request = objectStore.delete(noteId);

  // Indique à l'utilisateur que l'entrée a été supprimée
  transaction.oncomplete = function() {
    // supprime l'élément parent du bouton, le li
    // pour qu'il ne soit plus affiché
    e.target.parentNode.parentNode.removeChild(e.target.parentNode);
    console.log('Note ' + noteId + ' deleted.');

    // Si la liste est vide, affiche un message qui l'indique
    if(!list.firstChild) {
      let listItem = document.createElement('li');
      listItem.textContent = 'No notes stored.';
      list.appendChild(listItem);
    }
  };
}</pre>

<ul>
 <li>On récupère l'ID de l'entrée à supprimer avec <code>Number(e.target.parentNode.getAttribute('data-note-id'))</code> — souvenez-vous qu'on a mis l'ID de l'entrée dans l'attribut <code>data-note-id</code> du <code>&lt;li&gt;</code> au moment de l'afficher. On fait passer l'id à travers l'objet global <a href="/fr/docs/Web/JavaScript/Reference/Objets_globaux/Number">Number()</a>, puisqu'on a actuellement une chaîne de caractères et on a besoin d'un nombre pour qu'il soit reconnu par la base de données.</li>
 <li>On récupère ensuite une référence à l'object store de la même manière que précédemment, et on utilise la méthode {{domxref("IDBObjectStore.delete()")}} pour supprimer l'entrée de la base de données, en lui passant l'ID.</li>
 <li>Quand la transaction est terminée, on supprime le <code>&lt;li&gt;</code> du DOM, et on vérifie si le <code>&lt;ul&gt;</code> est maintenant vide. Si c'est le cas, on insère un message pour l'indiquer.</li>
</ul>

<p>Et voilà ! L'exemple devrait maintenant fonctionner.</p>

<div class="note">
<p><strong>Note :</strong> Si vous rencontrez des difficultés, n'hésitez pas à consulter <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/indexeddb/notes/">notre exemple en direct</a> (ou voir <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/indexeddb/notes/index.js">le code source</a>).</p>
</div>

<h3 id="Stocker_des_données_complexes_avec_IndexedDB">Stocker des données complexes avec IndexedDB</h3>

<p>Comme nous l'avons mentionné auparavant, IndexedDB peut être utilisé pour stocker plus que de simples chaînes de caractères. On peut stocker à peu près tout ce qu'on veux, y compris des objets complexes tels que des vidéos ou des images. Et ce n'est pas plus difficilte à réaliser qu'avec n'importe quel autre type de données.</p>

<p>Pour vous montrer comment le faire, nous avons écrit un autre exemple appelé <a href="https://github.com/mdn/learning-area/tree/master/javascript/apis/client-side-storage/indexeddb/video-store">IndexedDB video store</a> (le <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/indexeddb/video-store/">voir en direct</a>). Lorsque vous exécutez l'exemple pour la première fois, il télécharge des vidéos à partir du réseau, les stocke dans une base de données IndexedDB, puis affiche les vidéos dans des éléments {{htmlelement("video")}} de l'interface utilisateur. Les prochaines fois que vous l'exécutez, il récupère les vidéos de la base de données — cela rend les chargements suivants beaucoup plus rapides et moins gourmands en bande passante.</p>

<p>Passons en revue les parties les plus intéressantes de l'exemple. Nous ne regarderons pas tout — une grande partie est similaire à l'exemple précédent, et le code est bien commenté.</p>

<ol>
 <li>
  <p>Pour cet exemple, nous avons stocké le nom des vidéos à récupérer dans un tableau d'objets :</p>

  <pre class="brush: js">const videos = [
  { 'name' : 'crystal' },
  { 'name' : 'elf' },
  { 'name' : 'frog' },
  { 'name' : 'monster' },
  { 'name' : 'pig' },
  { 'name' : 'rabbit' }
];</pre>
 </li>
 <li>
  <p>Pour commencer, une fois que la base de données a été ouverte, on exécute la fonction <code>init()</code>. Elle boucle sur les noms des vidéos et essaie de charger l'entrée correspondante dans la base de données <code>videos</code>.</p>

  <p>On peut facilement vérifier si une entrée a été trouvée en vérifiant si <code>request.result</code> est évalué à <code>true</code> — si l'entrée n'est pas présente, la valeur retournée est <code>undefined</code>.</p>

  <p>Les vidéos présentes en base de données (stockées sous formes de blobs), sont directement passées à la fonction <code>displayVideo()</code> pour les afficher dans l'interface utilisateur. Pour les vidéos non présentes, on appelle la fonction <code>fetchVideoFromNetwork()</code>, qui récupère la vidéo à partir du réseau.</p>

  <pre class="brush: js">function init() {
  // Boucle sur les vidéos une par une
  for(let i = 0; i &lt; videos.length; i++) {
    // Ouvre une transaction, récupère l'object store, et récupère chaque video par son nom
    let objectStore = db.transaction('videos').objectStore('videos');
    let request = objectStore.get(videos[i].name);
    request.onsuccess = function() {
      // Si l'entrée existe dans la BDD (le résultat n'est pas undefined)
      if(request.result) {
        // Affiche la vidéo en utilisant displayVideo()
        console.log('taking videos from IDB');
        displayVideo(request.result.mp4, request.result.webm, request.result.name);
      } else {
        // Récupère la vidéo à partir du réseau
        fetchVideoFromNetwork(videos[i]);
      }
    };
  }
}</pre>
 </li>
 <li>
  <p>Le bout de code qui suit est extrait de la fonction <code>fetchVideoFromNetwork()</code> — ici, on récupère les versions MP4 et WebM de la vidéos en utilisant deux requêtes {{domxref("fetch()", "WindowOrWorkerGlobalScope.fetch()")}} distinctes. On utilise ensuite la méthode {{domxref("blob()", "Body.blob()")}} pour extraire la réponse sous forme de blob, ce qui nous donne une représentation objet de la vidéo que l'on peut stocker et afficher plus tard.</p>

  <p>Il reste cependant un problème — ces deux requêtes sont asynchrones et ont veut afficher/stocker la vidéo uniquement lorsque les deux promesses sont résolues. Heureusement, il existe une méthode native qui gère ce problème — {{jsxref("Promise.all()")}}. Elle prend un argument — la liste de toutes les promesses qui doivent être attendues — et retourne elle-même une promesse. Quand toutes les promesses sont résolues, alors la promesse de la méthode <code>all()</code> est résolue, avec pour valeur un tableau contenant toutes les valeurs individuelles retournées par les promesses.</p>

  <p>À l'intérieur du bloc <code>all()</code>, vous pouvez voir qu'on appelle la fonction <code>displayVideo()</code>, comme on l'a fait précédemment, pour afficher les vidéos dans l'interface utilisateur, puis la fonction <code>storeVideo()</code> pour stocker ces vidéos dans la base de données.</p>

  <pre class="brush: js">let mp4Blob = fetch('videos/' + video.name + '.mp4').then(response =&gt;
  response.blob()
);
let webmBlob = fetch('videos/' + video.name + '.webm').then(response =&gt;
  response.blob()
);

// Exécuter le bloc de code suivant lorsque les deux promesses sont résolues
Promise.all([mp4Blob, webmBlob]).then(function(values) {
  // Afficher la vidéo récupérée à partir du réseau avec displayVideo()
  displayVideo(values[0], values[1], video.name);
  // La stocker dans IDB avec storeVideo()
  storeVideo(values[0], values[1], video.name);
});</pre>
 </li>
 <li>
  <p>Regardons <code>storeVideo()</code> en premier. Cela ressemble beaucoup à ce qu'on a fait dans l'exemple précédent pour ajouter des données à la base de données — on ouvre une transaction en lecture/écriture et on récupère l'object store de <code>videos</code>, on crée un objet à ajouter à la base de données et on l'ajoute avec {{domxref("IDBObjectStore.add()")}}.</p>

  <pre class="brush: js">function storeVideo(mp4Blob, webmBlob, name) {
  // Ouvre une transaction, récupère object store
  let objectStore = db.transaction(['videos'], 'readwrite').objectStore('videos');
  // Crée une entrée à ajouter à IDB
  let record = {
    mp4 : mp4Blob,
    webm : webmBlob,
    name : name
  }

  // Ajoute l'entrée à IDB avec add()
  let request = objectStore.add(record);

  ...

};</pre>
 </li>
 <li>
  <p>Enfin, <code>displayVideo()</code> crée les éléments DOM nécessaires pour insérer la vidéo dans l'interface utilisateur, puis les ajoute à la page. Les parties les plus intéressantes sont copiées ci-dessous — pour afficher notre blob vidéo dans un élément <code>&lt;video&gt;</code>, on doit créer un objet URL (URL interne qui pointe vers un blob en mémoire) en utilisant la méthode {{domxref("URL.createObjectURL()")}}. Une fois que c'est fait, on peut assigner l'URL comme valeur d'attribut <code>src</code> de l'élément {{htmlelement("source")}}, et ça marche.</p>

  <pre class="brush: js">function displayVideo(mp4Blob, webmBlob, title) {
  // Crée l'objet URL à partir du blob
  let mp4URL = URL.createObjectURL(mp4Blob);
  let webmURL = URL.createObjectURL(webmBlob);

  ...

  let video = document.createElement('video');
  video.controls = true;
  let source1 = document.createElement('source');
  source1.src = mp4URL;
  source1.type = 'video/mp4';
  let source2 = document.createElement('source');
  source2.src = webmURL;
  source2.type = 'video/webm';

  ...
}</pre>
 </li>
</ol>

<h2 id="Stockage_hors-ligne_de_ressources">Stockage hors-ligne de ressources</h2>

<p>L'exemple ci-dessus montre comment créer une application qui stocke des ressources volumineuses dans une base de données IndexedDB, évitant ainsi de devoir les télécharger plus d'une fois. C'est déjà une grande amélioration pour l'expérience utilisateur, mais il manque encore une chose: les fichiers HTML, CSS, et JavaScript doivent encore être téléchargés à chaque fois que le site est accédé, ce qui veut dire qu'il ne fonctionnera pas lorsqu'il n'y a pas de connexion réseau</p>

<p><img alt="" src="ff-offline.png"></p>

<p>C'est là qu'interviennet les <a href="/fr/docs/Web/API/Service_Worker_API">Service workers</a> et l'API étroitement liée, <a href="/fr/docs/Web/API/Cache">Cache</a>.</p>

<h3 id="Service_Worker_Cache">Service Worker / Cache</h3>

<p>Un service worker est un fichier JavaScript qui, pour faire simple, est associé à une origine (un site web à un domaine donné) lorsque le navigateur y accède. Une fois associé, il peut contrôler les pages disponibles pour cette origine. Il le fait en s'installant entre la page chargée et le réseau, interceptant les requêtes réseau visant cette origine.</p>

<p>Quand le service worker intercepte une requête, il peut faire tout ce que vous voulez (voir quelques <a href="/fr/docs/Web/API/Service_Worker_API#Autres_id%C3%A9es_de_cas_d'utilisation">idées de cas d'utilisation</a>), mais l'exemple le plus classique est de sauvegarder les réponses réseau hors-ligne pour fournir ces réponses aux requêtes qui suivent au lieu d'utiliser le réseau. Ainsi, cela vous permet de faire fonctionner un site web complètement hors-ligne.</p>

<p>L'API Cache est un autre mécanisme de stockage côté client, il a été conçu pour enregistrer les réponses HTTP et fonctionne donc très bien en synergie avec les service workers.</p>

<div class="note">
<p><strong>Note :</strong> Les Service workers et Cache sont pris en charge par la plupart des navigateurs modernes aujourd'hui. Au moment de la rédaction de cet article, Safari était encore occupé à l'implémenter, mais il devrait bientôt être disponible.</p>
</div>

<h3 id="Un_exemple_service_worker">Un exemple service worker</h3>

<p>Voyons un exemple, pour vous donner une idée de ce à quoi cela pourrait ressembler. Nous avons crée une autre version de l'exemple video store vu précédemment. Cela fonctionne de manière identique, mais enregistre également le HTML, CSS, et JavaScript dans l'API Cache via un service worker, permettant à l'exemple de marcher hors ligne!</p>

<p>Voir <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/">IndexedDB video store avec service worker en direct</a>, ou <a href="https://github.com/mdn/learning-area/tree/master/javascript/apis/client-side-storage/cache-sw/video-store-offline">voir le code source</a>.</p>

<h3 id="Enregistrer_le_service_worker">Enregistrer le service worker</h3>

<p>La première chose à noter est qu'il  a un peu plus de code placé dans le fichier JavaScript principal (voir <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.js#L144">index.js</a>):</p>

<pre class="brush: js">// Enregistre un service worker pour contrôler le site hors-ligne
if('serviceWorker' in navigator) {
  navigator.serviceWorker
           .register('/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js')
           .then(function() { console.log('Service Worker Registered'); });
}</pre>

<ul>
 <li>On effectue d'abord un test de détection de fonctionnalité pour vérifier si l'objet <code>serviceWorker</code> existe dans l'objet {{domxref("Navigator")}}. Si c'est le cas, alors on sait qu'au moins les fonctionnalités de base des service workers sont prises en charge.</li>
 <li>On utilise la méthode {{domxref("ServiceWorkerContainer.register()")}} afin d'enregistrer le service worker <code>sw.js</code> pour l'origine où il se situe, ainsi il pourra contrôler les pages qui sont dans le même répertoire que lui, ou dans un sous-répertoire.</li>
 <li>Lorsque la promesse est résolue, c'est que le service worker est enregistré.</li>
</ul>

<div class="note">
<p><strong>Note :</strong> Le chemin du fichier <code>sw.js</code> est relatif à l'origine du site, et non au fichier JavaScript qui l'appelle.<br>
 Le service worker est sur <code>https://mdn.github.io/learning-area/.../sw.js</code>. L'origine est <code>https://mdn.github.io</code>. Le chemin donné doit donc être <code>/learning-area/.../sw.js</code>.<br>
 Si vous vouliez héberger cet exemple sur votre propre serveur, vous devriez changer le chemin en conséquence. C'est plutôt inhabituel, mais cela doit fonctionner de cette façon pour des raisons de sécurité.</p>
</div>

<h3 id="Installer_le_service_worker">Installer le service worker</h3>

<p>Quand une page sous le contrôle du service worker est appelée (par exemple lorsque l'exemple est rechargé), alors le service worker est installé par rapport à cette page et il peut commencer à la contrôler. Quand cela arrive, un événement <code>install</code> est déclenché sur le service worker; vous pouvez écrire du code dans le service worker pour qu'il réponde à cette installation.</p>

<p>Prenons pour exemple le fichier <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js">sw.js</a> (le service worker) :</p>

<pre class="brush: js">self.addEventListener('install', function(e) {
 e.waitUntil(
   caches.open('video-store').then(function(cache) {
     return cache.addAll([
       '/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/',
       '/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.html',
       '/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.js',
       '/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/style.css'
     ]);
   })
 );
});</pre>

<ol>
 <li>
  <p>Le gestionnaire d'événément <code>install</code> est enregistré sur <code>self</code>. Le mot-clé <code>self</code> est un moyen de faire référence au service worker de la portée globale à partir de son fichier.</p>
 </li>
 <li>
  <p>À l'intérieur du gestionnaire d'installation, on utilise la méthode {{domxref("ExtendableEvent.waitUntil()")}}, disponible sur l'objet événement, pour signaler que le navigateur ne doit pas terminer l'installation du service worker avant que la promesse qu'il contient ne soit résolue avec succès.</p>
 </li>
 <li>
  <p>Ici, on voit l'API Cache en action: on utilise la méthode {{domxref("CacheStorage.open()")}} pour ouvrir un nouvel objet cache dans lequel les réponses seront stockées (similaire à un object store IndexedDB). Cette promesse se résout avec un objet {{domxref("Cache")}} représentant le cache du <code>video-store</code>.</p>
 </li>
 <li>
  <p>On utilise la méthode {{domxref("Cache.addAll()")}} pour récupérer une série de ressources et ajouter leur réponse au cache.</p>
 </li>
</ol>

<p>C'est tout pour l'instant, l'installation est terminée.</p>

<h3 id="Répondre_aux_futures_requêtes">Répondre aux futures requêtes</h3>

<p>Avec le service worker enregistré et installé pour notre page HTML, et les ressources pertinentes ajoutées au cache, on est presque prêts. Il n'y a plus qu'une chose à faire: écrire du code pour répondre aux prochaines requêtes réseau.</p>

<p>C'est ce que fait le second bloc de code dans <code>sw.js</code> :</p>

<pre class="brush: js">self.addEventListener('fetch', function(e) {
  console.log(e.request.url);
  e.respondWith(
    caches.match(e.request).then(function(response) {
      return response || fetch(e.request);
    })
  );
});</pre>

<ol>
 <li>
  <p>On ajoute un deuxième gestionnaire d'événement au service worker, qui exécute une fonction quand l'événement <code>fetch</code> est déclenché. Cela arrive quand le navigateur requête une ressource dans le même répertoire que le service worker (ou sous-répertoire).</p>
 </li>
 <li>
  <p>À l'intérieur de cette fonction, on affiche l'URL de la ressource demandée dans la console, et on utilise la méthode {{domxref("FetchEvent.respondWith()")}} pour retourner une réponse personnalisée à la requête.</p>
 </li>
 <li>
  <p>Pour construire la réponse, on utilise d'abord {{domxref("CacheStorage.match()")}} afin de vérifier si la requête est en cache (qu'une requête correspond à l'URL demandée est en cache).</p>
 </li>
 <li>
  <p>Si elle est trouvée, la promesse se résout avec la réponse correspondante; sinon, avec <code>undefined</code>. Dans ce cas, on récupère la réponse à partir du réseau, en utilisant <code>fetch()</code>, et on retourne le résultat.</p>
 </li>
</ol>

<p>C'est tout pour notre service worker. Il y a tout un tas de choses que vous pouvez faire avec — pour plus de détails, consultez le <a href="https://serviceworke.rs/">service worker cookbook</a>. Et merci à Paul Kinlan pour son article <a href="https://developers.google.com/web/fundamentals/codelabs/offline/">Adding a Service Worker and Offline into your Web App</a>, qui a inspiré cet exemple.</p>

<h3 id="Tester_lexemple_hors-ligne">Tester l'exemple hors-ligne</h3>

<p>Pour tester notre <a href="https://mdn.github.io/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/">exemple de service worker</a>, rechargez d'abord la page pour vous assurer qu'il est bien installé. Une fois que c'est fait, vous pouvez soit:</p>

<ul>
 <li>Débrancher votre réseau ou éteindre votre Wifi.</li>
 <li>Si vous utilisez Firefox: Sélectionner <em>Fichier &gt; Travailler hors-connexion</em>.</li>
 <li>Si vous utilisez Chrome: Aller dans les DevTols, puis choisir <em>Application &gt; Service Workers</em>, et cocher la case à cocher <em>Offline</em>.</li>
</ul>

<p>Si vous actualisez votre page d'exemple, vous devriez toujours la voir se charger normalemment. Tout est stocké hors connexion — les ressources de la page dans Cache et les vidéos dans une base de données IndexedDB.</p>

<h2 id="Sommaire">Sommaire</h2>

<p>C'est tout pour l'instant. Nous espérons que vous avez trouvé notre récapitulatif des technologies de stockage côté client utile.</p>

<h2 id="Voir_aussi">Voir aussi</h2>

<ul>
 <li><a href="/fr/docs/Web/API/Web_Storage_API">Web storage API</a></li>
 <li><a href="/fr/docs/Web/API/API_IndexedDB">IndexedDB API</a></li>
 <li><a href="/fr/docs/Web/HTTP/Cookies">Cookies</a></li>
 <li><a href="/fr/docs/Web/API/Service_Worker_API">Service worker API</a></li>
</ul>

<p>{{PreviousMenu("Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}</p>

<h2 id="Dans_ce_module">Dans ce module</h2>

<ul>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Introduction">Introduction aux API du Web</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Manipulating_documents">Manipuler des documents</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Fetching_data">Récupérer des données du serveur</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Third_party_APIs">APIs tierces</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Drawing_graphics">Dessiner des éléments graphiques</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Video_and_audio_APIs">APIs vidéo et audio</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Client-side_storage">Stockage côté client</a></li>
</ul>