# gssh

Launcher SSH w terminalu z widokiem katalogowym: grupy hostów to foldery, hosty bez grupy leżą obok nich. Wchodzisz w grupę, wpisujesz kawałek nazwy, Enter i jesteś na maszynie.

Czyta plik hostów [goto](https://github.com/grafviktor/goto) (`~/.config/goto/hosts.yaml`), więc oba narzędzia działają na tych samych danych. Samo goto nie jest potrzebne.

## Wymagania

- bash
- python3 z PyYAML (`python3-yaml`)
- fzf 0.53 lub nowszy
- ssh

## Instalacja

```bash
curl -fsSLo ~/.local/bin/gssh https://raw.githubusercontent.com/pbabilas/gssh/main/gssh
chmod +x ~/.local/bin/gssh
```

`~/.local/bin` musi być w `PATH`.

## Klawisze

| Klawisz | Działanie |
|---------|-----------|
| pisanie | filtrowanie listy |
| Enter | wejście do grupy albo połączenie z hostem |
| → | wejście do grupy |
| ← (przy pustym filtrze), Esc | poziom wyżej; Esc na górze zamyka |
| Ctrl-N | nowy host w bieżącej grupie |

## Pliki

`~/.config/goto/hosts.yaml` (zmienna `GSSH_HOSTS`), format goto z polem `group`. Zagnieżdżenie przez `/`:

```yaml
- host:
    address: 198.51.100.11
    description: Worker k8s prod
    username: root
    network_port: '2222'
    title: node-01
    group: work/k8s-prod
```

Puste `username` i `network_port` nie trafiają do wywołania ssh, więc obowiązuje `~/.ssh/config`.

`~/.config/gssh/groups.yaml` (zmienna `GSSH_GROUPS`), opcjonalne podpisy grup wyświetlane pod nazwą folderu:

```yaml
work/k8s-prod: Klaster Kubernetes prod, workery
```

Przykłady są w `examples/`. Szybki podgląd bez ruszania własnej konfiguracji:

```bash
GSSH_HOSTS=examples/hosts.yaml GSSH_GROUPS=examples/groups.yaml ./gssh
```

## Licencja

MIT
