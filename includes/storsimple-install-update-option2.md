<!--author=SharS last changed: 03/17/2016-->

#### <a name="tooinstall-update-12-from-hello-azure-classic-portal"></a>tooinstall 1.2 aktualizacji z hello klasycznego portalu Azure
1. W hello klasycznego portalu Azure, przejdź do pozycji toohello **urządzeń** i wybrać opcję urządzenia.
2. Przejdź za**urządzeń** > **Konfiguruj**.
3. W obszarze **interfejsów sieciowych**, najpierw należy sprawdzić, czy co najmniej jeden interfejs sieciowy, który ma włączoną obsługę interfejsu iSCSI. Następnie odszukaj interfejsu sieciowego hello (inne niż dane 0), który ma przypisane bramę.
4. Wyłącz hello interfejsu sieciowego, który ma przypisane bramy i zapisać konfigurację zmodyfikowane hello. Ustawienia interfejsu sieciowego hello Uwaga zostaną zachowane, więc po ponownym włączeniu ten interfejs sieciowy później, hello portal spowoduje przywrócenie toohello pierwotne ustawienia.
5. Możesz teraz [Użyj klasycznego portalu Azure tooinstall 1.2 aktualizacji hello](#install-update-12-via-the-azure-classic-portal). Wykonaj instrukcje hello, zaczynając od kroku 3 tej procedury. Po zainstalowaniu wszystkich aktualizacji hello można ponownie włączyć hello interfejsu sieciowego, które zostały wyłączone.

