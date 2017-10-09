### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Udziel Mobile Engagement tooyour dostępu do klucza interfejsu API usługi GCM
tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy mieć do niej dostęp tooyour klucz interfejsu API toogrant. Jest to zrobić, konfigurując i wprowadzić klucz w portalu Mobile Engagement hello.

1. W klasycznym portalu Azure, upewnij się, pracy w aplikacji hello możemy jest używany dla tego projektu, a następnie kliknij przycisk hello **Engage** u dołu hello:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Następnie kliknij przycisk hello **ustawienia** -> **natywnych powiadomień wypychanych** sekcji tooenter klucz GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Kliknij przycisk hello **Edytuj** ikona przed **klucz interfejsu API** w hello **ustawienia GCM** sekcji, jak pokazano poniżej:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. W oknie podręcznym hello wklej uzyskany wcześniej klucz serwera GCM Server hello, a następnie kliknij przycisk **Ok**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Wyślij aplikacji tooyour powiadomień
Teraz utworzymy kampanii powiadomień wypychanych proste wysyłanej aplikacji tooour powiadomień wypychanych.

1. Przejdź toohello **OSIĄGNĄĆ** kartę w portalu usługi Mobile Engagement.
2. Kliknij przycisk **nowy anons** toocreate kampanię powiadomień wypychanych.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Skonfiguruj hello pierwsze pole kampanii hello następujące kroki:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Nadaj nazwę kampanii.
   
    b. Wybierz hello **typ dostawy** jako *powiadomienie systemowe -> Simple*: to hello prostego systemu Android wypychania powiadomień typ, który zawiera tytuł i krótki wiersz tekstu.
   
    c. Wybierz **czas dostawy** jako *Powi№zanych* tooallow hello tooreceive aplikacji powiadomienie, czy aplikacja hello jest uruchomiona lub nie.
   
    d. W hello powiadomień tekst typu hello **tytuł** której będą znajdować się w pogrubioną hello wypychania.
   
    e. Następnie wpisz komunikat w polu **Message** (Komunikat).
4. Przewiń w dół i w hello **zawartości** zaznacz **tylko powiadomienie**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Ustawienie hello najprostsze kampanii możliwe jest gotowe. Teraz przewiń ponownie w dół i kliknij przycisk hello **Utwórz** przycisk toosave kampanii.
6. Ostatni krok: kliknij **Aktywuj** tooactivate toosend kampanię powiadomień wypychanych.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

