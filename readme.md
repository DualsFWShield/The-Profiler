## 🇬🇧 English Documentation

### **Project: The Profiler**

### 1. Project Overview

**The Profiler** is a standalone, client-side web application designed for educational exploration of personality frameworks and behavioral indicators. It allows users to answer a series of modular questionnaires and instantly receive a generated profile report.

The core principles of this project are:
*   **Privacy First**: All data processing happens locally in the user's browser. No information is ever sent to or stored on a server.
*   **Educational Tool**: It is designed to provide insights based on established psychological models but is explicitly **not a diagnostic tool**. It should not be used as a substitute for professional medical or psychological advice.
*   **Zero Dependencies**: The application runs from a single HTML file with no need for a web server, build process, or external installations (besides the browser).

**Technologies Used:**
*   HTML5
*   CSS3 (embedded)
*   JavaScript (ES6, embedded)
*   jsPDF & jsPDF-AutoTable (via CDN) for PDF generation.

---

### 2. Features

*   **Modular Questionnaires**: The tool is organized into modules (e.g., "Base Personality Profile", "Behavioral Disorders (Adult)"). Users can enable or disable modules to customize their assessment.
*   **Diverse Psychological Models**:
    *   **Personality**: MBTI, Enneagram.
    *   **Behavioral Traits**: Dark Triad (Machiavellianism, Narcissism, Psychopathy).
    *   **Attachment Style**: Secure, Anxious, Avoidant, Fearful-Avoidant.
    *   **Screening Indicators**: Questionnaires inspired by criteria for ADHD, Oppositional Defiant Disorder (ODD), Conduct Disorder, BPD, Autism Spectrum, and more.
*   **Dynamic Report Generation**: An instant, detailed report is generated in the sidebar upon analysis, summarizing the key findings.
*   **Data Portability**:
    *   **PDF Export**: Generate and download a clean, formatted PDF of the report.
    *   **JSON Export/Import**: Export the raw results as a `.json` file for archival or sharing. Previously exported JSON files can be imported to view the report again.
*   **"Fill Example" Feature**: A button to automatically fill out all questionnaires with sample data to demonstrate the application's full reporting capabilities.
*   **Multi-language Support**: The interface includes a language switcher to navigate between different versions of the application (e.g., French, English, Dutch).

---

### 3. How to Use (User Guide)

1.  **Open the File**: Simply open the `.html` file in any modern web browser like Chrome, Firefox, or Edge.
2.  **Select Modules**: In the top-left card, check the boxes for the sets of questionnaires you wish to complete. The corresponding sections will appear below.
3.  **Answer the Questions**: Fill out the forms. Questions use various input types, including radio buttons (select one), checkboxes (select multiple), and range sliders (drag to select a value).
4.  **Generate Profile**: Click the **"Analyze (generate profile)"** button.
5.  **View the Report**: The detailed report will immediately appear in the **"Detailed Report"** panel on the right. The raw JSON data used for the report will appear in the **"JSON (export)"** panel below it.
6.  **Export Your Data**:
    *   Click **"Export to PDF"** to save the report as a PDF document.
    *   Click **"Export JSON"** to save the raw results data.
7.  **Import Data**: Click the **"Choose File"** button under "Import JSON" and select a `.json` file that was previously exported from this tool. The report and JSON views will be populated with the data from the file.
8.  **Other Actions**:
    *   Click **"Example"** to see how the tool works with a complete, pre-filled form.
    *   Click **"Reset"** to clear all your answers and the report panels.

---

### 4. Technical Breakdown

The entire application is self-contained within a single HTML file.

#### JavaScript Structure

The core logic is located inside the `<script>` tag at the end of the `<body>`.

1.  **Data Definitions (`MODULES` and `SECTIONS_DATA`)**
    *   This is the "database" of the application.
    *   `MODULES`: An object that defines the main categories of questionnaires. Each module has a title, an enabled/disabled state, and a list of section keys it contains.
    *   `SECTIONS_DATA`: A large object where each key represents a specific questionnaire (e.g., `mbti`, `top`, `autism`). Each section contains its title, description, prevalence data, and an array of `items` (the questions).

2.  **UI Building (`build()` and related functions)**
    *   The `build()` function is called on page load.
    *   It dynamically creates the HTML for the module checkboxes and then iterates through the enabled modules to build the HTML for each questionnaire.
    *   Specific functions like `buildMbti()` or `buildScaleQuestions()` handle the generation of different question formats. This data-driven approach makes the application easy to extend.

3.  **Analysis Logic (`analyzeAllEnabledSections()` and specific analyzers)**
    *   When the user clicks "Analyze", the `runAll()` function calls `analyzeAllEnabledSections()`.
    *   This function iterates through the enabled sections and calls the appropriate analysis function for each one.
    *   For standard scale-based questionnaires, the generic `analyzeSection()` calculates a total score and a percentage.
    *   For complex questionnaires, specific functions are used (e.g., `analyzeMBTI()` calculates the 4-letter type, `analyzeDark()` calculates scores for three separate traits).

4.  **Reporting & Exporting (`generateReport()`, `generatePDF()`)**
    *   `generateReport()`: Takes the unified `results` object from the analysis and formats it into user-friendly HTML for display in the report panel.
    *   `generatePDF()`: Uses the jsPDF library to construct a multi-page PDF document with titles, text sections, and tables based on the analysis results.

---

### 5. How to Extend or Modify

The application was designed to be easily extensible.

#### To Add a New Scale-Based Questionnaire:

1.  **Define the Data**: In the `SECTIONS_DATA` object, add a new key for your questionnaire. Provide a `title`, `description`, `prevalence`, the `scaleText` (e.g., `FREQUENCY_SCALE_TEXT`), and an `items` array with your questions.
    ```javascript
    // Example inside SECTIONS_DATA
    myNewQuiz: {
        title: 'My New Quiz (Screening)',
        description: "A brief description of what this quiz measures.",
        prevalence: "Affects about X% of the population.",
        scaleText: FREQUENCY_SCALE_TEXT, // Use the existing 0-4 scale
        items: [
            { id: 'mq1', text: "This is the first question." },
            { id: 'mq2', text: "This is the second question." }
        ]
    },
    ```
2.  **Add to a Module**: In the `MODULES` object, add your new key (`'myNewQuiz'`) to the `sections` array of an existing module, or create a new module for it.

That's it! The generic `buildScaleQuestions` and `analyzeSection` functions will automatically handle the UI generation, analysis, and reporting for your new quiz.

#### To Add a New Complex Questionnaire:

If your questionnaire requires unique logic (like MBTI's A/B choices), you will need to:
1.  Define the data in `SECTIONS_DATA` with a structure that fits your needs.
2.  Create a custom `buildMyNewQuiz()` function to generate the HTML for it.
3.  Create a custom `analyzeMyNewQuiz()` function to process the user's input and return a result object.
4.  Call these new functions from within `buildAllSections()` and `analyzeAllEnabledSections()` using a conditional check (e.g., `else if (sectionKey === 'myNewQuiz')`).

***

## 🇫🇷 Documentation Française

### **Projet : The Profiler**

### 1. Présentation du Projet

**The Profiler** est une application web autonome et côté client, conçue pour l'exploration éducative des cadres de personnalité et des indicateurs comportementaux. Elle permet aux utilisateurs de répondre à une série de questionnaires modulaires et de recevoir instantanément un rapport de profil généré.

Les principes fondamentaux de ce projet sont :
*   **Confidentialité d'abord**: Tout le traitement des données se fait localement dans le navigateur de l'utilisateur. Aucune information n'est jamais envoyée ou stockée sur un serveur.
*   **Outil Éducatif**: Il est conçu pour fournir des aperçus basés sur des modèles psychologiques établis, mais n'est explicitement **pas un outil de diagnostic**. Il ne doit pas être utilisé en remplacement d'un avis médical ou psychologique professionnel.
*   **Zéro Dépendance**: L'application fonctionne à partir d'un unique fichier HTML sans nécessiter de serveur web, de processus de compilation ou d'installations externes (hormis le navigateur).

**Technologies Utilisées :**
*   HTML5
*   CSS3 (intégré)
*   JavaScript (ES6, intégré)
*   jsPDF & jsPDF-AutoTable (via CDN) pour la génération de PDF.

---

### 2. Fonctionnalités

*   **Questionnaires Modulaires**: L'outil est organisé en modules (ex: "Profil de Personnalité", "Troubles du Comportement (Adulte)"). Les utilisateurs peuvent activer ou désactiver des modules pour personnaliser leur évaluation.
*   **Modèles Psychologiques Variés**:
    *   **Personnalité**: MBTI, Ennéagramme.
    *   **Traits Comportementaux**: Triade Noire (Machiavélisme, Narcissisme, Psychopathie).
    *   **Style d'Attachement**: Sécure, Anxieux, Évitant, Craintif-évitant.
    *   **Indicateurs de Dépistage**: Questionnaires inspirés des critères pour le TDA/H, le Trouble Oppositionnel avec Provocation (TOP), le Trouble des Conduites, la personnalité borderline, le spectre de l'autisme, et plus encore.
*   **Génération de Rapport Dynamique**: Un rapport détaillé et instantané est généré dans la barre latérale après l'analyse, résumant les principaux résultats.
*   **Portabilité des Données**:
    *   **Export PDF**: Générez et téléchargez une version PDF claire et formatée du rapport.
    *   **Export/Import JSON**: Exportez les résultats bruts sous forme de fichier `.json` pour archivage ou partage. Les fichiers JSON précédemment exportés peuvent être importés pour afficher à nouveau le rapport.
*   **Fonction "Exemple"**: Un bouton pour remplir automatiquement tous les questionnaires avec des données fictives afin de démontrer toutes les capacités de reporting de l'application.
*   **Support Multilingue**: L'interface inclut un sélecteur de langue pour naviguer entre différentes versions de l'application (ex: Français, Anglais, Néerlandais).

---

### 3. Comment Utiliser (Guide Utilisateur)

1.  **Ouvrir le Fichier**: Ouvrez simplement le fichier `.html` dans n'importe quel navigateur web moderne comme Chrome, Firefox ou Edge.
2.  **Sélectionner les Modules**: Dans la première carte en haut à gauche, cochez les cases des ensembles de questionnaires que vous souhaitez remplir. Les sections correspondantes apparaîtront en dessous.
3.  **Répondre aux Questions**: Remplissez les formulaires. Les questions utilisent divers types de champs : boutons radio (un seul choix), cases à cocher (choix multiples) et curseurs (glisser pour sélectionner une valeur).
4.  **Générer le Profil**: Cliquez sur le bouton **"Analyser (générer profil)"**.
5.  **Consulter le Rapport**: Le rapport détaillé apparaîtra immédiatement dans le panneau **"Rapport Détaillé"** à droite. Les données JSON brutes utilisées pour le rapport apparaîtront dans le panneau **"JSON (export)"** juste en dessous.
6.  **Exporter Vos Données**:
    *   Cliquez sur **"Exporter en PDF"** pour enregistrer le rapport en tant que document PDF.
    *   Cliquez sur **"Exporter JSON"** pour sauvegarder les données brutes des résultats.
7.  **Importer des Données**: Cliquez sur le bouton **"Choisir un fichier"** sous "Exporter JSON" et sélectionnez un fichier `.json` précédemment exporté depuis cet outil. Les vues du rapport et du JSON seront alors remplies avec les données du fichier.
8.  **Autres Actions**:
    *   Cliquez sur **"Exemple"** pour voir comment l'outil fonctionne avec un formulaire complet et pré-rempli.
    *   Cliquez sur **"Réinitialiser"** pour effacer toutes vos réponses et les panneaux de résultats.

---

### 4. Architecture Technique

L'application entière est contenue dans un seul fichier HTML.

#### Structure JavaScript

La logique principale est située dans la balise `<script>` à la fin du `<body>`.

1.  **Définitions des Données (`MODULES` et `SECTIONS_DATA`)**
    *   C'est la "base de données" de l'application.
    *   `MODULES`: Un objet qui définit les grandes catégories de questionnaires. Chaque module a un titre, un état activé/désactivé, et une liste des clés de section qu'il contient.
    *   `SECTIONS_DATA`: Un grand objet où chaque clé représente un questionnaire spécifique (ex: `mbti`, `top`, `autism`). Chaque section contient son titre, sa description, des données de prévalence, et un tableau d' `items` (les questions).

2.  **Construction de l'Interface (`build()` et fonctions associées)**
    *   La fonction `build()` est appelée au chargement de la page.
    *   Elle crée dynamiquement le HTML pour les cases à cocher des modules, puis parcourt les modules activés pour construire le HTML de chaque questionnaire.
    *   Des fonctions spécifiques comme `buildMbti()` ou `buildScaleQuestions()` gèrent la génération des différents formats de questions. Cette approche basée sur les données rend l'application facile à étendre.

3.  **Logique d'Analyse (`analyzeAllEnabledSections()` et analyseurs spécifiques)**
    *   Lorsque l'utilisateur clique sur "Analyser", la fonction `runAll()` appelle `analyzeAllEnabledSections()`.
    *   Cette fonction parcourt les sections activées et appelle la fonction d'analyse appropriée pour chacune.
    *   Pour les questionnaires standards basés sur une échelle, la fonction générique `analyzeSection()` calcule un score total et un pourcentage.
    *   Pour les questionnaires complexes, des fonctions spécifiques sont utilisées (ex: `analyzeMBTI()` calcule le type à 4 lettres, `analyzeDark()` calcule les scores pour trois traits distincts).

4.  **Rapport et Export (`generateReport()`, `generatePDF()`)**
    *   `generateReport()`: Prend l'objet `results` unifié de l'analyse et le formate en HTML lisible pour l'affichage dans le panneau de rapport.
    *   `generatePDF()`: Utilise la bibliothèque jsPDF pour construire un document PDF de plusieurs pages avec des titres, des sections de texte et des tableaux basés sur les résultats de l'analyse.

---

### 5. Comment Étendre ou Modifier

L'application a été conçue pour être facilement extensible.

#### Pour Ajouter un Nouveau Questionnaire Basé sur une Échelle :

1.  **Définir les Données**: Dans l'objet `SECTIONS_DATA`, ajoutez une nouvelle clé pour votre questionnaire. Fournissez un `title`, une `description`, une `prevalence`, le `scaleText` (ex: `FREQUENCY_SCALE_TEXT`), et un tableau `items` avec vos questions.
    ```javascript
    // Exemple à l'intérieur de SECTIONS_DATA
    monNouveauQuiz: {
        title: 'Mon Nouveau Quiz (Dépistage)',
        description: "Une brève description de ce que ce quiz mesure.",
        prevalence: "Affecte environ X% de la population.",
        scaleText: FREQUENCY_SCALE_TEXT, // Utilise l'échelle 0-4 existante
        items: [
            { id: 'mq1', text: "Ceci est la première question." },
            { id: 'mq2', text: "Ceci est la seconde question." }
        ]
    },
    ```
2.  **Ajouter à un Module**: Dans l'objet `MODULES`, ajoutez votre nouvelle clé (`'monNouveauQuiz'`) au tableau `sections` d'un module existant, ou créez un nouveau module pour celui-ci.

C'est tout ! Les fonctions génériques `buildScaleQuestions` et `analyzeSection` géreront automatiquement la génération de l'interface, l'analyse et le rapport pour votre nouveau quiz.

#### Pour Ajouter un Nouveau Questionnaire Complexe :

Si votre questionnaire nécessite une logique unique (comme les choix A/B du MBTI), vous devrez :
1.  Définir les données dans `SECTIONS_DATA` avec une structure adaptée à vos besoins.
2.  Créer une fonction personnalisée `buildMonNouveauQuiz()` pour générer le HTML correspondant.
3.  Créer une fonction personnalisée `analyzeMonNouveauQuiz()` pour traiter les réponses de l'utilisateur et retourner un objet de résultat.
4.  Appeler ces nouvelles fonctions depuis `buildAllSections()` et `analyzeAllEnabledSections()` en utilisant une vérification conditionnelle (ex: `else if (sectionKey === 'monNouveauQuiz')`).