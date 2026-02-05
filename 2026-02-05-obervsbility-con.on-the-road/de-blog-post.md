# ObservabilityCON - On The Road 2026

Am 5. Februar 2026 machte die **ObservabilityCON** in Frankfurt am Main Station. Das "On the Road"-Format komprimiert die Highlights der dreitägigen Flaggschiff-Konferenz von Grafana auf einen intensiven Tag. Mit rund 250 Teilnehmern bot das Event einen Einblick in die aktuelle Strategie von Grafana, den Einzug von KI in das Ökosystem.

## Opening Keynote: Open Source & Agentic AI

Die Keynote unterstrich Grafanas bewusstes Bekenntnis zu Open Source. Die Speaker betonten mehrfach, dass Grafana als Open-Source-Unternehmen agiert und dies auch so bleiben soll. Ein Großteil der Funktionen ist und bleibt in der Open-Source-Variante verfügbar; man verzichte sogar bewusst darauf, potenzielle Umsatzquellen zu monetarisieren, um die Community zu stärken.

Das technologische Highlight waren die neuen **KI-Features**. Grafana setzt hier nicht auf ein eigenes LLM, sondern investiert massiv in Prompt Engineering. Die gezeigten KI-Agenten können per Chat-Interaktion Daten aus quasi allen Datasources scannen. Per Klick auf "Deep Investigation" analysieren sie alle verfügbaren Datenquellen und liefern einen fertigen Bericht zur Fehlerursache – wenn man das passend aufsetzt auch schon, bevor ein Mensch überhaupt eingreift. Diese Funktionen sind aktuell in der Public Preview und exklusiv für die Grafana Cloud verfügbar.

## Session: Full-Stack Observability & Knowledge Graph

In dieser Session ging es um die Bewältigung von Systemkomplexität. Grafana Cloud führt hierfür drei Komponenten zusammen:
1. **Knowledge Graph:** Versteht die Beziehungen zwischen verschiedenen "Assets".
2. **Insights:** Automatische Erkennung von Mustern.
3. **RCA Workbench:** Ein dedizierter Bereich für die Root Cause Analysis.

In einer Live-Demo wurde gezeigt, wie das System von einer Schwellenwertüberschreitung bis hinunter zur SQL-Abfrage navigiert. Die KI identifizierte ein Feature-Flag als Auslöser und schlug sogar Code-Optimierungen vor.

## Session: Agentic AI im Troubleshooting

KI wird bei Grafana bei der User Interaktion für zwei Zwecke eingesetzt: **Troubleshooting** und **Informationsbeschaffung**. Cool ist die Fähigkeit der KI, Dashboards nicht nur auf Basis von Beschreibungen zu erstellen, sondern diese direkt aus den Ergebnissen einer Fehleruntersuchung zu generieren. Dadurch besitzen die Dashboards einen Kontext, den externe KI-Tools ohne direkten Datenzugriff nicht bieten können.

## Session: Reliability Culture mit IRM und SLOs

Zuverlässigkeit wurde als das wichtigste Produktfeature definiert. Da durch KI-Unterstützung immer mehr Code generiert wird, den Menschen potenziell weniger tief durchdringen (allein schon aufgrund der potenziellen Masse an Code), steigt die Gefahr von Incidents. 

Der Fokus lag hier auf dem **Incident Response Management (IRM)**. Die Integration direkt in die Observability-Plattform soll den Kontextwechsel minimieren. Ein wichtiger Aspekt war die Erkenntnis, dass eine gute Reliability-Kultur weniger auf Dashboards, sondern auf Prozessen wie Post-Incident Reviews und klaren Action-Items basiert

## Session: Adaptive Telemetry & Profiling

Hier wurde das Problem der Datenflut adressiert. **Adaptive Traces** behalten in der Cloud nur die "wertvollen" Traces, was Kosten und Speicher in der Grafana Cloud spart.

Ein weiterer Schwerpunkt war das **Profiling** mit Grafana Pyroscope. Dies ermöglicht "Code-level Granularity": Man kann direkt sehen, welche Zeile Code wie viel CPU-Zeit verbraucht. Während Traces im On-Premise-Bereich funktionieren, bleibt die intelligente Filterung (Adaptive Tracing) ein Cloud-Feature.

Für die intelligente Filterung von Date, setzt Grafana beim Fluss von Logs, Metrics, etc auf KI. Die KI lernt mit der Zeit, was relevant ist und was nicht.

## Praxisbericht: Erste Digital – Der Weg zur OpenTelemetry

Ein sEinblick in die regulierte Bankenwelt. Die Erste Digital nutzt ein Inhouse-Gateway, um Daten aus Legacy-Systemen zu harmonisieren, bevor sie in die Grafana Cloud fließen. Ansonsten hat die Session kaum neuen Infos zur Technik geliefert. 

**Key Takeaway:** Vorsicht bei der Label-Struktur! Zu viele Labels führen zur "Cardinality Hell" und beeinträchtigen die Performance von Loki massiv.

## Session: User Experience – Outside-In Monitoring

Mit Tools wie **Synthetic Monitoring**, **Frontend Observability** und **k6** simuliert Grafana die Nutzerperspektive. Besonders das **k6 Studio** stach hervor: Es erlaubt das Aufzeichnen von Interaktionen im Browser, um daraus JS-Testcases zu generieren. In der Cloud können diese Tests global von verschiedenen Regionen aus gestartet werden. Man kann also z.B.Zugriffe, wie sie ein User machen würde aus z.B. Indonesien testen und überwachen, ob die Antwortzeiten von dort such akzeptabel sind. 

## Fazit: Die Open-Source-Basis und die KI-Kluft

Die Konferenz hinterlässt ein zweigeteiltes Bild. Auf der einen Seite steht das Bekenntnis der Speaker, dass der Kern von Grafana Open Source bleibt und der Großteil der Features für alle Nutzer zugänglich ist. Das ist für On-Premise-Nutzer ein gutes Signal.

Auf der anderen Seite steht mein persönlicher Eindruck der gezeigten KI-Funktionen: Die Möglichkeiten der KI-Agenten – ob als interaktiver Assistent im Frontend oder als Automatik im Hintergrund – sind so mächtig, dass das Gefühl entsteht, die Grafana Cloud könne "viel mehr" als die Open-Source-Variante. Auch wenn dieser Eindruck trügerisch sein mag, wirlt die Geschwindigkeit und Tiefe der Analyse durch die KI wie ein enormer Vorteil. Da während des Events immer wieder betont wurde, dass diese KI-Features exklusiv der Cloud vorbehalten bleiben, entsteht hier für uns eineLücke. Für Unternehmen, die auf On-Premise-Lösungen angewiesen sind, bleibt die Hoffnung, dass die Effizienzgewinne der KI langfristig auch in den offenen Standard abfärben.
