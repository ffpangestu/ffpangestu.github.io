---
layout: about
title: about
permalink: /
subtitle: Industrie 4.0, Robotik und KI

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>Mechatronik Master</p>
    <p>Hochschule Darmstadt</p>

selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page

announcements:
  enabled: false # includes a list of news items
  scrollable: false # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder
---

<!-- Language Toggle -->
<a href="#" class="lang-toggle" data-lang="de" onclick="event.preventDefault(); showLang('de')" style="
  color: #007bff;
  text-decoration: none;
  margin-right: 1em;
  cursor: pointer;
  transition: 0.2s;
" onmouseover="this.style.textDecoration='underline'" onmouseout="this.style.textDecoration='none'">
  Deutsch
</a>

<a href="#" class="lang-toggle" data-lang="en" onclick="event.preventDefault(); showLang('en')" style="
  color: #007bff;
  text-decoration: none;
  cursor: pointer;
  transition: 0.2s;
" onmouseover="this.style.textDecoration='underline'" onmouseout="this.style.textDecoration='none'">
  English
</a>

<!-- German Section -->
<div id="lang-de" style="text-align: justify;">
  <p>Schon seit meiner Schulzeit motiviert mich mein Interesse, Programmierung zu lernen und an nationalen Wettbewerben teilzunehmen. Ich habe mich dazu entschieden, mich im industriellen Bereich weiter zu spezialisieren. Dafür bin ich direkt ins Epizentrum von Industrie 4.0 gezogen.</p>

  <p>Nach Abschluss meines Sprachkurses ging ich 2018 nach Deutschland, schrieb mich am Studienkolleg ein und entschied mich letztendlich, mein Studium der <strong>Mechatronik</strong> an der <strong>Hochschule Kaiserslautern</strong> fortzusetzen. Dort hatte ich die Möglichkeit, von Professorinnen und Professoren sowie Expertinnen und Experten auf diesem Fachgebiet zu lernen und gleichzeitig meine Sprachkenntnisse zu verbessern. Schließlich schrieb ich meine Bachelorarbeit und hielt mein Colloquium auf Deutsch über die Entwicklung, Echtzeitsimulation und Implementierung mobiler Roboter am <strong>Fraunhofer ITWM</strong>.</p>

  <p>Als eine der Voraussetzungen für das Masterstudium habe ich meine Englischkenntnisse verbessert und gleichzeitig in meiner Heimatstadt das handwerkliche Grundlagenwissen in den Bereichen Elektrotechnik und Mechanik erworben. Nun bin ich nach Deutschland zurückgekehrt, um meine Passion für die Schwerpunkte Industrie 4.0, Robotik und KI an der <strong>Hochschule Darmstadt</strong> weiterzuverfolgen.</p>
</div>

<!-- English Section -->
<div id="lang-en" style="display:none; text-align: justify;">
  <p>Since I was in high school, my interest motivated me to learn programming and compete in national level. I followed my dream to further my specialization in industrial field straight to the epicenter of Industry 4.0, Germany.</p>

  <p>I went to Germany in 2018 after I finished Sprachkurs and enrolled to Studienkolleg before I decided to continue as <strong>Mechatronics</strong> student at <strong>Hochschule Kaiserslautern</strong>. I had opportunities to learn from professors and experts in the field while at the same time improving my language skill. In the end, I did my bachelor thesis and its kolloquium in german about the designing, real-time simulation, and implementation of mobile robot at <strong>Fraunhofer ITWM</strong>.</p>

  <p>As one of the prerequisite master program, I polished my english while learning electrical and mechanical tradecraft at my hometown. I went back to Germany to continue my passion with specialization in Industry 4.0, Robotics, and AI at <strong>Hochschule Darmstadt</strong>.</p>
</div>

<script>
function showLang(lang) {
  document.getElementById('lang-de').style.display = lang === 'de' ? 'block' : 'none';
  document.getElementById('lang-en').style.display = lang === 'en' ? 'block' : 'none';
  
  document.querySelectorAll('a.lang-toggle').forEach(a => {
    a.style.fontWeight = (a.dataset.lang === lang) ? 'bold' : 'normal';
  });
}
</script>





