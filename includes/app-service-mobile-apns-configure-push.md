

1. Na komputerze Mac Uruchom **dostęp łańcucha kluczy**. Na powitania po lewej paska nawigacji w obszarze **kategorii**, otwórz **moje certyfikaty**. Znajdź certyfikat SSL hello pobranego w poprzedniej sekcji hello i ujawniać jego zawartość. Wybierz tylko hello certyfikatu (nie zaznaczaj hello klucz prywatny), a [wyeksportować go](https://support.apple.com/kb/PH20122?locale=en_US).
2. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **Przeglądaj wszystko** > **usługi aplikacji**i kliknij przycisk z zaplecza aplikacji mobilnej. W obszarze **ustawienia**, kliknij przycisk **aplikacji usługi wypychania**, a następnie kliknij nazwę Centrum powiadomień. Przejdź za**Apple Push Notification Services** > **Przekaż certyfikat**. Przekaż plik .p12 hello, wybierając hello poprawne **tryb** (w zależności od tego, czy certyfikat SSL klienta od wcześniej to środowisko produkcyjne lub piaskownicy). Zapisz zmiany.

Usługa jest teraz skonfigurowany toowork z powiadomień wypychanych w systemie iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
