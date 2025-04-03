<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kapłani Niezłomni - Prawda zapisana w ogniu</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
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
            width: 60px;
            height: 60px;
            background: #5D2906;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(0,0,0,0.2);
            z-index: 1000;
            cursor: pointer;
            transition: all 0.3s ease;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #f0e6d2;
            font-size: 12px;
            text-align: center;
            padding: 5px;
        }
        
        .support-box:hover {
            width: 300px;
            height: auto;
            border-radius: 5px;
            padding: 0;
        }
        
        .support-box.expanded {
            width: 300px;
            height: auto;
            border-radius: 5px;
            padding: 0;
        }
        
        .support-box .support-icon {
            display: block;
        }
        
        .support-box:hover .support-icon,
        .support-box.expanded .support-icon {
            display: none;
        }
        
        .support-header {
            background: #3a1a04;
            color: #f0e6d2;
            padding: 8px;
            text-align: center;
            font-weight: normal;
            display: none;
        }
        
        .support-content {
            padding: 15px;
            color: #333;
            line-height: 1.5;
            display: none;
            background: rgba(240, 230, 210, 0.95);
        }
        
        .support-box:hover .support-header,
        .support-box:hover .support-content,
        .support-box.expanded .support-header,
        .support-box.expanded .support-content {
            display: block;
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
        
        h3 {
            color: #5D2906;
            margin-top: 25px;
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
            background-color: rgba(255, 255, 255, 0.7);
        }
        
        .footer-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 15px;
        }
        
        .footer-links a {
            color: #5D2906;
            text-decoration: none;
        }
        
        .footer-links a:hover {
            text-decoration: underline;
        }
        
        .social-media {
            margin: 20px 0;
        }
        
        .social-media a {
            color: #5D2906;
            font-size: 1.5em;
            margin: 0 10px;
            transition: color 0.3s;
        }
        
        .social-media a:hover {
            color: #3a1a04;
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
        
        /* Sekcja edukacyjna */
        .education-section {
            background-color: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border: 1px solid #5D2906;
            margin-top: 40px;
        }
        
        .lesson-plan {
            margin-top: 20px;
        }
        
        .lesson-item {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px dashed #5D2906;
        }
        
        .lesson-title {
            font-weight: bold;
            color: #5D2906;
        }
        
        .pdf-download {
            display: inline-block;
            background-color: #5D2906;
            color: #f0e6d2;
            padding: 5px 10px;
            margin-top: 5px;
            text-decoration: none;
            font-size: 0.85em;
        }
        
        .pdf-download:hover {
            background-color: #3a1a04;
        }
        
        /* Biografie kapłanów */
        .priest-bio {
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #5D2906;
        }
        
        .bio-link {
            color: #5D2906;
            text-decoration: none;
            font-weight: bold;
        }
        
        .bio-link:hover {
            text-decoration: underline;
        }
        
        /* Sekcja męczenników */
        .martyrs-section {
            background-color: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border: 1px solid #5D2906;
            margin-top: 40px;
        }
        
        .martyrs-gallery {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        
        .martyr-card {
            width: calc(33% - 15px);
            min-width: 250px;
            background-color: rgba(240, 230, 210, 0.9);
            border: 1px solid #5D2906;
            padding: 15px;
        }
        
        .martyr-name {
            font-weight: bold;
            color: #5D2906;
            margin-bottom: 5px;
        }
        
        .martyr-details {
            font-size: 0.9em;
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
            
            .martyr-card {
                width: 100%;
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
            
            <div class="priest-bio">
                <h3><a href="biografia-gurgacz.html" class="bio-link">Ks. Franciszek Gurgacz SJ - "Kapelan Wyklętych"</a></h3>
                <p>Jezuita, kapelan Polskiej Podziemnej Armii Niepodległościowej. Aresztowany przez UB w 1949 roku. W sfingowanym procesie skazany na śmierć za "zdradę narodu polskiego". Rozstrzelany 14 września 1949 roku w więzieniu Montelupich.</p>
            </div>
            
            <div class="priest-bio">
                <h3><a href="biografia-kotlarz.html" class="bio-link">Ks. Roman Kotlarz - "Męczennik Radomski"</a></h3>
                <p>Proboszcz z Pelagowa, który odważył się publicznie poprzeć robotnicze protesty w Radomiu w 1976 roku. Dotkliwie pobity przez SB, zmarł w niewyjaśnionych okolicznościach. Jego pogrzeb stał się manifestacją antykomunistyczną.</p>
            </div>
            
            <div class="priest-bio">
                <h3><a href="biografia-popieluszko.html" class="bio-link">Ks. Jerzy Popiełuszko - "Kapelan Solidarności"</a></h3>
                <p>Duszpasterz ludzi pracy, symbol oporu przeciwko reżimowi. Uprowadzony i bestialsko zamordowany przez funkcjonariuszy SB w 1984 roku. Jego śmierć wstrząsnęła Polską i przyspieszyła upadek systemu.</p>
            </div>
            
            <div class="priest-bio">
                <h3><a href="biografia-wyszynski.html" class="bio-link">Prymas Stefan Wyszyński - "Prymas Tysiąclecia"</a></h3>
                <p>Kardynał, prymas Polski, przywódca duchowy narodu w czasach komunizmu. Internowany w latach 1953-1956. Inicjator Wielkiej Nowenny przed Millenium Chrztu Polski. Jego niezłomna postawa dała siłę Kościołowi i narodowi.</p>
            </div>
        </section>
        
        <!-- Sekcja męczenników niemieckich i sowieckich -->
        <section class="martyrs-section">
            <h2>◈ KAPŁANI POMORDOWANI PRZEZ NIEMCÓW I SOWIETÓW ◈</h2>
            <p>W czasie II wojny światowej tysiące polskich kapłanów stało się ofiarami nazistowskich Niemiec i sowieckiego reżimu. Oto niektóre z tych postaci:</p>
            
            <div class="martyrs-gallery">
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Maksymilian Kolbe</div>
                    <div class="martyr-details">Franciszkanin, męczennik Auschwitz, dobrowolnie oddał życie za współwięźnia. Zmarł 14 sierpnia 1941 roku.</div>
                </div>
                
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Stefan Frelichowski</div>
                    <div class="martyr-details">Duszpasterz harcerzy, więzień Dachau. Zmarł 23 lutego 1945 roku na tyfus, którym zaraził się opiekując chorymi.</div>
                </div>
                
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Władysław Goral</div>
                    <div class="martyr-details">Biskup pomocniczy lubelski, aresztowany przez Gestapo w 1939 roku. Zmarł w Sachsenhausen w 1945 roku.</div>
                </div>
                
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Zygmunt Pisarski</div>
                    <div class="martyr-details">Proboszcz z Gdeszyna, rozstrzelany przez Niemców 30 stycznia 1943 roku za pomoc Żydom.</div>
                </div>
                
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Jan Leon Ziółkowski</div>
                    <div class="martyr-details">Proboszcz z Białegostoku, zamordowany przez NKWD w 1940 roku w ramach zbrodni katyńskiej.</div>
                </div>
                
                <div class="martyr-card">
                    <div class="martyr-name">Ks. Antoni Beszta-Borowski</div>
                    <div class="martyr-details">Proboszcz z Bielska Podlaskiego, rozstrzelany przez Niemców 15 lipca 1943 roku wraz z 49 innymi osobami.</div>
                </div>
            </div>
        </section>
        
        <!-- Sekcja edukacyjna -->
        <section class="education-section">
            <h2>◈ SEKCJA EDUKACYJNA DLA MŁODZIEŻY ◈</h2>
            <p>Materiały edukacyjne dla młodzieży od 16 roku życia, przygotowane we współpracy z historykami i pedagogami.</p>
            
            <h3>Przykładowy plan lekcji:</h3>
            <div class="lesson-plan">
                <div class="lesson-item">
                    <div class="lesson-title">Lekcja 1: Kim byli Kapłani Niezłomni?</div>
                    <p>Wprowadzenie do tematu, definicja pojęcia, kontekst historyczny.</p>
                    <a href="#" class="pdf-download">Pobierz materiały (PDF, 2.4MB)</a>
                </div>
                
                <div class="lesson-item">
                    <div class="lesson-title">Lekcja 2: Metody prześladowań duchowieństwa w PRL</div>
                    <p>Inwigilacja, prowokacje, procesy pokazowe, metody pracy SB.</p>
                    <a href="#" class="pdf-download">Pobierz materiały (PDF, 1.8MB)</a>
                </div>
                
                <div class="lesson-item">
                    <div class="lesson-title">Lekcja 3: Najważniejsze postacie</div>
                    <p>Sylwetki ks. Popiełuszki, ks. Gurgacza, Prymasa Wyszyńskiego i innych.</p>
                    <a href="#" class="pdf-download">Pobierz materiały (PDF, 3.1MB)</a>
                </div>
                
                <div class="lesson-item">
                    <div class="lesson-title">Lekcja 4: Kapłani-męczennicy II wojny światowej</div>
                    <p>Duchowieństwo w obozach koncentracyjnych i łagrach.</p>
                    <a href="#" class="pdf-download">Pobierz materiały (PDF, 2.7MB)</a>
                </div>
                
                <div class="lesson-item">
                    <div class="lesson-title">Lekcja 5: Źródła historyczne i praca z dokumentami</div>
                    <p>Jak badać historię Kapłanów Niezłomnych? Praktyczne wskazówki.</p>
                    <a href="#" class="pdf-download">Pobierz materiały (PDF, 1.5MB)</a>
                </div>
            </div>
            
            <h3>Dodatkowe materiały:</h3>
            <ul>
                <li><a href="#" class="pdf-download">Kronika prześladowań Kościoła w PRL (PDF)</a></li>
                <li><a href="#" class="pdf-download">Słownik biograficzny duchownych ofiar komunizmu (PDF)</a></li>
                <li><a href="#" class="pdf-download">Wywiady z żyjącymi świadkami historii (PDF + audio)</a></li>
            </ul>
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
            <div class="social-media">
                <a href="#" title="Facebook"><i class="fab fa-facebook"></i></a>
                <a href="#" title="Twitter"><i class="fab fa-twitter"></i></a>
                <a href="#" title="YouTube"><i class="fab fa-youtube"></i></a>
                <a href="#" title="Instagram"><i class="fab fa-instagram"></i></a>
            </div>
            
            <div class="footer-links">
                <a href="#">Polityka prywatności</a>
                <a href="#">Kontakt</a>
                <a href="#">O projekcie</a>
                <a href="#">Współpraca</a>
                <a href="#">Archiwum</a>
            </div>
            
            <p>Strona powstała w hołdzie kapłanom, którzy oddali życie za wiarę i wolną Polskę</p>
            <p>© 2023 Stowarzyszenie Kapłani Niezłomni | Wszelkie prawa zastrzeżone</p>
        </footer>
    </div>
    
    <!-- SEKCJA WSPARCIA -->
    <div class="support-box" id="supportBox">
        <div class="support-icon">WSPARCIE</div>
        <div class="support-header">WSPARCIE DLA ARCHIWUM</div>
        <div class="support-content">
            <p>Jeśli chcesz pomóc w utrzymaniu archiwum, przekaż darowiznę na:</p>
            
            <div class="support-options">
                <a href="https://www.buymeacoffee.com/twojprofil" target="_blank" class="support-btn">
                    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Wsparcie">
                    Wsparcie finansowe
                </a>
                
                <a href="https://paypal.me/twojprofil" target="_blank" class="support-btn">
                    <img src="https://www.paypalobjects.com/webstatic/mktg/logo/pp_cc_mark_37x23.jpg" alt="PayPal">
                    Przelew PayPal
                </a>
                
                <div class="bank-details">
                    <p>TRADYCYJNY PRZELEW:</p>
                    <p>Stowarzyszenie Kapłani Niezłomni<br>
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
        
        // Obsługa sekcji wsparcia
        const supportBox = document.getElementById('supportBox');
        
        supportBox.addEventListener('click', function(e) {
            e.stopPropagation();
            this.classList.toggle('expanded');
        });
        
        // Zamykanie sekcji wsparcia po kliknięciu gdzie indziej
        document.addEventListener('click', function() {
            supportBox.classList.remove('expanded');
        });
        
        // Zapobieganie zamykaniu przy kliknięciu wewnątrz
        supportBox.querySelector('.support-content').addEventListener('click', function(e) {
            e.stopPropagation();
        });
    </script>
</body>
</html>
