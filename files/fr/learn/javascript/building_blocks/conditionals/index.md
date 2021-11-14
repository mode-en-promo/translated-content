---
title: Prendre des décisions dans le code — conditions
slug: Learn/JavaScript/Building_blocks/conditionals
tags:
  - Article
  - CodingScripting
  - Conditionnel
  - Débutant
  - JavaScript
  - Switch
  - conditions
  - else
  - if
  - ternaire
translation_of: Learn/JavaScript/Building_blocks/conditionals
original_slug: Apprendre/JavaScript/Building_blocks/conditionals
---
<p>{{LearnSidebar}}</p>

<p>{{NextMenu("Apprendre/JavaScript/Building_blocks/Looping_code", "Apprendre/JavaScript/Building_blocks")}}</p>

<p>Dans tout langage de programmation, le code doit prendre des décisions et agir en fonction des différents paramètres. Par exemple dans un jeu, si le nombre de vies du joueur atteint 0, alors le jeu est terminé. Dans une application météo, si elle est consultée le matin, l'application montrera une image du lever de soleil ; l'application proposera des étoiles et la lune s'il fait nuit. Dans cet article nous allons découvrir comment ces instructions conditionnelles fonctionnent en JavaScript.</p>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="row">Prérequis :</th>
   <td>Connaissances du vocabulaire informatique, compréhension des bases du HTML et des CSS, <a href="/fr/docs/Learn/JavaScript/First_steps">Premiers pas en JavaScript</a>.</td>
  </tr>
  <tr>
   <th scope="row">Objectif :</th>
   <td>Comprendre comment utiliser les structures conditionnelles en JavaScript.</td>
  </tr>
 </tbody>
</table>

<h2 id="Vous_laurez_à_une_condition_!..">Vous l'aurez à une condition !..</h2>

<p>Les êtres humains (et d'autres animaux) prennent tout le temps des décisions qui affectent leur vie, de la plus insignifiante (« Est‑ce que je devrais prendre un biscuit ou deux ? ») à la plus importante (« Est‑ce que je dois rester dans mon pays natal et travailler à la ferme de mon père, ou déménager aux États-Unis et étudier l'astrophysique ? »)</p>

<p>Les instructions conditionnelles nous permettent de représenter ce genre de prise de décision en JavaScript, du choix qui doit être fait (par ex. « un biscuit ou deux »), à la conséquence de ces choix (il se peut que la conséquence de « manger un biscuit » soit « avoir encore faim », et celle de « manger deux biscuits » soit « se sentir rassasié, mais se faire gronder par maman pour avoir mangé tous les biscuits ».)</p>

<p><img alt="" src="cookie-choice-small.png"></p>

<h2 id="Instruction_if_..._else">Instruction if ... else</h2>

<p>Intéressons nous de plus près à la forme la plus répandue d'instruction conditionnelle que vous utiliserez en JavaScript — la modeste <a href="/fr/docs/Web/JavaScript/Reference/Instructions/if...else">instruction</a> <code><a href="/fr/docs/Web/JavaScript/Reference/Instructions/if...else">if ... else</a></code>.</p>

<h3 id="Syntaxe_élémentaire_if_..._else">Syntaxe élémentaire if ... else</h3>

<p>La syntaxe élémentaire de <code>if...else</code> ressemble à cela en {{glossary("pseudocode")}}:</p>

<pre>if (condition) {
  code à exécuter si la condition est true
} else {
  sinon exécuter cet autre code à la place
}</pre>

<p>Ici nous avons:</p>

<ol>
 <li>Le mot‑clé <code>if</code> suivie de parenthèses.</li>
 <li>Une condition à évaluer, placée entre les parenthèses (typiquement « cette valeur est‑elle plus grande que cet autre valeur ? » ou « cette valeur existe‑t‑elle ? »). Cette condition se servira des <a href="/fr/docs/Learn/JavaScript/First_steps/Math#Comparison_operators">opérateurs de comparaison</a> que nous avons étudié dans le précédent module, et renverra <code>true</code> ou <code>false</code>.</li>
 <li>Une paire d'accolades, à l'intérieur de laquelle se trouve du code — cela peut être n'importe quel code voulu ; il sera exécuté seulement si la condition renvoie <code>true</code>.</li>
 <li>Le mot‑clé <code>else</code>.</li>
 <li>Une autre paire d'accolades, à l'intérieur de laquelle se trouve du code différent — tout code souhaité et il sera exécuté seulement si la condition ne renvoie pas <code>true</code>.</li>
</ol>

<p>Ce code est facile à lire pour une personne — il dit « <strong>si</strong> la <strong>condition</strong> renvoie <code>true</code>, exécuter le code A, <strong>sinon</strong> exécuter le code B ».</p>

<p>Notez qu'il n'est pas nécessaire d'inclure une instruction <code>else</code> et le deuxième bloc entre accolades — le code suivant est aussi parfaitement correct :</p>

<pre>if (condition) {
  code à exécuter si la condition est true
}

exécuter un autre code</pre>

<p>Cependant, vous devez faire attention ici — dans ce cas, le deuxième bloc de code n'est pas controlé par l'instruction conditionnelle, donc il sera <strong>toujours</strong> exécuté, que la condition ait renvoyé <code>true</code> ou <code>false</code>. Ce n'est pas nécessairement une mauvaise chose, mais il se peut que ce ne soit pas ce que vous vouliez — le plus souvent vous voudrez exécuter un bloc de code <em>ou</em> l'autre, et non les deux.</p>

<p>Une dernière remarque, vous verrez quelques fois les instructions <code>if...else</code> écrites sans accolades, de manière abrégée, ainsi :</p>

<pre>if (condition) code à exécuter si la condition est true
else exécute un autre code à la place</pre>

<p>Ce code est parfaitement valide, mais il n'est pas recommandé — il est nettement plus facile de lire le code et d'en déduire ce qui se passe si vous utilisez des accolades pour délimiter les blocs de code, des lignes séparées et des indentations.</p>

<h3 id="Un_exemple_concret">Un exemple concret</h3>

<p>Pour mieux comprendre cette syntaxe, prenons un exemple concret. Imaginez un enfant à qui le père ou la mère demande de l'aide pour une tâche. Le parent pourrait dire « Mon chéri, si tu m'aides en allant faire les courses, je te donnerai un peu plus d'argent de poche pour que tu puisses t'acheter ce jouet que tu voulais ». En JavaScript, on pourrait le représenter de cette manière :</p>

<pre class="brush: js">let coursesFaites = false;

if (coursesFaites === true) {
  let argentDePoche = 10;
} else {
  let argentDePoche = 5;
}</pre>

<p>Avec un tel code, la variable <code>coursesFaites</code> renvoie toujours <code>false</code>, imaginez la déception de ce pauvre enfant. Il ne tient qu'à nous de fournir un mécanisme pour que le parent assigne <code>true</code> à la variable <code>coursesFaites</code> si l'enfant a fait les courses.</p>

<div class="note">
<p><strong>Note :</strong> Vous pouvez voir une <a href="https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/allowance-updater.html">version plus complète de cet exemple sur GitHub</a> (ainsi qu'en <a href="http://mdn.github.io/learning-area/javascript/building-blocks/allowance-updater.html">version live</a>.)</p>
</div>

<h3 id="else_if">else if</h3>

<p>Il n'y a qu'une alternative dans l'exemple précédent — mais qu'en est‑il si l'on souhaite plus de choix ?</p>

<p>Il existe un moyen d'enchaîner des choix / résultats supplémentaires à <code>if...else</code> — en utilisant <code>else if</code> entre. Chaque choix supplémentaire nécessite un bloc additionnel à placer entre <code>if() { ... }</code> et <code>else { ... }</code> — regardez l'exemple suivant plus élaboré, qui pourrait faire partie d'une simple application de prévisions météo:</p>

<pre class="brush: html">&lt;label for="weather"&gt;Select the weather type today: &lt;/label&gt;
&lt;select id="weather"&gt;
  &lt;option value=""&gt;--Make a choice--&lt;/option&gt;
  &lt;option value="sunny"&gt;Sunny&lt;/option&gt;
  &lt;option value="rainy"&gt;Rainy&lt;/option&gt;
  &lt;option value="snowing"&gt;Snowing&lt;/option&gt;
  &lt;option value="overcast"&gt;Overcast&lt;/option&gt;
&lt;/select&gt;

&lt;p&gt;&lt;/p&gt;</pre>

<pre class="brush: js">const select = document.querySelector('select');
const para = document.querySelector('p');

select.addEventListener('change', setWeather);

function setWeather() {
  const choice = select.value;

  if (choice === 'sunny') {
    para.textContent = 'It is nice and sunny outside today. Wear shorts! Go to the beach, or the park, and get an ice cream.';
  } else if (choice === 'rainy') {
    para.textContent = 'Rain is falling outside; take a rain coat and a brolly, and don\'t stay out for too long.';
  } else if (choice === 'snowing') {
    para.textContent = 'The snow is coming down — it is freezing! Best to stay in with a cup of hot chocolate, or go build a snowman.';
  } else if (choice === 'overcast') {
    para.textContent = 'It isn\'t raining, but the sky is grey and gloomy; it could turn any minute, so take a rain coat just in case.';
  } else {
    para.textContent = '';
  }
}</pre>

<p>{{ EmbedLiveSample('else_if', '100%', 100) }}</p>

<ol>
 <li>Ici nous avons l'élément HTML {{htmlelement("select")}} nous permettant de sélectionner divers choix de temps et un simple paragraphe.</li>
 <li>Dans le JavaScript, nous conservons une référence aussi bien à l'élément {{htmlelement("select")}} qu'à l'élément {{htmlelement("p")}}, et ajoutons un écouteur d'évènement à l'élément <code>&lt;select&gt;</code> de sorte que la fonction <code>setWeather()</code> soit exécutée quand sa valeur change.</li>
 <li>Quand cette fonction est exécutée, nous commençons par assigner à la variable <code>choice</code> la valeur actuellement sélectionnée dans l'élément <code>&lt;select&gt;</code>. Nous utilisons ensuite une instruction conditionnelle pour montrer différents textes dans le paragraphe en fonction de la valeur de <code>choice</code>. Remarquez comment toutes les conditions sont testées avec des blocs <code>else if() {...}</code>, mis à part le tout premier testé avec un  <code>bloc if() {...}</code>.</li>
 <li>Le tout dernier choix, à l'intérieur du bloc <code>else {...}</code>, est simplement une option de "secours" — le code qui s'y trouve ne sera exécuté que si aucune des conditions n'est <code>true</code>. Dans ce cas, il faut vider le texte du paragraphe si rien n'est sélectionné, par exemple si un utilisateur décide de resélectionner le texte à substituer « --Choisir-- » présenté au début.</li>
</ol>

<div class="note">
<p><strong>Note :</strong> Vous trouverez également <a href="https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/simple-else-if.html">cet exemple sur GitHub</a> (ainsi qu'en <a href="http://mdn.github.io/learning-area/javascript/building-blocks/simple-else-if.html">version live</a> ici.)</p>
</div>

<h3 id="Une_note_sur_les_opérateurs_de_comparaison">Une note sur les opérateurs de comparaison</h3>

<p>Les opérateurs de comparaison sont utilisés pour tester les conditions dans nos instructions conditionnelles. Nous avons d'abord regardé les opérateurs de comparaison dans notre <a href="/fr/docs/Learn/JavaScript/First_steps/Math#Opérateurs_de_comparaison">Mathématiques de base en JavaScript — nombres et opérateurs</a> article. Nos choix sont :</p>

<ul>
 <li><code>===</code> et <code>!==</code> — teste si une valeur est identique ou non à une autre.</li>
 <li><code>&lt;</code> and <code>&gt;</code> —teste si une valeur est inférieure ou non à une autre.</li>
 <li><code>&lt;=</code> and <code>&gt;=</code> — teste si une valeur est inférieur ou égal, ou égal à, ou supérieur ou égal à une autre.</li>
</ul>

<div class="note">
<p><strong>Note :</strong> Revoyez le contenu du lien précédent si vous voulez vous rafraîchir la mémoire.</p>
</div>

<p>Nous souhaitons mentionner à propos des tests des valeurs booléennes (<code>true</code>/<code>false</code>) un modèle courant que vous rencontrerez souvent. Toute valeur autre que <code>false</code>, <code>undefined</code>, <code>null</code>, <code>0</code>, <code>NaN</code> ou une chaîne vide  (<code>''</code>) renvoie <code>true</code> lorsqu'elle est testée dans une structure conditionnelle, vous pouvez donc simplement utiliser un nom de variable pour tester si elle est <code>true</code>, ou même si elle existe (c'est-à-dire si elle n'est pas <code>undefined</code>).<br>
 Par exemple :</p>

<pre class="brush: js">const fromage = 'Comté';

if (fromage) {
  console.log('Ouaips ! Du fromage pour mettre sur un toast.');
} else {
  console.log('Pas de fromage sur le toast pour vous aujourd\'hui.');
}</pre>

<p>Et, revenant à notre exemple précédent sur l'enfant rendant service à ses parents, vous pouvez l'écrire ainsi :</p>

<pre class="brush: js">let coursesFaites = false;

if (coursesFaites) { // pas besoin d'écrire explicitement '=== true'
  let argentDePoche = 10;
} else {
  let argentDePoche = 5;
}</pre>

<h3 id="if_..._else_imbriqué"> if ... else imbriqué</h3>

<p>Il est parfaitement correct d'ajouter une déclaration <code>if...else</code> à l'intérieur d'une autre — pour les imbriquer. Par exemple, nous pourrions mettre à jour notre application de prévisions météo pour montrer un autre ensemble de choix en fonction de la température :</p>

<pre class="brush: js">if (choice === 'sunny') {
  if (temperature &lt; 86) {
    para.textContent = 'Il fait ' + temperature + ' degrés dehors — beau et ensoleillé. Allez à la plage ou au parc et achetez une crème glacée.';
  } else if (temperature &gt;= 86) {
    para.textContent = 'Il fait ' + temperature + ' degrés dehors — VRAIMENT CHAUD ! si vous voulez sortir, n\'oubliez pas de mettre de la crème solaire.';
  }
}</pre>

<p>Même si tout le code fonctionne ensemble, chaque déclaration <code>if...else</code> fonctionne indépendamment de l'autre.</p>

<h3 id="Opérateurs_logiques_AND_OR_et_NOT">Opérateurs logiques AND, OR et NOT</h3>

<p>Si vous voulez tester plusieurs conditions sans imbriquer des instructions <code>if...else</code> , les <a href="/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/Op%C3%A9rateurs_logiques">opérateurs logiques</a> pourront vous rendre service. Quand ils sont utilisés dans des conditions, les deux premiers sont représentés comme ci dessous :</p>

<ul>
 <li><code>&amp;&amp;</code> — AND ; vous permet d'enchaîner deux ou plusieurs expressions de sorte que toutes doivent être individuellement égales à <code>true</code> pour que l'enemble de l'expression retourne <code>true</code>.</li>
 <li><code>||</code> — OR ; vous permet d'enchaîner deux ou plusieurs expressions ensemble de sorte qu'il suffit qu'une au plus soit évaluée comme étant  <code>true</code> pour que l'ensemble de l'expression renvoie <code>true</code>.</li>
</ul>

<p>Pour vous donner un exemple de AND, le morceau de code précedent peut être réécrit ainsi :</p>

<pre class="brush: js">if (choice === 'sunny' &amp;&amp; temperature &lt; 86) {
  para.textContent = 'Il fait ' + temperature + ' degrés dehors — beau temps ensoleillé. Allez à la plage ou au parc et achetez une crème glacée.';
} else if (choice === 'sunny' &amp;&amp; temperature &gt;= 86) {
  para.textContent = 'Il fait ' + temperature + ' degrés dehors — VRAIMENT CHAUD ! Si vous voulez sortir, assurez‑vous d'avoir passé une crème solaire.';
}</pre>

<p>Ainsi, par exemple, le premier bloc de code ne sera exécuté que si <code>choice === 'sunny'</code> <em>ET</em> <code>temperature &lt; 86</code> renvoient tous deux <code>true</code>.</p>

<p>Voyons un petit exemple avec OR :</p>

<pre class="brush: js">if (camionDeGlaces || etatDeLaMaison === 'on fire') {
  console.log('Vous devriez sortir de la maison rapidement.');
} else {
  console.log('Vous pouvez probablement rester dedans.');
}</pre>

<p>Le dernier type d'opérateur logique, NOT, exprimé par l'opérateur <code>!</code>,  peut s'utiliser pour nier une expression. Combinons‑le avec OR dans cet exemple :</p>

<pre class="brush: js">if (!(camionDeGlaces || etatDeLaMaison === 'on fire')) {
  console.log('Vous pouvez probablement rester dedans.');
} else {
  console.log('Vous devriez sortir de la maison rapidement.');
}</pre>

<p>Dans cet extrait, si la déclaration avec OR renvoie <code>true</code>, l'opérateur NOT va nier l'ensemble : l'expression retournera donc <code>false</code>.</p>

<p>Vous pouvez combiner autant d'instructions logiques que vous le souhaitez, quelle que soit la structure. L'exemple suivant n'exécute le code entre accolades que si les deux instructions OR renvoient true, l'instruction AND recouvrante renvoie alors <code>true</code> :</p>

<pre class="brush: js">if ((x === 5 || y &gt; 3 || z &lt;= 10) &amp;&amp; (loggedIn || userName === 'Steve')) {
  // exécuter le code
}</pre>

<p>Une erreur fréquente avec l'opérateur OR dans des instructions conditionnelles est de n'indiquer la variable dont vous testez la valeur qu'une fois, puis de donner une liste de valeurs sensées renvoyer <code>true</code> séparées par des || (OR) opérateurs. Par exemple :</p>

<pre class="example-bad brush: js">if (x === 5 || 7 || 10 || 20) {
  // exécuter le code
}</pre>

<p>Dans ce cas, la condition dans le <code>if(...) </code>sera toujours évaluée à vrai puisque 7 (ou toute autre valeur non nulle) est toujours <code>true</code>. Cette condition dit en réalité « si x est égal à 5, ou bien 7 est vrai » — ce qui est toujours le cas. Ce n'est pas ce que nous voulons logiquement ! Pour que cela fonctionne, vous devez définir un test complet entre chaque opérateur OR :</p>

<pre class="brush: js">if (x === 5 || x === 7 || x === 10 ||x === 20) {
  // exécuter le code
}</pre>

<h2 id="Instruction_switch">Instruction switch</h2>

<p>Les Instructions <code>if...else</code>  font bien le travail d'aiguiller la programmation selon des conditions, mais elles ne sont pas sans inconvénient. Elles sont principalement adaptées aux cas où vous avez un choix binaire, chacun nécessitant une quantité raisonnable de code à exécuter, et/ou au cas où les conditions sont complexes (par ex. plusieurs opérateurs logiques). Si vous voulez juste fixer la valeur d'une variable à un choix donné ou afficher une déclaration particulière en fonction d'une condition, cette syntaxe peut devenir un peu lourde, surtout si le nombre de choix est important.</p>

<p>Les <a href="/fr/docs/Web/JavaScript/Reference/Instructions/switch">instructions switch</a> sont vos amies — elles prennent une seule valeur ou expression en entrée, puis examinent une palette de choix jusqu'à trouver celui qui correspond, et exécutent le code qui va avec. Voici un peu de pseudo-code, pour vous donner l'idée :</p>

<pre class="brush: js"><strong>switch (expression) {</strong>
  <strong>case</strong> choix1<strong>:</strong>
    exécuter ce code
    <strong>break;</strong>

  <strong>case</strong> choix2<strong>:</strong>
    exécuter ce code à la place
    <strong>break;</strong>

  // incorporez autant de <strong>case</strong> que vous le souhaitez

  <strong>default:</strong>
    sinon, exécutez juste ce code
<strong>}</strong></pre>

<p>Ici nous avons</p>

<ol>
 <li>Le mot‑clé <code>switch</code> suivi de parenthèses.</li>
 <li>Une expression ou une valeur mise entre les parenthèses.</li>
 <li>Le mot‑clé <code>case</code> suivi d'une expression ou d'une valeur, et de deux‑points.</li>
 <li>Le code exécuté si l'expression/valeur de <code>case</code> correspond à celles de <code>switch</code>.</li>
 <li>Une déclaration <code>break</code>, suivie d'un point‑virgule. Si le choix précédent correspond à l'expression/valeur, le navigateur va stopper l'exécution du bloc de code ici et continuer après l'instruction <strong>switch</strong>.</li>
 <li>Vous pouvez rajouter autant de <strong>cas</strong> que vous le souhaitez. (points 3–5)</li>
 <li>Le mot‑clé <code>default</code>,  suivi d'une même structure de code qu'aux points 3-5, sauf que <code>default</code> n'a pas de choix après lui et n'a donc pas besoin de l'instruction <code>break</code>  puisqu'il n'y a plus rien à exécuter après ce bloc. C'est l'option <code>default</code> qui sera exécutée si aucun choix ne correspond.</li>
</ol>

<div class="note">
<p><strong>Note :</strong> Vous n'avez pas à inclure la section  <code>default</code> — elle peut être omise en toute sécurité s'il n'y a aucune chance que l'expression finisse par égaler une valeur inconnue. À contrario, vous devez l'inclure s'il est possible qu'il y ait des cas inconnus.</p>
</div>

<h3 id="Un_exemple_de_switch">Un exemple de switch</h3>

<p>Voyons un exemple concret — nous allons réécrire notre application de prévision météo en utilisant une instruction <code>switch</code> à la place :</p>

<pre class="brush: html">&lt;label for="weather"&gt;Select the weather type today: &lt;/label&gt;
&lt;select id="weather"&gt;
  &lt;option value=""&gt;--Make a choice--&lt;/option&gt;
  &lt;option value="sunny"&gt;Sunny&lt;/option&gt;
  &lt;option value="rainy"&gt;Rainy&lt;/option&gt;
  &lt;option value="snowing"&gt;Snowing&lt;/option&gt;
  &lt;option value="overcast"&gt;Overcast&lt;/option&gt;
&lt;/select&gt;

&lt;p&gt;&lt;/p&gt;</pre>

<pre class="brush: js">const select = document.querySelector('select');
const para = document.querySelector('p');

select.addEventListener('change', setWeather);


function setWeather() {
  let choice = select.value;

  switch (choice) {
    case 'sunny':
      para.textContent = 'It is nice and sunny outside today. Wear shorts! Go to the beach, or the park, and get an ice cream.';
      break;
    case 'rainy':
      para.textContent = 'Rain is falling outside; take a rain coat and a brolly, and don\'t stay out for too long.';
      break;
    case 'snowing':
      para.textContent = 'The snow is coming down — it is freezing! Best to stay in with a cup of hot chocolate, or go build a snowman.';
      break;
    case 'overcast':
      para.textContent = 'It isn\'t raining, but the sky is grey and gloomy; it could turn any minute, so take a rain coat just in case.';
      break;
    default:
      para.textContent = '';
  }
}</pre>

<p>{{ EmbedLiveSample('Un_exemple_de_switch', '100%', 100) }}</p>

<div class="note">
<p><strong>Note :</strong> Vous trouverez également cet <a href="https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/simple-switch.html">exemple sur GitHub</a> (voyez‑le en <a href="http://mdn.github.io/learning-area/javascript/building-blocks/simple-switch.html">cours d'exécution </a>ici aussi.)</p>
</div>

<h2 id="Opérateur_ternaire">Opérateur ternaire</h2>

<p>Voici une dernière syntaxe que nous souhaitons vous présenter avant de nous amuser avec quelques exemples. L'<a href="/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/L_op%C3%A9rateur_conditionnel">opérateur ternaire ou conditionnel</a> est un petit morceau de code qui teste une condition et renvoie une valeur ou expression si elle est <code>true</code> et une autre si elle est <code>false</code> — elle est utile dans certains cas, et occupe moins de place qu'un bloc <code>if...else</code> si votre choix est limité à deux possibilités à choisir via une condition <code>true</code>/<code>false</code>. Voici le pseudo‑code correspondant :</p>

<pre>( condition ) ? exécuter ce code : exécuter celui‑ci à la place</pre>

<p>Regardons cet exemple simple :</p>

<pre class="brush: js">let formuleDePolitesse = ( est_anniversaire ) ? 'Bon anniversaire Mme Smith — nous vous souhaitons une belle journée !' : 'Bonjour Mme Smith.';</pre>

<p>Ici, nous avons une variable nommée <code>est_anniversaire</code> — si elle est <code>true</code>, nous adressons à notre hôte un message de « Bon anniversaire » ; si ce n'est pas le cas, c'est-à-dire si <code>est_anniversaire</code> renvoie <code>false</code>, nous disons simplement « Bonjour ».</p>

<h3 id="Exemple_opérateur_ternaire">Exemple opérateur ternaire</h3>

<p>L'opérateur ternaire ne sert pas qu'à définir des valeurs de variables ; vous pouvez aussi exécuter des fonctions, ou des lignes de code — ce que vous voulez. Voici un exemple concret de choix de thème où le style du site est déterminé grâce à un opérateur ternaire.</p>

<pre class="brush: html">&lt;label for="theme"&gt;Select theme: &lt;/label&gt;
&lt;select id="theme"&gt;
  &lt;option value="white"&gt;White&lt;/option&gt;
  &lt;option value="black"&gt;Black&lt;/option&gt;
&lt;/select&gt;

&lt;h1&gt;This is my website&lt;/h1&gt;</pre>

<pre class="brush: js">const select = document.querySelector('select');
const html = document.querySelector('html');
document.body.style.padding = '10px';

function update(bgColor, textColor) {
  html.style.backgroundColor = bgColor;
  html.style.color = textColor;
}

select.onchange = function() {
  ( select.value === 'black' ) ? update('black','white') : update('white','black');
}
</pre>

<p>{{ EmbedLiveSample('Exemple_opérateur_ternaire', '100%', 300, "", "", "hide-codepen-jsfiddle") }}</p>

<p>Nous mettons un élément {{htmlelement('select')}} pour choisir un thème (noir ou blanc), plus un simple élément {{htmlelement('h1')}} pour afficher un titre de site web. Nous avons aussi une fonction <code>update()</code>, qui prend deux couleurs en paramètre (entrées). La couleur de fond du site est déterminée par la couleur indiquée dans le premier paramètre fourni, et la couleur du texte par le deuxième.</p>

<p>Nous avons également mis un écouteur d'événement <a href="/fr/docs/Web/API/GlobalEventHandlers/onchange">onchange</a> qui sert à exécuter une fonction contenant un opérateur ternaire. Il débute par un test de condition — <code>select.value === 'black'</code>. Si le test renvoie <code>true</code>, nous exécutons la fonction <code>update()</code> avec les paramètres blanc et noir : cela signifie que le fond sera noir et le texte blanc. S'il renvoie <code>false</code>, nous exécutons <code>update()</code> avec les paramètres noir et blanc, les couleurs du site seront inversées.</p>

<div class="note">
<p><strong>Note :</strong> Vous trouverez également cet <a href="https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/simple-ternary.html">exemple sur GitHub</a> (voyez‑le en <a href="http://mdn.github.io/learning-area/javascript/building-blocks/simple-ternary.html">cours d'exécution </a>ici aussi.)</p>
</div>

<h2 id="Apprentissage_actif_un_calendrier_simple">Apprentissage actif : un calendrier simple</h2>

<p>Dans cet exemple nous allons vous aider à finaliser une application de calendrier simple. Dans le code, vous avez :</p>

<ul>
 <li>Un élément {{htmlelement("select")}} permettant à l'utilisateur de choisir un mois.</li>
 <li>Un pilote d'événement <code>onchange</code> pour détecter si la valeur choisie dans le menu <code>&lt;select&gt;</code> a été modifiée.</li>
 <li>Une fonction <code>createCalendar()</code> qui trace le calendrier et affiche le mois voulu dans l'élément {{htmlelement("h1")}}.</li>
</ul>

<p>Vous aurez besoin d'écrire une instruction conditionnelle dans la fonction <code>onchange</code>, juste au dessous du commentaire <code>// AJOUTER LA CONDITION ICI</code>. Elle doit :</p>

<ol>
 <li>Noter le mois choisi (enregistré dans la variable <code>choice</code>. Ce doit être la valeur de l'élément <code>&lt;select&gt;</code> après un changement, "Janvier" par exemple).</li>
 <li>Faire en sorte que la variable nommée <code>days</code> soit égale au nombre de jours du mois sélectionné. Pour ce faire, examinez le nombre de jours dans chaque mois de l'année. Vous pouvez ignorer les années bissextiles pour les besoins de cet exemple.</li>
</ol>

<p>Conseils :</p>

<ul>
 <li>Utilisez un OR logique pour grouper plusieurs mois ensemble dans une même condition, beaucoup d'entre eux ont le même nombre de jours.</li>
 <li>Voyez quel est le nombre de jours le plus courant et utilisez le comme valeur par défaut.</li>
</ul>

<p>Si vous faites une erreur, vous pouvez toujours réinitialiser l'exemple avec le bouton "Réinitialiser". Si vous êtes vraiment bloqué, pressez "Voir la solution".</p>

<pre class="brush: html hidden">&lt;div class="output" style="height: 500px;overflow: auto;"&gt;
  &lt;label for="month"&gt;Choisissez un mois : &lt;/label&gt;
  &lt;select id="month"&gt;
    &lt;option value="Janvier"&gt;Janvier&lt;/option&gt;
    &lt;option value="Février"&gt;Février&lt;/option&gt;
    &lt;option value="Mars"&gt;Mars&lt;/option&gt;
    &lt;option value="Avril"&gt;Avril&lt;/option&gt;
    &lt;option value="Mai"&gt;Mai&lt;/option&gt;
    &lt;option value="Juin"&gt;Juin&lt;/option&gt;
    &lt;option value="Juillet"&gt;Juillet&lt;/option&gt;
    &lt;option value="Août"&gt;Août&lt;/option&gt;
    &lt;option value="Septembre"&gt;Septembre&lt;/option&gt;
    &lt;option value="Octobre"&gt;Octobre&lt;/option&gt;
    &lt;option value="Novembre"&gt;Novembre&lt;/option&gt;
    &lt;option value="Decembre"&gt;Décembre&lt;/option&gt;
  &lt;/select&gt;

  &lt;h1&gt;&lt;/h1&gt;

  &lt;ul&gt;&lt;/ul&gt;
&lt;/div&gt;

&lt;hr&gt;

&lt;textarea id="code" class="playable-code" style="height: 500px;"&gt;
var select = document.querySelector('select');
var list = document.querySelector('ul');
var h1 = document.querySelector('h1');

select.onchange = function() {
  var choice = select.value;

  // AJOUTER LA CONDITION ICI

  createCalendar(days, choice);
}

function createCalendar(days, choice) {
  list.innerHTML = '';
  h1.textContent = choice;
  for (var i = 1; i &lt;= days; i++) {
    const listItem = document.createElement('li');
    listItem.textContent = i;
    list.appendChild(listItem);
  }
}

createCalendar(31,'Janvier');
&lt;/textarea&gt;

&lt;div class="playable-buttons"&gt;
  &lt;input id="reset" type="button" value="Réinitialiser"&gt;
  &lt;input id="solution" type="button" value="Voir la solution"&gt;
&lt;/div&gt;
</pre>

<pre class="brush: css hidden">.output * {
  box-sizing: border-box;
}

.output ul {
  padding-left: 0;
}

.output li {
  display: block;
  float: left;
  width: 25%;
  border: 2px solid white;
  padding: 5px;
  height: 40px;
  background-color: #4A2DB6;
  color: white;
}
</pre>

<pre class="brush: js hidden">const textarea = document.getElementById('code');
const reset = document.getElementById('reset');
const solution = document.getElementById('solution');
let code = textarea.value;

function updateCode() {
  eval(textarea.value);
}

reset.addEventListener('click', function() {
  textarea.value = code;
  updateCode();
});

solution.addEventListener('click', function() {
  textarea.value = jsSolution;
  updateCode();
});

var jsSolution = 'var select = document.querySelector(\'select\');\nvar list = document.querySelector(\'ul\');\nvar h1 = document.querySelector(\'h1\');\n\nselect.onchange = function() {\n  var choice = select.value;\n  var days = 31;\n  if(choice === \'February\') {\n    days = 28;\n  } else if(choice === \'April\' || choice === \'June\' || choice === \'September\'|| choice === \'November\') {\n    days = 30;\n  }\n\n  createCalendar(days, choice);\n}\n\nfunction createCalendar(days, choice) {\n  list.innerHTML = \'\';\n  h1.textContent = choice;\n for(var i = 1; i &lt;= days; i++) {\n    var listItem = document.createElement(\'li\');\n    listItem.textContent = i;\n    list.appendChild(listItem);\n  }\n }\n\ncreateCalendar(31,\'January\');';

textarea.addEventListener('input', updateCode);
window.addEventListener('load', updateCode);
</pre>

<p>{{ EmbedLiveSample('Apprentissage_actif_un_calendrier_simple', '100%', 1110, "", "", "hide-codepen-jsfiddle") }}</p>

<h2 id="Activité_plus_de_choix_de_couleurs">Activité : plus de choix de couleurs</h2>

<p>Nous allons reprendre l'exemple de l'opérateur ternaire vu plus haut et transformer cet opérateur ternaire en une directive <code>switch</code>  qui nous permettra une plus grande variété de choix pour le site web tout simple. Voyez l'élément {{htmlelement("select")}} — cette fois, il n'y a pas deux options de thème, mais cinq. Il vous faut ajouter une directive <code>switch</code> au dessous du commentaire  <code>// AJOUT D'UNE DIRECTIVE SWITCH</code> :</p>

<ul>
 <li>Elle doit accepter la variable <code>choice</code> comme expression d'entrée.</li>
 <li>Pour chaque cas, le choix doit être égal à une des valeurs possibles pouvant être choisies, c'est-à-dire blanc, noir, mauve, jaune ou psychédélique.</li>
 <li>Chaque cas exécutera la fonction <code>update()</code> à laquelle deux valeurs de couleurs seront passées, la première pour le fond, la seconde pour le texte. Souvenez vous que les valeurs de couleurs sont des chaînes ; elle doivent donc être mises entre guillemets.</li>
</ul>

<p>Si vous faites une erreur, vous pouvez toujours réinitialiser l'exemple avec le bouton « Réinitialiser ». Si vous êtes vraiment bloqué, pressez « Voir la solution ».</p>

<pre class="brush: html hidden">&lt;div class="output" style="height: 300px;"&gt;
  &lt;label for="theme"&gt;Choisissez un thème : &lt;/label&gt;
  &lt;select id="theme"&gt;
    &lt;option value="white"&gt;Blanc&lt;/option&gt;
    &lt;option value="black"&gt;Noir&lt;/option&gt;
    &lt;option value="purple"&gt;Mauve&lt;/option&gt;
    &lt;option value="yellow"&gt;Jaune&lt;/option&gt;
    &lt;option value="psychedelic"&gt;Psychédélique&lt;/option&gt;
  &lt;/select&gt;

  &lt;h1&gt;Voici mon site Web&lt;/h1&gt;
&lt;/div&gt;

&lt;hr&gt;

&lt;textarea id="code" class="playable-code" style="height: 450px;"&gt;
const select = document.querySelector('select');
const html = document.querySelector('.output');

select.onchange = function() {
  let choice = select.value;

  // AJOUT D'UNE DIRECTIVE SWITCH
}

function update(bgColor, textColor) {
  html.style.backgroundColor = bgColor;
  html.style.color = textColor;
}&lt;/textarea&gt;

&lt;div class="playable-buttons"&gt;
  &lt;input id="reset" type="button" value="Réinitialiser"&gt;
  &lt;input id="solution" type="button" value="Voir la solution"&gt;
&lt;/div&gt;
</pre>

<pre class="brush: js hidden">const textarea = document.getElementById('code');
const reset = document.getElementById('reset');
const solution = document.getElementById('solution');
let code = textarea.value;

function updateCode() {
  eval(textarea.value);
}

reset.addEventListener('click', function() {
  textarea.value = code;
  updateCode();
});

solution.addEventListener('click', function() {
  textarea.value = jsSolution;
  updateCode();
});

const jsSolution = 'const select = document.querySelector(\'select\');\nlet html = document.querySelector(\'.output\');\n\nselect.onchange = function() {\n  let choice = select.value;\n\n  switch(choice) {\n    case \'black\':\n      update(\'black\',\'white\');\n      break;\n    case \'white\':\n      update(\'white\',\'black\');\n      break;\n    case \'purple\':\n      update(\'purple\',\'white\');\n      break;\n    case \'yellow\':\n      update(\'yellow\',\'darkgray\');\n      break;\n    case \'psychedelic\':\n      update(\'lime\',\'purple\');\n      break;\n  }\n}\n\nfunction update(bgColor, textColor) {\n  html.style.backgroundColor = bgColor;\n  html.style.color = textColor;\n}';

textarea.addEventListener('input', updateCode);
window.addEventListener('load', updateCode);
</pre>

<p>{{ EmbedLiveSample('Activité_plus_de_choix_de_couleurs', '100%', 850) }}</p>

<h2 id="Conclusion">Conclusion</h2>

<p>C'est tout ce qu'il est nécessaire de connaître à propos des structures conditionnelles en JavaScript pour le moment ! Je pense que vous avez assurément compris ces concepts et travaillé les exemples aisément ; s'il y a quelque chose que vous n'avez pas compris, relisez cet article à nouveau, ou bien <a href="/fr/Apprendre#Nous_contacter">contactez‑nous</a> pour une aide.</p>

<h2 id="Voir_aussi">Voir aussi</h2>

<ul>
 <li><a href="/fr/docs/Learn/JavaScript/First_steps/Math#Opérateurs_de_comparaison">Opérateurs de comparaison</a></li>
 <li><a href="/fr/docs/Web/JavaScript/Guide/Contrôle_du_flux_Gestion_des_erreurs#Les_instructions_conditionnelles">Les instructions conditionnelles</a></li>
 <li><a href="/fr/docs/Web/JavaScript/Reference/Instructions/if...else">Référence if...else</a></li>
 <li><a href="/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/L_op%C3%A9rateur_conditionnel">Référence opérateur conditionnel (ternaire)</a></li>
</ul>

<p>{{NextMenu("Apprendre/JavaScript/Building_blocks/Looping_code", "Apprendre/JavaScript/Building_blocks")}}</p>

<h2 id="Dans_ce_module">Dans ce module</h2>

<ul>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/conditionals">Prendre des décisions dans du code — conditions</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Looping_code">Les boucles dans le code</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Fonctions">Fonctions — blocs de code réutilisables</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Build_your_own_function">Construire vos propres fonctions</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Return_values">Valeurs de retour des fonctions</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Ev%C3%A8nements">Introduction aux événements</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Building_blocks/Image_gallery">Gallerie d'images</a></li>
</ul>