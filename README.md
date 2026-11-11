# Le sirene nelle principali città ucraine: grafico da incorporare

| File | Che cosa contiene |
|---|---|
| `dashboard.html` | Il grafico: menu delle sei città, numeri del mese, timeline 10 ottobre – 10 novembre 2026, confronto tra città |
| `index.html` | Pagina di prova che incorpora il grafico come farebbe il sito |
| `dati.json` | I dati usati dal grafico (dati aperti; il grafico ha gli stessi dati già al suo interno) |

La pagina non usa librerie esterne. L'unica risorsa esterna sono i font Archivo Narrow e Source Sans 3 di Google Fonts.

## 1. Pubblicare su GitHub Pages

1. Su github.com crea un nuovo repository (**New**), per esempio `sirene-ucraina`, impostalo **Public** e crealo.
2. **Add file → Upload files**, trascina i file di questa cartella e conferma con **Commit changes**.
3. **Settings → Pages**: **Deploy from a branch**, branch **main**, cartella **/ (root)**, **Save**.
4. Dopo uno o due minuti il grafico è online:
   - `https://cosimofire.github.io/sirene-ucraina/dashboard.html`
   - `https://cosimofire.github.io/sirene-ucraina/` (pagina di prova)

Per aggiornare il grafico basta ricaricare `dashboard.html` su GitHub: la versione online si aggiorna in circa un minuto, anche negli articoli dove è già incorporato.

## 2. Incorporare nell'articolo

Nel CMS inserisci un blocco HTML con questo codice:

```html
<iframe src="https://cosimofire.github.io/sirene-ucraina/dashboard.html"
        title="Le sirene nelle principali città ucraine nell'ultimo mese"
        style="width:100%;border:0;height:1650px" scrolling="no"></iframe>
```

Per aprire il grafico già su una città, aggiungi il suo nome dopo `#` nell'indirizzo: `dashboard.html#kharkiv`, `#dnipro`, `#zaporizhzhia`, `#odessa`, `#leopoli` (senza nulla si apre Kyiv).

### Altezza automatica

Il grafico comunica la propria altezza alla pagina che lo ospita. Per usarla aggiungi **una sola volta** nella pagina questo script (è lo stesso del golden power: se è già nel template del sito non serve ripeterlo):

```html
<script>
window.addEventListener('message', function (e) {
  if (e.origin !== 'https://cosimofire.github.io') return;
  if (!e.data || !e.data.gpEmbed || !e.data.height) return;
  document.querySelectorAll('iframe').forEach(function (f) {
    if (f.contentWindow === e.source) f.style.height = e.data.height + 'px';
  });
});
</script>
```

Se il CMS non permette script, l'iframe funziona con l'altezza fissa indicata sopra; in quel caso conviene `scrolling="auto"`.

## 3. Note

- **Fonte dei dati:** alerts.in.ua, vista "Alerts History", 10 ottobre – 10 novembre 2026. Metodo e correzioni nel file LEGGIMI.md del lavoro di raccolta dati.
- **Privacy:** i font vengono caricati dai server di Google. Se la policy del giornale lo vieta, si possono caricare i file dei font nel repository e togliere il link a `fonts.googleapis.com`.
