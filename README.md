# bttpisidewinderx2
Celem tego repo jest zainstalowanie klippera na drukarce a następnie stworzenia środowiska agentów, którzy sami wprowadzają zmiany w kliperze i tuningują drukarkę

## Tailscale GitHub Action - czy to się nada?

Tak, do tego celu to dobre podejście: akcja Tailscale pozwala bezpiecznie połączyć runner GitHub Actions z Twoim tailnetem, więc workflow może dostać dostęp do hosta z Klipperem bez wystawiania usług do publicznego internetu.

Najważniejsze warunki:
- dodać sekrety `TAILSCALE_OAUTH_CLIENT_ID` i `TAILSCALE_OAUTH_SECRET` w repo,
- mieć skonfigurowane ACL/tagi w Tailscale dla tego typu dostępu,
- najlepiej uruchamiać tuning na `self-hosted` runnerze (stabilniejszy dostęp do drukarki i mniejsze ryzyko timeoutów).

Poniżej jest minimalny workflow do ręcznego sprawdzenia połączenia przez Tailscale.
