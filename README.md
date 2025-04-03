
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kapłani Niezłomni - Prawda zapisana w ogniu</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
    <style>
        body {
            background-color: #f0e6d2;
            color: #333;
            font-family: 'Courier New', Courier, monospace;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-image: url('https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/old-paper.jpg');
            background-size: cover;
            background-attachment: fixed;
            position: relative;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }
        
        /* Sekcja wsparcia - TAJNA INSTRUKCJA */
        .support-box {
            position: fixed;
            bottom: 20px;
            right: 20px;
            width: 300px;
            background: rgba(240, 230, 210, 0.95);
            border: 1px solid #5D2906;
            border-radius: 3px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            z-index: 1000;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.9em;
            transform: rotate(0deg);
            transition: all 0.3s;
            opacity: 0.9;
        }
        
        .support-box:hover {
            box-shadow: 0 0 15px rgba(93, 41, 6, 0.3);
        }
        
        .support-header {
            background: #5D2906;
            color: #f0e6d2;
            padding: 8px;
            text-align: center;
            font-weight: normal;
            letter-spacing: 0.5px;
        }
        
        .support-content {
            padding: 15px;
            color: #333;
            line-height: 1.5;
        }
        
        .support-options {
            margin: 15px 0;
        }
        
        .support-btn {
            display: block;
            background: #8B4513;
            color: #f0e6d2;
            padding: 8px;
            margin: 10px 0;
            text-align: center;
            text-decoration: none;
            border-radius: 2px;
            transition: background 0.3s;
            font-size: 0.85em;
        }
        
        .support-btn:hover {
            background: #5D2906;
        }
        
        .support-btn img {
            vertical-align: middle;
            margin-right: 8px;
            width: 18px;
            height: 18px;
        }
        
        .bank-details {
            background: rgba(93, 41, 6, 0.05);
            padding: 10px;
            margin-top: 15px;
            border-left: 1px solid #5D2906;
            font-size: 0.8em;
        }
        
        .support-note {
            font-size: 0.75em;
            font-style: italic;
            margin-top: 15px;
            color: #5D2906;
        }

        /* Reszta stylów */
        header {
            text-align: center;
            padding: 30px 0;
            border-bottom: 1px solid #5D2906;
            margin-bottom: 40px;
            position: relative;
        }
        
        h1 {
            color: #5D2906;
            font-size: 2.5em;
            margin: 0;
            animation: fadeIn 2s;
            letter-spacing: 1px;
        }
        
        h2 {
            color: #5D2906;
            border-bottom: 1px solid #5D2906;
            padding-bottom: 8px;
            margin-top: 40px;
            font-size: 1.5em;
        }
        
        .typewriter-text {
            border-right: 1px solid #333;
            white-space: nowrap;
            overflow: hidden;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
            margin-bottom: 30px;
            font-size: 1em;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: #333 }
        }
        
        .timeline {
            position: relative;
            max-width: 800px;
            margin: 40px auto;
        }
        
        .timeline::after {
            content: '';
            position: absolute;
            width: 1px;
            background-color: #5D2906;
            top: 0;
            bottom: 0;
            left: 50%;
            margin-left: -1px;
        }
        
        .timeline-item {
            padding: 10px 40px;
            position: relative;
            width: 50%;
            box-sizing: border-box;
            animation: fadeIn 1s;
        }
        
        .timeline-item::after {
            content: '';
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: #5D2906;
            border-radius: 50%;
            top: 15px;
            z-index: 1;
        }
        
        .left {
            left: 0;
            text-align: right;
        }
        
        .right {
            left: 50%;
            text-align: left;
        }
        
        .left::after {
            right: -7px;
        }
        
        .right::after {
            left: -7px;
        }
        
        .timeline-content {
            padding: 15px;
            background-color: rgba(255, 255, 255, 0.8);
            border: 1px solid #5D2906;
            border-radius: 3px;
            font-size: 0.95em;
        }
        
        .gallery {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
        }
        
        .gallery-item {
            width: 200px;
            height: 200px;
            overflow: hidden;
            border: 1px solid #5D2906;
            position: relative;
            transition: transform 0.3s;
        }
        
        .gallery-item:hover {
            transform: scale(1.03);
            z-index: 2;
        }
        
        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .gallery-caption {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba(93, 41, 6, 0.8);
            color: #f0e6d2;
            padding: 5px;
            text-align: center;
            font-size: 0.85em;
        }
        
        .contact-form {
            background-color: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border: 1px solid #5D2906;
            margin-top: 40px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
        }
        
        input, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #5D2906;
            background-color: rgba(240, 230, 210, 0.7);
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.95em;
        }
        
        button {
            background-color: #5D2906;
            color: #f0e6d2;
            border: none;
            padding: 8px 16px;
            cursor: pointer;
            font-family: 'Courier New', Courier, monospace;
            transition: background-color 0.3s;
            font-size: 0.95em;
        }
        
        button:hover {
            background-color: #3a1a04;
        }
        
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            border-top: 1px solid #5D2906;
            font-size: 0.85em;
        }
        
        .stamp {
            position: absolute;
            opacity: 0.7;
            transform: rotate(15deg);
            z-index: 1;
        }
        
        .stamp-1 {
            right: 50px;
            top: 50px;
            width: 100px;
        }
        
        .stamp-2 {
            left: 30px;
            bottom: 100px;
            width: 80px;
            transform: rotate(-10deg);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        /* Mapa Dachau */
        .dachau-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 20px;
        }
        
        .dachau-title {
            flex: 1;
        }
        
        #dachau-map {
            height: 400px;
            width: 100%;
            border: 1px solid #5D2906;
            margin-bottom: 20px;
        }
        
        .map-caption {
            font-size: 0.85em;
            text-align: center;
            color: #5D2906;
            margin-bottom: 30px;
        }
        
        @media screen and (max-width: 768px) {
            .timeline::after {
                left: 31px;
            }
            
            .timeline-item {
                width: 100%;
                padding-left: 70px;
                padding-right: 25px;
            }
            
            .timeline-item::after {
                left: 21px;
            }
            
            .left, .right {
                left: 0;
                text-align: left;
            }
            
            .support-box {
                width: 90%;
                right: 5%;
                bottom: 10px;
            }
            
            .dachau-header {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- Znaczki -->
    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/secret-stamp.png" alt="Tajne" class="stamp stamp-1">
    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/confidential-stamp.png" alt="Poufne" class="stamp stamp-2">
    
    <div class="container">
        <header>
            <div class="dachau-header">
                <div class="dachau-title">
                    <h1>KAPŁANI NIEZŁOMNI</h1>
                    <p class="typewriter-text">Prawda zapisana w ogniu prześladowań...</p>
                </div>
                <div id="dachau-map"></div>
            </div>
            <h2>Polscy kapłani w Dachau</h2>
        </header>
        
        <!-- Sekcja wprowadzająca -->
        <section>
            <h2>◈ WSTĘP ◈</h2>
            <div class="typewriter-text">
                <p>W czasach PRL-u, gdy system komunistyczny dążył do wynarodowienia i ateizacji społeczeństwa, grupa kapłanów stanęła w obronie wiary i polskości. Wielu zapłaciło za to najwyższą cenę...</p>
            </div>
            <p>Strona ta poświęcona jest pamięci duchownych, którzy mimo represji, tortur i śmierci, pozostali wierni swoim ideałom. To hołd dla tych, o których historia przez długie lata milczała.</p>
        </section>
        
        <!-- Linia czasu -->
        <section>
            <h2>◈ KALENDARIUM MĘCZEŃSTWA ◈</h2>
            <div class="timeline">
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3>1945</h3>
                        <p>Początek masowych aresztowań duchownych przez UB. Więzieni m.in. bp Antoni Baraniak, ks. Zygmunt Kaczyński.</p>
                    </div>
                </div>
                <div class="timeline-item right">
                    <div class="timeline-content">
                        <h3>1948</h3>
                        <p>Ks. Franciszek Gurgacz SJ zostaje kapelanem Polskiej Podziemnej Armii Niepodległościowej.</p>
                    </div>
                </div>
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3>14.09.1949</h3>
                        <p>Rozstrzelanie ks. Franciszka Gurgacza w więzieniu Montelupich w Krakowie.</p>
                    </div>
                </div>
                <div class="timeline-item right">
                    <div class="timeline-content">
                        <h3>1953</h3>
                        <p>Aresztowanie Prymasa Stefana Wyszyńskiego. Internowanie w klasztorze w Komańczy.</p>
                    </div>
                </div>
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3>19.10.1984</h3>
                        <p>Porwanie i morderstwo ks. Jerzego Popiełuszki przez funkcjonariuszy SB.</p>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Galeria -->
        <section>
            <h2>◈ GALERIA PAMIĘCI ◈</h2>
            <div class="gallery">
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/gurgacz.jpg" alt="Ks. Franciszek Gurgacz">
                    <div class="gallery-caption">Ks. Franciszek Gurgacz SJ (1914-1949)</div>
                </div>
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/kotlarz.jpg" alt="Ks. Roman Kotlarz">
                    <div class="gallery-caption">Ks. Roman Kotlarz (1928-1976)</div>
                </div>
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/popieluszko.jpg" alt="Ks. Jerzy Popiełuszko">
                    <div class="gallery-caption">Ks. Jerzy Popiełuszko (1947-1984)</div>
                </div>
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/wyszynski.jpg" alt="Prymas Stefan Wyszyński">
                    <div class="gallery-caption">Prymas Stefan Wyszyński (1901-1981)</div>
                </div>
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/ub-interrogation.jpg" alt="Przesłuchanie przez UB">
                    <div class="gallery-caption">Przesłuchanie duchownego przez UB</div>
                </div>
                <div class="gallery-item">
                    <img src="https://raw.githubusercontent.com/twoj-login/twoj-repozytorium/main/montelupich.jpg" alt="Więzienie Montelupich">
                    <div class="gallery-caption">Więzienie Montelupich w Krakowie</div>
                </div>
            </div>
        </section>
        
        <!-- Biografie -->
        <section>
            <h2>◈ PORTETY NIEZŁOMNYCH ◈</h2>
            
            <h3>Ks. Franciszek Gurgacz SJ - "Kapelan Wyklętych"</h3>
            <p>Jezuita, kapelan Polskiej Podziemnej Armii Niepodległościowej. Aresztowany przez UB w 1949 roku. W sfingowanym procesie skazany na śmierć za "zdradę narodu polskiego". Rozstrzelany 14 września 1949 roku w więzieniu Montelupich.</p>
            
            <h3>Ks. Roman Kotlarz - "Męczennik Radomski"</h3>
            <p>Proboszcz z Pelagowa, który odważył się publicznie poprzeć robotnicze protesty w Radomiu w 1976 roku. Dotkliwie pobity przez SB, zmarł w niewyjaśnionych okolicznościach. Jego pogrzeb stał się manifestacją antykomunistyczną.</p>
            
            <h3>Ks. Jerzy Popiełuszko - "Kapelan Solidarności"</h3>
            <p>Duszpasterz ludzi pracy, symbol oporu przeciwko reżimowi. Uprowadzony i bestialsko zamordowany przez funkcjonariuszy SB w 1984 roku. Jego śmierć wstrząsnęła Polską i przyspieszyła upadek systemu.</p>
        </section>
        
        <!-- Formularz kontaktowy -->
        <section>
            <h2>◈ ZGŁOŚ WIADOMOŚĆ ◈</h2>
            <div class="contact-form">
                <p>Masz informacje o zapomnianych kapłanach-męczennikach? Znane Ci są rodzinne historie związane z prześladowaniami duchowieństwa? Napisz do nas!</p>
                
                <form action="https://formspree.io/f/your-form-id" method="POST">
                    <div class="form-group">
                        <label for="name">Imię i nazwisko:</label>
                        <input type="text" id="name" name="name" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="email">E-mail:</label>
                        <input type="email" id="email" name="email" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="message">Wiadomość:</label>
                        <textarea id="message" name="message" rows="5" required></textarea>
                    </div>
                    
                    <button type="submit">Wyślij depeszę</button>
                </form>
            </div>
        </section>
        
        <footer>
            <p>Strona powstała w hołdzie kapłanom, którzy oddali życie za wiarę i wolną Polskę</p>
            <p>© 2023 Stowarzyszenie Pamięci Kapłanów Niezłomnych</p>
        </footer>
    </div>
    
    <!-- SEKCJA WSPARCIA -->
    <div class="support-box">
        <div class="support-header">WSPARCIE DLA ARCHIWUM</div>
        <div class="support-content">
            <p>Jeśli chcesz pomóc w utrzymaniu archiwum, przekaż darowiznę na:</p>
            
            <div class="support-options">
                <!-- BuyMeACoffee - bardziej dyskretny -->
                <a href="https://www.buymeacoffee.com/twojprofil" target="_blank" class="support-btn">
                    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Wsparcie">
                    Wsparcie finansowe
                </a>
                
                <!-- PayPal -->
                <a href="https://paypal.me/twojprofil" target="_blank" class="support-btn">
                    <img src="https://www.paypalobjects.com/webstatic/mktg/logo/pp_cc_mark_37x23.jpg" alt="PayPal">
                    Przelew PayPal
                </a>
                
                <!-- Bank -->
                <div class="bank-details">
                    <p>TRADYCYJNY PRZELEW:</p>
                    <p>Stowarzyszenie Pamięci<br>
                    <strong>PL 12 3456 7890 0000 1111 2222 3333</strong></p>
                </div>
            </div>
            
            <p class="support-note">Środki zostaną wykorzystane na:<br>
            - Opłacenie serwera<br>
            - Zakup domeny<br>
            - Digitalizację dokumentów</p>
        </div>
    </div>

    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
    <script>
        // Inicjalizacja mapy Dachau
        const map = L.map('dachau-map').setView([48.2699, 11.4663], 15);
        
        // Dodanie warstwy mapy
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(map);
        
        // Dodanie znaczników dla miejsc związanych z kapłanami
        const priestMarkers = [
            {
                lat: 48.2699,
                lng: 11.4663,
                title: "Obóz koncentracyjny Dachau",
                description: "Miejsce przetrzymywania i męczeństwa wielu polskich kapłanów w czasie II wojny światowej."
            },
            {
                lat: 48.2675,
                lng: 11.4682,
                title: "Barak 28",
                description: "Barak, w którym przetrzymywano polskich księży. Wielu zmarło z powodu ciężkich warunków."
            },
            {
                lat: 48.2712,
                lng: 11.4647,
                title: "Kaplica Śmiertelnego Lęku Chrystusa",
                description: "Miejsce modlitwy więzionych kapłanów. Zbudowana po wojnie jako pomnik męczeństwa."
            }
        ];
        
        // Dodanie znaczników do mapy
        priestMarkers.forEach(marker => {
            L.marker([marker.lat, marker.lng])
                .addTo(map)
                .bindPopup(`<b>${marker.title}</b><br>${marker.description}`);
        });
        
        // Dodanie warstwy z grobami
        const gravesLayer = L.layerGroup().addTo(map);
        
        // Przykładowe groby (można dodać więcej danych)
        const graves = [
            {
                lat: 48.2705,
                lng: 11.4671,
                title: "Grób ks. Jana Kowalskiego",
                description: "Zmarł 12 marca 1942 roku z wycieńczenia."
            },
            {
                lat: 48.2688,
                lng: 11.4659,
                title: "Grób ks. Andrzeja Nowaka",
                description: "Rozstrzelany 5 maja 1941 roku za organizowanie modlitw."
            }
        ];
        
        graves.forEach(grave => {
            L.marker([grave.lat, grave.lng], {
                icon: L.divIcon({
                    className: 'grave-marker',
                    html: '✟',
                    iconSize: [20, 20]
                })
            })
            .addTo(gravesLayer)
            .bindPopup(`<b>${grave.title}</b><br>${grave.description}`);
        });
    </script>
</body>
</html>
