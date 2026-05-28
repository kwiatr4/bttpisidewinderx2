# bttpisidewinderx2
Celem tego repo jest zainstalowanie klippera na drukarce a następnie stworzenia środowiska agentów, którzy sami wprowadzają zmiany w kliperze i tuningują drukarkę

## Czy Tailscale GitHub Action będzie OK do połączenia Gita z drukarką?
Tak — to jest dobre i bezpieczne podejście, jeśli workflow GitHub Actions ma łączyć się z hostem drukarki (np. Klipper/Moonraker) przez prywatną sieć Tailscale zamiast przez publiczny Internet.

Warunki, żeby to działało poprawnie:
- host drukarki musi być w tej samej sieci Tailscale (tailnet),
- w GitHub Actions trzeba dodać `tailscale/github-action@v4`,
- autoryzację trzymać w `GitHub Secrets` (OAuth client lub auth key),
- użyć tagów i ACL w Tailscale, aby ograniczyć dostęp tylko do potrzebnych zasobów.

Przykład kroku w workflow:

```yaml
- name: Tailscale
  uses: tailscale/github-action@v4
  with:
    oauth-client-id: ${{ secrets.TS_OAUTH_CLIENT_ID }}
    oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
    tags: tag:ci
```
