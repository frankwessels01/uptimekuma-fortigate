# Uptime Kuma FortiGate

Aangeleverde FortiGate Automation-configuraties voor pushmeldingen naar Uptime Kuma.

## Bestanden

| Bestand | Inhoud |
| --- | --- |
| `execute batch start.txt` | Webhook-actions binnen een batch, voor heartbeat, CPU, geheugen, administratoraanmaak en interfacestatus |
| `config system automation-trigger.txt` | Event-triggers voor CPU, geheugen, administratoraanmaak en interfaces |
| `config system automation-stitch.txt` | Koppelingen tussen triggers en actions |

## Voorbereiding

De oorspronkelijke servernaam en push-token zijn vóór publicatie vervangen door `kuma.example.com` en `REPLACE_WITH_PUSH_TOKEN`. Vul deze lokaal in met de hostname en token uit je Uptime Kuma pushmonitor. Publiceer ingevulde tokens niet in GitHub.

Controleer de interfaces (`lan1`, `lan2`, `lan3` en `a`) en pas deze aan je FortiGate aan. Controleer de configuratie tegen de FortiOS-versie op je apparaat. Er is geen test op een FortiGate uitgevoerd.

## Importvolgorde en ontbrekende configuratie

1. Actions uit `execute batch start.txt`.
2. Event-triggers uit `config system automation-trigger.txt`.
3. Ontbrekende heartbeat-triggers aanmaken.
4. Stitches uit `config system automation-stitch.txt`.

De stitches verwijzen naar zes heartbeat-triggers die niet in de aangeleverde triggerconfiguratie staan: `Kuma-HB-00`, `Kuma-HB-10`, `Kuma-HB-20`, `Kuma-HB-30`, `Kuma-HB-40` en `Kuma-HB-50`. Maak deze aan met het bedoelde schema voordat je de heartbeat-stitches toepast.

Alle actions gebruiken dezelfde pushmonitor. Een `up`-melding kan daardoor een eerdere `down`-melding van een andere action overschrijven. Houd hiermee rekening bij de monitorindeling en het heartbeat-interval.

De configuratie is overgenomen met alleen de vervanging van hostname en token; de ontbrekende triggers zijn niet toegevoegd.

## Uptime Kuma-server

De native installatie- en onderhoudsscripts staan in [uptimekuma-cyberframe](https://github.com/frankwessels01/uptimekuma-cyberframe).
