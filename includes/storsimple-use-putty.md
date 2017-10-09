<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect za pośrednictwem konsoli szeregowej hello
1. Podłącz kabel szeregowy urządzenie toohello, (bezpośrednio lub za pośrednictwem adaptera szeregowego USB).
2. Otwórz hello **Panelu sterowania**, a następnie otwórz hello **Menedżera urządzeń**.
3. Zidentyfikuj port hello COM pokazane na następującej ilustracji hello.
   
     ![Łączenie za pośrednictwem konsoli szeregowej](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Uruchom program PuTTY. 
5. W okienku po prawej stronie powitania, zmień hello **typ połączenia** za**Serial**.
6. W okienku po prawej stronie powitania wpisz odpowiedni port COM. hello. Upewnij się, że parametry konfiguracji portu hello są ustawione w następujący sposób:
   
   * Szybkość: 115 200
   * Bity danych: 8
   * Bity stopu: 1
   * Parzystość: Brak
   * Sterowanie przepływem: Brak
     
     Te ustawienia zostały pokazane hello następującej ilustracji.
     
     ![Ustawienia programu PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Jeśli hello domyślne ustawienie sterowania przepływem nie działa, spróbuj hello przepływu sterowania tooXON/XOFF.
     > 
     > 
7. Kliknij przycisk **Otwórz** toostart sesję serial.

