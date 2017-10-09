### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Udziel dostępu tooyour tooMobile certyfikatu wypychania zaangażowania
tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy uzyskać dostępu do certyfikatu tooyour toogrant. Jest to zrobić, konfigurując i wprowadzić certyfikat w portalu Mobile Engagement hello. Upewnij się, że dysponujesz certyfikatem p12, zgodnie z objaśnieniem w [dokumentacji firmy Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6).

1. Przejdź tooyour portalu Mobile Engagement. Upewnij się, zalogowanie hello poprawne, a następnie kliknij polecenie hello **Engage** u dołu hello:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Polecenie hello **ustawienia** strony w portalu usługi Engagement. Kliknij hello **natywnych powiadomień wypychanych** sekcji tooupload certyfikat p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Wybierz certyfikat p12, prześlij go i wpisz hasło:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Wyślij aplikacji tooyour powiadomień
Teraz utworzymy prostą kampanię powiadomień wypychanych, która będzie wysyłać aplikacji tooour wypychania:

1. Przejdź toohello **osiągnąć** kartę w portalu usługi Mobile Engagement.
2. Kliknij przycisk **nowy anons** toocreate kampanii wypychania
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Konfiguracja hello pierwsze pola kampanii:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Podaj nazwę kampanii w polu **Name** (Nazwa). 
   * Wybierz hello **czas dostawy** jako **tylko poza aplikacją**: jest to hello Apple push powiadomień typu prostego, który zawiera krótki tekst.
   * W tekście powiadomienia hello, wpisz pierwszy hello **tytuł** który będzie stanowić pierwszy wiersz hello hello wypychania.
   * Następnie wpisz Twojej **komunikat** który będzie stanowić drugi wiersz hello
4. Przewiń w dół i w hello sekcji zawartości wybierz **tylko powiadomienie**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Wszystko gotowe ustawienie hello najbardziej podstawowej kampanii. Teraz przewiń w dół i wybierz polecenie **Utwórz** przycisk toosave kampanię powiadomień wypychanych. 
6. Na koniec — kliknij pozycję **Aktywuj** toosend powiadomień wypychanych. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Można otrzymywać powiadomienia hello na urządzeniu z systemem iOS w Centrum powiadomień hello podobnie następującej hello:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Jeśli masz Apple Watch łączyć się z tego urządzenia z systemem iOS zostanie wyświetlony hello powiadomienie na Twoje Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

