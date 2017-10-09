> [!IMPORTANT]
> tooreceive powiadomienia wypychane z usługi Mobile Engagement należy tooenable `Silent Remote Notifications` w aplikacji. Należy tablicy UIBackgroundModes toohello tooadd hello wartość remote-notification w pliku Info.plist.
> 
> 

1. Otwórz `info.plist` plik w projekcie hello
2. Kliknij prawym przyciskiem myszy pierwszy element listy hello hello (`Information Property List`) i Dodaj nowy wiersz
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. W hello wprowadź nowy wiersz`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Polecenie hello strzałki w lewo tooexpand hello wiersza
5. Dodaj hello elementem toohello wartość 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Po wprowadzeniu zmiany hello info.plist hello XML powinien zawierać powitania po klucz i wartość:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Jeśli używasz programu **Xcode 7 +** i systemu **iOS 9 +**:
   
   * Włącz funkcję **Push Notifications** (Powiadomienia wypychane), wybierając kolejno opcje Targets (Obiekty docelowe ) > Your Target Name (Nazwa obiektu docelowego) > Capabilities (Funkcje).

