# Price Bailey UK office map

A single self-contained page (`index.html`) showing the Price Bailey UK offices. It is built to be published on GitHub Pages and embedded by iframe on each location page.

## Publish on GitHub Pages

1. Create a repository, for example `pb-office-map`, and upload `index.html` and this README to the root.
2. Go to Settings > Pages. Under "Build and deployment", set Source to "Deploy from a branch", choose `main` and `/ (root)`, then save.
3. After a minute the map is live at `https://<your-account>.github.io/pb-office-map/`.

## Embed on a location page

Change `office=` to match the page. That office shows as "You are here".

```html
<iframe id="pb-office-map"
  src="https://<your-account>.github.io/pb-office-map/?office=chelmsford"
  title="Price Bailey UK office map"
  style="width:100%;height:760px;border:0;display:block"
  loading="lazy"></iframe>
<script>
  // Optional: resizes the iframe to fit (mainly for mobile, where the office list stacks under the map)
  window.addEventListener('message', function (e) {
    if (e.data && e.data.type === 'pb-office-map:height') {
      document.getElementById('pb-office-map').style.height = e.data.height + 'px';
    }
  });
</script>
```

Office codes: `bishops-stortford`, `cambridge`, `chelmsford`, `great-yarmouth`, `city-of-london`, `mayfair`, `newmarket`, `norwich`, `oxford`, `peterborough`, `sawston`.
Leave `?office=` off for a general version, for example on the main locations page.

## Edit office details

Open `index.html` on GitHub, click the pencil icon and search for `const CONFIG`. Each office is a block like this:

```js
{
  "id": "chelmsford",
  "name": "Chelmsford",
  "address": "Elizabeth House, 28 Baddow Road, Chelmsford, Essex, CM2 0DG",
  "phone": "01245 202613",
  "specialisms": ["Corporate finance", "Audit & assurance", "Private client"],
  "hours": "Monday to Friday, 9am to 5:30pm",
  ...
}
```

- Phone: enter as `01245 202613`. The map shows it as `+44 (0)1245 202613`.
- Specialisms: leave as `[]` to show "Full range of Price Bailey services".
- Hours: leave out to use `defaultHours` at the top of the block.
- Commit the change. GitHub Pages updates within a minute or two.

Do not move an office's `lat` or `lng` here. Pin positions are fixed when the file is built, so a new office or a moved office needs a rebuild (ask the person who maintains the map).

Brand colours and font are the `:root` values at the top of the `<style>` block.

## Before go-live

- [ ] Sawston: add its address and phone, or ask for it to be removed.
- [ ] Opening hours: all offices use `defaultHours`; confirmed for Chelmsford only.
- [ ] Specialisms: only Chelmsford has them so far.
- [ ] Teal: `--pb-teal` (#1fa6a0) is an estimate. Swap in the exact brand hex.
- [ ] Confirm the Volte font is licensed for web use on github.io; otherwise the map uses Figtree.

Map data: Natural Earth (public domain).
