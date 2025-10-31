# Referat
1. Edition
!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interaktiver Report: Allocation im Elektronikmarkt</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Chosen Palette: Warm Neutral & Muted Blue -->
    <!-- Application Structure Plan: The SPA uses a top navigation bar (Übersicht, Das Problem, Unser Unternehmen, Ausblick) to switch between thematic content sections, controlled by JS. This non-linear, task-oriented structure is more user-friendly than a linear presentation. 'Das Problem' groups all external factors (Definitions, Causes, Mechanisms) for context. 'Unser Unternehmen' groups all internal relevance (Impacts, Strategies), allowing users to quickly find company-specific information. This design prioritizes exploration and understanding over a fixed narrative. -->
    <!-- Visualization & Content Choices:
    1.  Supply Chain (Slide 3) -> Goal: Organize/Inform -> Viz: Simple HTML/Tailwind flowchart -> Interaction: None (static visual) -> Justification: Clear visualization of complexity without SVG/Mermaid. (HTML/CSS)
    2.  Allocation Mechanism (Slide 5) -> Goal: Organize/Inform -> Viz: HTML/Tailwind Funnel/Trichter Diagram -> Interaction: None (static visual) -> Justification: Visually represents the 'Trichter' concept from the report. (HTML/CSS)
    3.  Kostensteigerung (Slide 7) -> Goal: Inform/Compare -> Viz: Vertical Bar Chart -> Interaction: Tooltips on hover -> Justification: Clearly shows the dramatic price difference between normal and spot market prices, making the "100%-1000%" text tangible. (Chart.js/Canvas)
    4.  Strategies (Slide 8) -> Goal: Organize/Inform -> Viz: Interactive Accordion/Toggle List -> Interaction: Click to expand/collapse strategy details -> Justification: Organizes dense text into a clean, interactive list, allowing users to explore only the strategies they are interested in. (HTML/JS)
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 320px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
        .nav-link {
            @apply px-3 py-2 rounded-md text-sm font-medium text-neutral-700 hover:bg-neutral-200 transition-colors;
        }
        .nav-link.active {
            @apply bg-sky-700 text-white hover:bg-sky-800;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .info-card {
            @apply bg-white p-6 rounded-lg shadow-md border border-neutral-200 transition-shadow hover:shadow-lg;
        }
        .strategy-item header {
            @apply flex justify-between items-center p-4 bg-neutral-100 rounded-lg cursor-pointer hover:bg-neutral-200;
        }
        .strategy-item .content {
            @apply p-4 bg-white rounded-b-lg border border-t-0 border-neutral-200;
        }
    </style>
</head>
<body class="bg-neutral-50 text-neutral-900">

    <nav class="bg-white shadow-sm sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex-shrink-0 flex items-center">
                    <span class="text-xl font-bold text-sky-700">Pantel-Elektronik</span>
                    <span class="ml-2 text-lg font-light text-neutral-600">| Allocation Report</span>
                </div>
                <div class="hidden sm:ml-6 sm:flex sm:space-x-4">
                    <a href="#overview" class="nav-link active" data-target="overview">Übersicht</a>
                    <a href="#problem" class="nav-link" data-target="problem">Das Problem</a>
                    <a href="#company" class="nav-link" data-target="company">Unser Unternehmen</a>
                    <a href="#outlook" class="nav-link" data-target="outlook">Ausblick</a>
                </div>
                <div class="sm:hidden">
                    <select id="mobile-nav" class="block w-full rounded-md border-neutral-300 shadow-sm focus:border-sky-500 focus:ring-sky-500">
                        <option value="overview">Übersicht</option>
                        <option value="problem">Das Problem</option>
                        <option value="company">Unser Unternehmen</option>
                        <option value="outlook">Ausblick</option>
                    </select>
                </div>
            </div>
        </div>
    </nav>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">

        <main id="overview" class="content-section active">
            <header class="mb-8">
                <h1 class="text-4xl font-bold text-sky-800 mb-2">Allocation im Globalen Elektronikmarkt</h1>
                <p class="text-xl text-neutral-700">Wie globale Verknappung Pantel-Elektronik herausfordert und welche Strategien wir verfolgen.</p>
            </header>
            
            <section class="mb-12">
                <p class="text-lg text-neutral-800 mb-6">
                    Willkommen zu diesem interaktiven Report. Das Thema "Allocation" ist mehr als nur ein Lieferengpass; es ist eine fundamentale Verknappung, die unsere gesamte Branche betrifft. Diese Anwendung soll Ihnen einen klaren Überblick über die Ursachen des Problems, die direkten Auswirkungen auf unser Unternehmen und die von uns ergriffenen Gegenmaßnahmen geben. Nutzen Sie die Navigation, um die für Sie relevantesten Themen zu erkunden.
                </p>
            </section>

            <section class="grid md:grid-cols-2 gap-6">
                <div class="info-card bg-sky-50 border-sky-200">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-3">Was ist Allocation?</h2>
                    <p class="mb-4">Allocation (Kontingentierung) tritt auf, wenn die weltweite Nachfrage nach Bauteilen die Produktionskapazitäten massiv übersteigt. Hersteller können nicht mehr alle Aufträge bedienen und beginnen, die knappen Güter zuzuteilen.</p>
                    <a href="#problem" class="font-medium text-sky-700 hover:underline" data-target-link="problem">Mehr zum globalen Problem ➔</a>
                </div>
                <div class="info-card bg-amber-50 border-amber-200">
                    <h2 class="text-2xl font-semibold text-amber-900 mb-3">Auswirkungen auf Pantel</h2>
                    <p class="mb-4">Für uns bedeutet dies konkret: massive Kostensteigerungen am Spotmarkt, unzuverlässige Liefertermine und das Risiko von Produktionsstillständen. Unsere Planungssicherheit ist stark gefährdet.</p>
                    <a href="#company" class="font-medium text-amber-700 hover:underline" data-target-link="company">Unsere Auswirkungen & Strategien ➔</a>
                </div>
            </section>
        </main>

        <main id="problem" class="content-section">
            <header class="mb-8">
                <h1 class="text-4xl font-bold text-sky-800 mb-2">Das Globale Problem</h1>
                <p class="text-xl text-neutral-700">Definition, Ursachen und Mechanismen der Verknappung.</p>
            </header>

            <section class="mb-12">
                <p class="text-lg text-neutral-800 mb-6">
                    Um unsere Situation bei Pantel-Elektronik zu verstehen, müssen wir zunächst das globale Phänomen "Allocation" betrachten. Es ist ein komplexes Zusammenspiel aus Marktcharakteristiken, unvorhergesehenen Ereignissen und den Mechanismen der Verteilung. Dieser Abschnitt schlüsselt auf, warum der Elektronikmarkt so fragil ist und wie die Verknappung verwaltet wird.
                </p>
            </section>

            <div class="space-y-12">
                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-4">Definition: Allocation vs. Lieferengpass</h2>
                    <div class="grid md:grid-cols-2 gap-6">
                        <div>
                            <h3 class="font-semibold text-lg text-neutral-800">Lieferengpass (Standard)</h3>
                            <p class="text-neutral-700">Ein Lieferengpass betrifft die **Lieferzeit**. Ein Bauteil ist bestellbar, aber die Lieferung verzögert sich.</p>
                            <p class="text-neutral-600 text-sm mt-2">Beispiel: 4 Wochen Lieferzeit statt 2 Wochen.</p>
                        </div>
                        <div class="border-t md:border-t-0 md:border-l border-neutral-200 pt-4 md:pt-0 md:pl-6">
                            <h3 class="font-semibold text-lg text-red-700">Allocation (Kritisch)</h3>
                            <p class="text-neutral-700">Allocation betrifft die **bestellbare Menge**. Wir erhalten nur einen Bruchteil der bestellten Menge, unabhängig vom Preis.</p>
                            <p class="text-red-600 text-sm mt-2">Beispiel: 10.000 Stück bestellt, 1.500 Stück zugeteilt.</p>
                        </div>
                    </div>
                </div>

                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-4">Die fragile Lieferkette des Elektronikmarkts</h2>
                    <p class="text-neutral-700 mb-6">Die Industrie ist von wenigen, hochspezialisierten Herstellern (insb. bei Halbleitern) abhängig. Die Produktion ist global verteilt und lief lange nach dem "Just-in-Time"-Prinzip ohne große Puffer.</p>
                    <div class="flex flex-col md:flex-row md:space-x-4 space-y-2 md:space-y-0 text-center">
                        <div class="flex-1 p-3 bg-neutral-100 rounded-lg">Rohstoffe (z.B. Silizium)</div>
                        <div class="font-bold text-2xl text-sky-600 self-center">➔</div>
                        <div class="flex-1 p-3 bg-neutral-100 rounded-lg">Chip-Design (USA/EU)</div>
                        <div class="font-bold text-2xl text-sky-600 self-center">➔</div>
                        <div class="flex-1 p-3 bg-red-100 rounded-lg border border-red-300">Wafer-Fabrikation (Asien) <span class="block text-sm text-red-700 font-medium">(Flaschenhals)</span></div>
                        <div class="font-bold text-2xl text-sky-600 self-center">➔</div>
                        <div class="flex-1 p-3 bg-neutral-100 rounded-lg">Montage & Test</div>
                        <div class="font-bold text-2xl text-sky-600 self-center">➔</div>
                        <div class="flex-1 p-3 bg-neutral-100 rounded-lg">Endprodukt</div>
                    </div>
                </div>

                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-4">Hauptursachen der Allocation</h2>
                    <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
                        <div class="p-4 bg-neutral-50 rounded-lg border border-neutral-200">
                            <h3 class="font-semibold text-neutral-800">1. Nachfrageschock</h3>
                            <p class="text-sm text-neutral-600">COVID-19 löste einen Boom bei Home-Office, Gaming und E-Mobilität aus, was die Nachfrage explodieren ließ.</p>
                        </div>
                        <div class="p-4 bg-neutral-50 rounded-lg border border-neutral-200">
                            <h3 class="font-semibold text-neutral-800">2. Kapazitätsengpässe</h3>
                            <p class="text-sm text-neutral-600">Der Bau neuer Chipfabriken dauert Jahre und ist extrem teuer. Die Kapazität konnte nicht schnell genug mitwachsen.</p>
                        </div>
                        <div class="p-4 bg-neutral-50 rounded-lg border border-neutral-200">
                            <h3 class="font-semibold text-neutral-800">3. Geopolitische Faktoren</h3>
                            <p class="text-sm text-neutral-600">Handelskonflikte und der Ruf nach "Reshoring" führten zu panischen Bevorratungen (Hortung) bei Großkonzernen.</p>
                        </div>
                        <div class="p-4 bg-neutral-50 rounded-lg border border-neutral-200">
                            <h3 class="font-semibold text-neutral-800">4. Unglücke</h3>
                            <p class="text-sm text-neutral-600">Brände in wichtigen Fabriken oder extreme Wetterereignisse legten kritische Produktionslinien monatelang lahm.</p>
                        </div>
                    </div>
                </div>

                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-4">Mechanismus der Zuteilung: Der "Trichter"</h2>
                    <p class="text-neutral-700 mb-6">Wenn die Nachfrage das Angebot übersteigt, priorisieren die Hersteller ihre Kunden. Dies schafft eine "Zwei-Klassen-Gesellschaft" im Einkauf.</p>
                    <div class="flex flex-col items-center">
                        <div class="w-full md:w-3/4 p-4 text-center bg-neutral-100 rounded-t-lg">
                            <h3 class="font-semibold">Globale Nachfrage (Alle Kunden)</h3>
                        </div>
                        <div class="w-24 h-16 border-l-8 border-r-8 border-neutral-300" style="border-left-color: transparent; border-right-color: transparent; border-image: linear-gradient(to bottom, #d4d4d4, #a3a3a3) 1 100%;"></div>
                        <div class="w-full md:w-3/4 flex justify-between space-x-4">
                            <div class="w-1/2 p-4 text-center bg-sky-100 border border-sky-300 rounded-lg">
                                <h3 class="font-semibold text-sky-800">Priorisierte Zuteilung</h3>
                                <p class="text-sm text-sky-700">(Tier-1-Kunden wie Apple, Samsung, VW)</p>
                            </div>
                            <div class="w-1/2 p-4 text-center bg-amber-100 border border-amber-300 rounded-lg">
                                <h3 class="font-semibold text-amber-800">Restmengen & Spotmarkt</h3>
                                <p class="text-sm text-amber-700">(Kleinere & Mittelständische Kunden)</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>

        <main id="company" class="content-section">
            <header class="mb-8">
                <h1 class="text-4xl font-bold text-amber-800 mb-2">Pantel-Elektronik in der Allocation-Falle</h1>
                <p class="text-xl text-neutral-700">Konkrete Auswirkungen auf unser Unternehmen und unsere strategischen Antworten.</p>
            </header>
            
            <section class="mb-12">
                <p class="text-lg text-neutral-800 mb-6">
                    Als mittelständisches Unternehmen mit Sitz in Erlangen sind wir auf hochspezialisierte Bauteile angewiesen. Wir fallen bei den Herstellern oft nicht in die höchste Prioritätsstufe, was uns vor enorme Herausforderungen stellt. Dieser Abschnitt zeigt die direkten Folgen für unsere Produktion und Finanzen und welche Strategien Einkauf, Technik und Vertrieb gemeinsam erarbeiten, um das Risiko zu managen.
                </p>
            </section>

            <div class="space-y-12">
                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-amber-900 mb-6">Konkrete Folgen der Allocation</h2>
                    <div class="grid md:grid-cols-3 gap-6 mb-8">
                        <div class="p-4 bg-red-50 rounded-lg border border-red-200">
                            <h3 class="font-semibold text-red-800 mb-2">1. Produktion & Planung</h3>
                            <ul class="list-disc list-inside text-sm text-red-700 space-y-1">
                                <li>Verzögerte Fertigung ("Teile-Warte-Stand")</li>
                                <li>Unzuverlässige Liefertermine für Kunden</li>
                                <li>Hoher manueller Planungsaufwand</li>
                            </ul>
                        </div>
                        <div class="p-4 bg-red-50 rounded-lg border border-red-200">
                            <h3 class="font-semibold text-red-800 mb-2">2. Kostensteigerung (Einkauf)</h3>
                             <ul class="list-disc list-inside text-sm text-red-700 space-y-1">
                                <li>Massive Spotmarkt-Preisaufschläge</li>
                                <li>Hohe Kosten für Eiltransporte (Flugfracht)</li>
                                <li>Zusatzkosten für Redesigns</li>
                            </ul>
                        </div>
                        <div class="p-4 bg-red-50 rounded-lg border border-red-200">
                            <h3 class="font-semibold text-red-800 mb-2">3. Lager & Kapitalbindung</h3>
                             <ul class="list-disc list-inside text-sm text-red-700 space-y-1">
                                <li>"Dead Stock" (unvollständige Baugruppen)</li>
                                <li>Hohe Kapitalbindung im Lager</li>
                                <li>Lagerkosten für überbevorratete Teile</li>
                            </ul>
                        </div>
                    </div>

                    <h3 class="text-xl font-semibold text-neutral-800 mb-4 text-center">Analyse: Kostensteigerung am Spotmarkt</h3>
                    <div class="chart-container">
                        <canvas id="kostenChart"></canvas>
                    </div>
                </div>

                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-amber-900 mb-6">Unsere Strategien zur Risikominderung</h2>
                    <div class="space-y-4" id="strategy-accordion">
                        
                        <div class="strategy-item">
                            <header data-parent="#strategy-accordion">
                                <h3 class="font-semibold text-lg text-neutral-800">1. Multi-Sourcing & Redesign</h3>
                                <span class="text-2xl text-sky-700 transition-transform duration-300 transform">+</span>
                            </header>
                            <div class="content hidden">
                                <p class="text-neutral-700">Die Technik (Engineering) sucht intensiv nach technisch kompatiblen Alternativ-Bauteilen ("Multi-Sourcing"). Wo möglich, werden Baugruppen auf verfügbare Standardkomponenten umgestellt ("Redesign"), um die Abhängigkeit von einzelnen Lieferanten zu reduzieren.</p>
                            </div>
                        </div>

                        <div class="strategy-item">
                            <header data-parent="#strategy-accordion">
                                <h3 class="font-semibold text-lg text-neutral-800">2. Enge Lieferantenbindung</h3>
                                <span class="text-2xl text-sky-700 transition-transform duration-300 transform">+</span>
                            </header>
                            <div class="content hidden">
                                <p class="text-neutral-700">Der Einkauf intensiviert die Kommunikation mit unseren strategischen Distributoren und Herstellern. Durch transparente, langfristige Bedarfsplanung (Forecasts) und Rahmenverträge versuchen wir, uns zukünftige Kontingente zu sichern.</p>
                            </div>
                        </div>

                        <div class="strategy-item">
                            <header data-parent="#strategy-accordion">
                                <h3 class="font-semibold text-lg text-neutral-800">3. Pufferlager aufbauen</h3>
                                <span class="text-2xl text-sky-700 transition-transform duration-300 transform">+</span>
                            </header>
                            <div class="content hidden">
                                <p class="text-neutral-700">Wir weichen vom reinen Just-in-Time-Prinzip ab und bauen gezielt Pufferlager für kritische Bauteile (insb. C-Teile mit langen Lieferzeiten) auf. Dies erhöht zwar die Lagerbestände, sichert aber die Produktionsfähigkeit.</p>
                            </div>
                        </div>
                        
                        <div class="strategy-item">
                            <header data-parent="#strategy-accordion">
                                <h3 class="font-semibold text-lg text-neutral-800">4. Vorausschauende Bedarfsplanung</h3>
                                <span class="text-2xl text-sky-700 transition-transform duration-300 transform">+</span>
                            </header>
                            <div class="content hidden">
                                <p class="text-neutral-700">Die Zusammenarbeit zwischen Vertrieb, Technik und Einkauf wird verstärkt. Der Vertrieb muss den Bedarf so früh wie möglich melden (mind. 12-18 Monate im Voraus), damit der Einkauf langfristig bestellen und Kapazitäten reservieren kann.</p>
                            </div>
                        </div>

                    </div>
                </div>
            </div>
        </main>

        <main id="outlook" class="content-section">
            <header class="mb-8">
                <h1 class="text-4xl font-bold text-sky-800 mb-2">Fazit und Ausblick</h1>
                <p class="text-xl text-neutral-700">Was wir gelernt haben und was auf uns zukommt.</p>
            </header>

            <section class="mb-12">
                <p class="text-lg text-neutral-800 mb-6">
                    Die Allocation-Krise hat die globalen Lieferketten nachhaltig verändert. Eine vollständige Entspannung der Märkte wird von Experten frühestens 2026-2027 erwartet. Für uns bei Pantel-Elektronik bedeutet dies, dass ein proaktives Risikomanagement in der Beschaffung kein temporärer Krisenmodus, sondern eine dauerhafte Kernkompetenz bleibt.
                </p>
            </section>

            <div class="grid md:grid-cols-2 gap-6">
                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-3">Zusammenfassung</h2>
                    <ul class="list-disc list-inside text-neutral-700 space-y-2">
                        <li>Allocation ist ein massives globales Ungleichgewicht von Nachfrage und Kapazität.</li>
                        <li>Pantel-Elektronik ist durch hohe Kosten und Lieferverzögerungen direkt betroffen.</li>
                        <li>Unsere Reaktion ist eine enge Verzahnung von Einkauf, Technik und strategischer Lagerhaltung.</li>
                    </ul>
                </div>
                <div class="info-card">
                    <h2 class="text-2xl font-semibold text-sky-900 mb-3">Ausblick</h2>
                    <ul class="list-disc list-inside text-neutral-700 space-y-2">
                        <li>Die Märkte bleiben volatil (schwankungsanfällig).</li>
                        <li>Lieferketten werden "resilienter" (widerstandsfähiger), z.B. durch Regionalisierung (Aufbau von Fabriken in EU/USA).</li>
                        <li>Für Industriekaufleute wird die strategische Beschaffung wichtiger als je zuvor.</li>
                    </ul>
                </div>
            </div>
        </main>

    </div>

    <footer class="bg-white border-t border-neutral-200 mt-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 text-center">
            <p class="text-sm text-neutral-600">&copy; [Aktuelles Jahr] Pantel-Elektronik | Interaktiver Report | [Ihr Name]</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            
            const navLinks = document.querySelectorAll('.nav-link');
            const mobileNav = document.getElementById('mobile-nav');
            const contentSections = document.querySelectorAll('.content-section');
            const linkButtons = document.querySelectorAll('a[data-target-link]');

            function switchTab(targetId) {
                contentSections.forEach(section => {
                    section.classList.remove('active');
                });
                const activeSection = document.getElementById(targetId);
                if (activeSection) {
                    activeSection.classList.add('active');
                }

                navLinks.forEach(link => {
                    if (link.dataset.target === targetId) {
                        link.classList.add('active');
                    } else {
                        link.classList.remove('active');
                    }
                });

                mobileNav.value = targetId;
                window.scrollTo(0, 0);
            }

            navLinks.forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const targetId = this.dataset.target;
                    switchTab(targetId);
                    window.location.hash = targetId;
                });
            });

            linkButtons.forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const targetId = this.dataset.targetLink;
                    switchTab(targetId);
                    window.location.hash = targetId;
                });
            });

            mobileNav.addEventListener('change', function(e) {
                switchTab(e.target.value);
                window.location.hash = e.target.value;
            });

            if (window.location.hash) {
                const targetId = window.location.hash.substring(1);
                if (document.getElementById(targetId)) {
                    switchTab(targetId);
                }
            }

            const accordionHeaders = document.querySelectorAll('#strategy-accordion header');
            accordionHeaders.forEach(header => {
                header.addEventListener('click', function() {
                    const content = this.nextElementSibling;
                    const icon = this.querySelector('span');
                    
                    if (content.classList.contains('hidden')) {
                        content.classList.remove('hidden');
                        icon.classList.add('rotate-45');
                        icon.textContent = '+';
                    } else {
                        content.classList.add('hidden');
                        icon.classList.remove('rotate-45');
                        icon.textContent = '+'; 
                    }
                });
            });
            
            Chart.defaults.font.family = "'Inter', sans-serif";
            
            function createKostenChart() {
                const ctx = document.getElementById('kostenChart');
                if (!ctx) return;

                const chartData = {
                    labels: ['Microcontroller (MCU)', 'Power-Management-IC (PMIC)', 'Spezial-Kondensator'],
                    datasets: [
                        {
                            label: 'Normaler Vertragspreis (€)',
                            data: [5.50, 2.10, 0.80],
                            backgroundColor: 'rgba(59, 130, 246, 0.7)',
                            borderColor: 'rgba(59, 130, 246, 1)',
                            borderWidth: 1
                        },
                        {
                            label: 'Aktueller Spotmarkt-Preis (€)',
                            data: [55.00, 28.50, 9.00],
                            backgroundColor: 'rgba(239, 68, 68, 0.7)',
                            borderColor: 'rgba(239, 68, 68, 1)',
                            borderWidth: 1
                        }
                    ]
                };

                new Chart(ctx, {
                    type: 'bar',
                    data: chartData,
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: {
                            y: {
                                beginAtZero: true,
                                title: {
                                    display: true,
                                    text: 'Einkaufspreis in Euro (€)'
                                }
                            },
                            x: {
                                title: {
                                    display: true,
                                    text: 'Beispiel-Bauteile'
                                }
                            }
                        },
                        plugins: {
                            title: {
                                display: true,
                                text: 'Vergleich: Vertrags- vs. Spotmarkt-Preise',
                                font: {
                                    size: 16
                                }
                            },
                            tooltip: {
                                mode: 'index',
                                intersect: false,
                                callbacks: {
                                    label: function(context) {
                                        let label = context.dataset.label || '';
                                        if (label) {
                                            label += ': ';
                                        }
                                        if (context.parsed.y !== null) {
                                            label += new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR' }).format(context.parsed.y);
                                        }
                                        return label;
                                    }
                                }
                            }
                        }
                    }
                });
            }

            const companyTabObserver = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if(entry.isIntersecting){
                        if(document.getElementById('company').classList.contains('active')){
                            createKostenChart();
                            observer.unobserve(entry.target);

                        }
                    }
                });
            }, { threshold: 0.1 });
            
            const companySection = document.getElementById('company');
            if(companySection) {
                companyTabObserver.observe(companySection);
                
                document.querySelectorAll('.nav-link[data-target="company"], a[data-target-link="company"]').forEach(link => {
                    link.addEventListener('click', () => {
                        setTimeout(() => {
                            if (!document.getElementById('kostenChart')._chart) {
                                createKostenChart();
                            }
                        }, 100);
                    });
                });
                
                if(companySection.classList.contains('active')) {
                     createKostenChart();
                     companyTabObserver.unobserve(companySection);
                }
            }
        });
    </script>
</body>
</html>
