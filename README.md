# 🌟 Tähtipolku

Lasten hyvien tekojen palkintotaulu — taikametsän seikkailu.

Tähtipolku on ilmainen, avoin web-sovellus perheille. Sovellus auttaa palkitsemaan lapsia hyvistä teoista kerättävillä tähdillä, ja kun tähtiä on tarpeeksi, aukenee pieniä palkintoja. Koko sovellus toimii suomeksi, ilman tilejä, ilman mainoksia, ilman pilvipalveluita — kaikki tieto tallentuu omaan laitteeseen.

![Tähtipolku](./icon-512.png)

## ✨ Ominaisuudet

- **Alustus omalle perheelle**: lisää 1–6 lasta, anna nimet, valitse jokaiselle rooli metsässä (Ketturitari, Perhoskeijutar, Karhuseikkailija, Lohikäärmesankari ym. — 14 vaihtoehtoa)
- **Muokattavat tehtävät**: määritä omat hyvät teot ja niistä saatavat tähdet (1–3 / teko)
- **3-portainen palkintojärjestelmä**: 10 ⭐ Tikkari, 25 ⭐ Jäätelö, 50 ⭐ HopLop tai elokuvat
- **Taikametsän tarina**: Kuutontut, Tähtipuut ja Taikametsän Kuningatar
- **Juhlat**: konfetti ja soiva fanfaari kun palkintoraja ylittyy
- **Äänimaailma**: kevyt klik-ääni teoista, pehmeä peruutus, riemukas melodia rajapyykeistä
- **Toimii offline**: kerran ladattuna sovellus toimii ilman nettiyhteyttä
- **Asennettavissa kotivalikkoon**: iPhonella, iPadilla ja Androidilla "Lisää aloitusnäyttöön" tekee siitä oikean näköisen appisin

## 🚀 Käyttö

1. Avaa sivu selaimessa: `https://<käyttäjänimesi>.github.io/tahtipolku/`
2. Täytä onboarding (seikkailijat ja tehtävät)
3. iPadilla tai puhelimella: lisää kotivalikkoon ("Share → Add to Home Screen")
4. Kerätkää tähtiä yhdessä!

Kaikki data tallentuu vain laitteen selaimen localStorageen — mikään ei lähde verkkoon.

## 🛠 Tekniikka

- Vanilla HTML/CSS/JavaScript — ei rakennusvaiheita, ei riippuvuuksia
- Web Audio API äänille (ei audiotiedostoja)
- Service Worker offline-tukeen
- PWA manifest kotivalikko-asennukseen
- localStorage tallennukseen

## 📁 Tiedostot

```
index.html                  — pääsovellus
manifest.json               — PWA-manifesti
sw.js                       — service worker (offline-tuki)
icon-192.png                — ikoni
icon-512.png                — ikoni (iso)
icon-512-maskable.png       — maskable ikoni Androidille
```

## 📜 Lisenssi

MIT — vapaasti käytettävissä, muokattavissa ja jaettavissa.

---

Rakennettu rakkaudella Turussa ✨
