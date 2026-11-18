# Układ okna – Grid, StackPanel, marginesy

## Grid – siatka wierszy i kolumn
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="200"/>
    </Grid.ColumnDefinitions>

    <DataGrid Grid.Row="0" Grid.Column="0" />
    <Button   Grid.Row="1" Grid.ColumnSpan="2">Dodaj</Button>
</Grid>
```

### Rozmiar wiersza / kolumny
| Wartość | Znaczenie |
|---|---|
| `Auto` | dokładnie tyle, ile potrzebuje zawartość (np. wysokość przycisku) |
| `*` | **całe pozostałe** wolne miejsce; rośnie razem z oknem |
| `2*` | dwa razy więcej wolnego miejsca niż `*` (proporcje) |
| `200` | stała wartość w pikselach (niezależnych od rozdzielczości) |

Typowy układ: pasek przycisków `Auto`, a główna treść `*` – przy powiększaniu okna rośnie tylko treść.

### Położenie w siatce
- `Grid.Row="1"`, `Grid.Column="0"` – numeracja **od 0**; brak atrybutu = 0.
- `Grid.ColumnSpan="2"` – element zajmuje **2 kolumny**, zaczynając od swojej `Grid.Column`. Analogicznie `Grid.RowSpan`.

```xml
<Button Name="addProduct" Grid.Row="1" Click="Add" Grid.ColumnSpan="2">Dodaj</Button>
<!-- przycisk w drugim wierszu, rozciągnięty na kolumny 0 i 1 -->
```

## StackPanel – elementy jeden za drugim
```xml
<StackPanel Orientation="Horizontal">
    <TextBlock Text="Lokalizacja" FontWeight="Bold"/>
    <ComboBox x:Name="lokalizacja" Width="100"/>
</StackPanel>
```
- `Orientation="Horizontal"` – elementy **obok siebie, od lewej do prawej**: napis „Lokalizacja”, a za nim lista rozwijana.
- `Orientation="Vertical"` (domyślnie) – elementy **jeden pod drugim**.
- StackPanel nie zawija – elementy, które się nie mieszczą, są obcinane. Do zawijania służy `WrapPanel`.

## Margin i wyrównanie
```xml
<Button Content="Kliknij mnie" HorizontalAlignment="Left" VerticalAlignment="Top"
        Margin="331,317,0,0" Width="112" Height="70" Click="Przycisk_Click"/>
```
`Margin="lewy,górny,prawy,dolny"`. Taki kod generuje designer Visual Studio po przeciągnięciu kontrolki myszą.

Po **powiększeniu okna** przycisk **zostaje w tym samym miejscu** – 331 px od lewej i 317 px od góry – i ma ten sam rozmiar. Wolne miejsce pojawia się po prawej i na dole. Po **zmniejszeniu** okna przycisk może zostać obcięty lub zniknąć.

| Ustawienie | Zachowanie przy zmianie rozmiaru okna |
|---|---|
| `Left`/`Top` + duży `Margin` | stała pozycja od lewego górnego rogu |
| `Right`/`Bottom` | przyklejony do prawej / dolnej krawędzi |
| `Center` | zawsze na środku |
| `Stretch` (domyślne, bez `Width`/`Height`) | rozciąga się razem z komórką |

> Zamiast dużych marginesów lepiej układać okno siatką `Grid` z wierszami `Auto`/`*` – wtedy dopasowuje się do rozmiaru.

## Pytania kontrolne
1. Czym różni się wiersz o wysokości `Auto` od wiersza `*`?
2. Co oznacza `Grid.ColumnSpan="2"`?
3. Jak zostaną ułożone elementy w `StackPanel` z `Orientation="Horizontal"`?
4. Co stanie się z położeniem przycisku z `Margin="331,317,0,0"` po powiększeniu okna?
