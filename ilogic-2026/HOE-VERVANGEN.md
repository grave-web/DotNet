# Waarom je nog `SaveCopyAs` / regel 40 ziet

Op GitHub staat `saveDXF.iLogicVb` **zonder** `TranslatorAddIn.SaveCopyAs`.
Regel 40 daar is alleen een MessageBox-argument.

Als Inventor toch meldt:

```text
TranslatorAddIn.SaveCopyAs ... ThisRule.Main() ... line 40
```

dan draait **niet** dat GitHub-bestand. Meestal is dit een **interne rule**
met dezelfde naam `saveDXF` die in `Drawing1.dwg` zelf zit.

## Doe dit

1. Pull in GitHub Desktop: repo `grave-web/DotNet`
2. Draai **niet** `saveDXF`, maar de nieuwe rule: **`SAVE_DXF_2026`**
3. In de iLogic Browser:
   - onder het document (Drawing1) → dat zijn **interne** rules
   - onder **External Rules** → dat zijn de bestanden uit je map
4. Rechtsklik **External Rules → SAVE_DXF_2026 → Run Rule**
5. Je moet eerst zien: `Dit IS SAVE_DXF_2026 (externe rule).`

Zie je die melding niet → je start nog een andere rule (vaak de interne `saveDXF`).

Optioneel: open de interne rule `saveDXF` in Drawing1 en verwijder/hernoem die,
of plak daar de nieuwe code in.
