# Migratie-notities (deze twee regels)

## Wat er veranderd is

| Was (2024-stijl) | Nu (2026 VB.NET) |
| --- | --- |
| Impliciete variabelen (`oRevNum`, `PDFAddIn`, …) | Overal `Dim … As …` |
| `On Error Goto` / labels | `Try` / `Catch` |
| `Goto` + `Exit Sub` | `Return` / gestructureerde flow |
| `vbNo` (uitgecommentarieerd) | `DialogResult.No` |
| `ItemById(...)` zonder cast | `DirectCast(..., TranslatorAddIn)` |
| PDF: `HasSaveCopyAsOptions(oDataMedium, …)` | `HasSaveCopyAsOptions(oDocument, …)` (bugfix) |

## Wat hetzelfde blijft

- Extensie `.iLogicVb` (standaard iLogic-regel, geen Straight VB)
- Helpers: `ThisApplication`, `ThisDoc`, `iProperties`, `MessageBox`
- DXF/PDF translator-GUID’s
- Bestandsnaam: `PathAndFileName` + `_` + revisie + extensie
- INI-pad: `C:\temp\dxfout.ini`

## In Inventor 2026

1. Kopieer de bestanden uit `2026/` naar je externe-rules-map, of plak de inhoud in een bestaande regel.
2. **Sla de tekening eerst op.** Op een nieuw `Drawing1` zonder pad faalt `SaveCopyAs` met `E_INVALIDARG`.
3. INI is optioneel: als `C:\temp\dxfout.ini` ontbreekt, zoekt de regel de standaard `exportdxf.ini` onder Inventor Design Data; anders exporteert hij zonder INI.
4. Test DXF en PDF op een schone 2026-installatie.

## Veelgemaakte fout: `E_INVALIDARG` op `SaveCopyAs`

Meestal één van deze oorzaken:

- tekening niet opgeslagen (`Drawing1`) → geen geldig uitvoerpad
- `Export_Acad_IniFile` wijst naar een INI die niet bestaat
- verkeerde INI (bijv. Design Data `exportdxf.ini` = plaatwerk/flat pattern, niet tekening-export)

Huidige regels proberen eerst `ThisDoc.Document.SaveAs(... .dxf, True)`.
Pas daarna de translator. INI alleen als `C:\temp\dxfout.ini` bestaat
(aanmaken via Save Copy As → DXF → Options → Save Configuration).
