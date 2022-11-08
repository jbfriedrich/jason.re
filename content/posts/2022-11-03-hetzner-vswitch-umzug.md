---
title: Kein IP-Umzug auf Hetzner vSwitches
slug: hetzner-vswitches-ipnetz
feature_image: "https://images.unsplash.com/photo-1558494949-ef010cbdcc31?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2834&q=80"
date: 2022-11-03T17:20:00
tags:
  - tech
  - network
  - customer-service
  - de
---

Ich bin gerade ein wenig von [Hetzner](https://www.hetzner.de) enttäuscht. Ich bin sehr lange Kunde dort, und hatte über die Jahre bereits etliche Root Server und VPS. Eigentlich war ich immer recht zufrieden. Nun habe ich seit ein oder zwei Jahren wieder einen Root Server gemietet, dazu ein "/64" IPv6-Netz und ein "/29" IPv4-Netz.

Ich nutze den Server mit VMware vSphere und betreibe eine funktionierende, dennoch ein bisschen unschöne Router-VM Lösung, die ich gerne abschaffen würde. Ein [Hetzner vSwitch](https://docs.hetzner.com/de/robot/dedicated-server/network/vswitch/) wäre dafür eigentlich ideal! In der UI wird mir nur angeboten das ich neue IPv4- und IPv6-Netze für den vSwitch bestellen kann. Leider gibt es nirgendwo die Möglichkeit IP-Adressen oder Netze zu migrieren, oder in irgendeiner Weise zu importieren – schließlich habe ich ja schon zwei Netze. 

![Hetzner vSwitch IP Preise](https://cloud.rmbr.eu/file/dstore/vswitch-preise.png)

Nachdem Hetzner die monatliche Gebühr verdoppelt, und den Bereitstellungspreis für IPv4-Adressen und -Netze drastisch erhöht hat, würde ich ungern nur für einen Umzug auf den vSwitch den Bereitstellungspreis noch einmal bezahlen. Vielleicht gibt es dort ja ein Entgegenkommen, eventuell eine Gutschrift oder eine Anrechnung auf den Preis, oder so etwas. 

Einen Telefonanruf später bin ich sehr ernüchtert. Klare Aussage vom Support: "Geht leider nicht – wurde von der Geschäftsleitung so entschieden". Ich müsste meine Netze kündigen und dann neue Netze für den vSwitch beantragen. Kostenpunkt: einmalig 180 € und dann monatlich 27 € statt 17 € für das "/29" IPv4-Netz 😞. Die monatlichen Kosten würden sich schnell amortisieren, schließlich kann die die IPv4 Adresse der Router-VM abbestellen. Aber die Bereitstellungskosten sind zu hoch. Ich glaube das ist es mir nicht wert.

### Update Nov 7 2022

Ich habe noch einmal den Hetzner Support via Email kontaktiert und die Situation geschildert. Herr S. aus der Hetzner Sales Abteilung schrieb mir, das die Setup Gebühr aus Kulanz erlassen wird. Ich soll ganz normal bestellen und werde dann eine Gutschrift erhalten. Chapeau Hetzner, guter Kundenservice. Vielen Dank dafür!
