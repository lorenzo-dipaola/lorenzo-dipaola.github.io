---
layout: single
title: "ViVo – Visualizing Voices"
description: "ViVo (Visualizing Voices) is a research project on Corriere dei Piccoli, oral culture, childhood, and the transformation of Italian comics within media ecology."
permalink: /projects/vivo/
author_profile: true
---



## Project overview

ViVo (*Visualising Voices*) is an FNRS-funded research project hosted at the Université libre de Bruxelles.  
The project investigates *Corriere dei Piccoli* (1908–1931) as a key laboratory of Italian media culture in the early twentieth century.

Rather than treating *Corriere dei Piccoli* as an “immature” or technically limited form of comics, ViVo approaches the magazine as a **specific editorial device**, designed to translate oral and performative traditions into printed culture for children. In this perspective, the magazine functions as a space of mediation between popular orality, bourgeois pedagogy, and the emerging logics of mass culture.

Combining archival research and media analysis, ViVo examines how images, texts, seriality, and advertising contributed to shaping new ways of reading, seeing, and learning.

---

## Phase 1 – Remediating orality: *La bande chantée*

The first phase of the project is grounded in the article *La bande chantée: tradition orale et croyances pédagogiques dans le Corriere dei Piccoli* (with Eva Van de Wiele).

The article reinterprets the use of rhymed captions instead of speech balloons not as a technical limitation, but as a **deliberate editorial choice**, closely linked to the cultural and pedagogical context of early twentieth-century Italy.

The analysis shows how the format of *Corriere dei Piccoli* remediates traditional performative practices, especially those of the **cantastorie**:

- illustrated posters are translated into the page grid;
- the sung voice becomes rhythmic, rhymed captions;
- public performance is relocated into domestic reading practices;
- ephemeral spectacle is transformed into printed seriality.

This model encourages adult-assisted reading and allows literacy training, pedagogical control, and early forms of cultural consumption to coexist within a single editorial environment.

---

## Visual examples

![Cantastorie with illustrated poster](/images/vivo-cantastorie.jpg)

*Cantastorie performing with illustrated posters (early 20th century).  
The performative model remediated by* Corriere dei Piccoli.

---

![Corriere dei Piccoli page with rhymed captions](/images/vivo-cdp-captions.jpg)

*A page from* Corriere dei Piccoli *showing the use of rhymed captions instead of speech balloons.*

---

## Phase 2 – Visual pedagogy and the colonial gaze

The second phase of ViVo extends the analysis from formal questions to issues of representation and ideology. At this stage, the project examines how *Corriere dei Piccoli* contributed to shaping a **visual pedagogy of race and otherness** in the early twentieth century.

Through the analysis of characters such as *BilBolBul*, *I tre Cinesini*, and *Il Negro Tom*, the research shows how racialised bodies were transformed into comic spectacle. Humour, visual deformation, and linguistic stereotyping work together to present the colonial “Other” as harmless, entertaining, and fundamentally different.

Presented at the conference *Comics and the Politics of Looking* (Ghent, 2025), this phase combines visual culture studies and postcolonial perspectives to show how children’s comics functioned as a form of “soft” pedagogy in a period marked by colonial expansion and national identity building.

---

![BilBolBul, Corriere dei Piccoli (1908–1909)](/images/vivo-bilbolbul.jpg)

*BilBolBul*, created by Attilio Mussino, is one of the earliest iconic characters of Italian comics.  
His Black body, constantly subjected to comic transformations and literalised linguistic gags, becomes a surface onto which racial stereotypes and colonial anxieties are projected, within an apparently playful and pedagogical framework.

---

## Phase 3 – Media ecology and cultural domestication

The third phase of ViVo adopts a media-ecological perspective, situating *Corriere dei Piccoli* within the broader Italian media ecosystem of the early twentieth century.

Rather than focusing on individual characters or stories, this phase examines the magazine as an **environment** in which narratives, images, pedagogical discourse, and advertising operate together. Particular attention is paid to processes of **cultural domestication**, through which international comics models were adapted to Italian moral and educational frameworks.

Case studies such as the transformation of *Buster Brown* into *Mimmo* and the Italian reinterpretation of *Little Nemo* show how global visual forms were reshaped to support a national project of childhood education and cultural regulation. This phase was presented at the conference *Popular Cultures* (Messina, 2025).

---
## Interactive Data Dashboard: Corriere dei Piccoli (1908-1909)

<div class="dashboard-container" style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center; margin-bottom: 40px; margin-top: 20px;">
    <div class="chart-box" style="background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); width: 45%; min-width: 300px;">
        <canvas id="autoriChart"></canvas>
    </div>
    <div class="chart-box" style="background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); width: 45%; min-width: 300px;">
        <canvas id="categorieChart"></canvas>
    </div>
</div>

<div class="table-box" style="background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); margin-bottom: 40px; overflow-x: auto;">
    <link rel="stylesheet" href="https://cdn.datatables.net/1.13.6/css/jquery.dataTables.min.css">
    <table id="dataTable" class="display" style="width:100%; text-align: left; font-size: 0.9em;">
        <thead>
            <tr>
                <th>Numero</th>
                <th>Pagina</th>
                <th>Categoria</th>
                <th>Titolo Opera</th>
                <th>Autore</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<script src="https://code.jquery.com/jquery-3.7.0.min.js"></script>
<script src="https://cdn.datatables.net/1.13.6/js/jquery.dataTables.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>

<script>
    Papa.parse("/files/vivo/dati-cdp.csv", {
        download: true,
        header: true,
        skipEmptyLines: true,
        complete: function(results) {
            let data = results.data;
            let tableBody = "";
            let autoriCount = {};
            let categorieCount = {};

            data.forEach(row => {
                tableBody += `<tr>
                    <td>${row['Numero'] || ''}</td>
                    <td>${row['Data.Pagina'] || ''}</td>
                    <td>${row['Data.Categoria'] || ''}</td>
                    <td>${row['Data.Titolo Opera / Sezione'] || ''}</td>
                    <td>${row['Data.Autore (Testi/Disegni)'] || ''}</td>
                </tr>`;

                let autore = row['Data.Autore (Testi/Disegni)'];
                if(autore && autore !== 'N.D.') {
                    autoriCount[autore] = (autoriCount[autore] || 0) + 1;
                }
                let categoria = row['Data.Categoria'];
                if(categoria) {
                    categorieCount[categoria] = (categorieCount[categoria] || 0) + 1;
                }
            });

            document.querySelector("#dataTable tbody").innerHTML = tableBody;
            
            $('#dataTable').DataTable({
                pageLength: 10,
                language: { url: "//cdn.datatables.net/plug-ins/1.13.6/i18n/en-GB.json" }
            });

            let autoriArray = Object.keys(autoriCount).map(key => ({ nome: key, conteggio: autoriCount[key] }));
            autoriArray.sort((a, b) => b.conteggio - a.conteggio);
            let top10Autori = autoriArray.slice(0, 10);

            new Chart(document.getElementById('autoriChart'), {
                type: 'bar',
                data: {
                    labels: top10Autori.map(a => a.nome),
                    datasets: [{
                        label: 'Publications',
                        data: top10Autori.map(a => a.conteggio),
                        backgroundColor: '#3498db'
                    }]
                }
            });

            let categorieArray = Object.keys(categorieCount).map(key => ({ nome: key, conteggio: categorieCount[key] }));
            categorieArray.sort((a, b) => b.conteggio - a.conteggio);
            let topCategorie = categorieArray.slice(0, 6);

            new Chart(document.getElementById('categorieChart'), {
                type: 'doughnut',
                data: {
                    labels: topCategorie.map(c => c.nome),
                    datasets: [{
                        data: topCategorie.map(c => c.conteggio),
                        backgroundColor: ['#e74c3c', '#2ecc71', '#f1c40f', '#9b59b6', '#34495e', '#e67e22']
                    }]
                }
            });
        }
    });
</script>

---
## Key publication

- **La bande chantée: tradition orale et croyances pédagogiques dans le *Corriere dei Piccoli***  
  (with Eva Van de Wiele), *Comicalités. Études de culture graphique*, 2024  
  [Read the article](https://journals.openedition.org/comicalites/9855)

---

## Conference presentations

- **Playing with the Other: Race, Spectacle and Visual Pedagogy in *Corriere dei Piccoli* (1908–1909)**  
  *Comics and the Politics of Looking*, Ghent, September 2025  
  [Download slides (PDF)](/files/vivo/vivo-ghent-2025.pdf)

- **Corriere dei Piccoli in the Italian Media Ecosystem: Orality, Childhood, and Cultural Transformation**  
  *Popular Cultures*, Messina, October 2025  
  [Download slides (PDF)](/files/vivo/vivo-messina-2025.pdf)
