<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicjowanie i formatowanie woluminu
1. Uruchom inicjatora iSCSI firmy Microsoft hello.
2. W hello **właściwości inicjatora iSCSI** okna na powitania **odnajdywania** , kliknij pozycję **odnajdź Portal**.
3. W hello **odnajdowanie portalu obiektu docelowego** okno dialogowe, podaj hello adres IP interfejsu sieci iSCSI, a następnie kliknij **OK**. 
4. W hello **właściwości inicjatora iSCSI** okna na powitania **celów** zlokalizuj hello **wykryte obiekty docelowe**. Stan urządzenia Hello powinny się wyświetlać jako **nieaktywne**.
5. Wybierz urządzenie docelowe hello, a następnie kliknij przycisk **Connect**. Po podłączeniu urządzenia hello hello stan powinien zmienić się zbyt**połączony**. (Aby uzyskać więcej informacji o korzystaniu z inicjatora iSCSI firmy Microsoft hello, zobacz [Instalowanie i konfigurowanie programu Microsoft iSCSI Initiator][1]).
6. Na hoście z systemem Windows, naciśnij klawisze Windows Logo hello + X, a następnie kliknij przycisk **Uruchom**. 
7. W hello **Uruchom** okno dialogowe, typ **Diskmgmt.msc**. Kliknij przycisk **OK**i hello **Zarządzanie dyskami** zostanie wyświetlone okno dialogowe. Witaj prawym okienku zostaną wyświetlone powitalne woluminy na hoście.
8. W hello **Zarządzanie dyskami** oknie hello zostaną wyświetlone zainstalowane woluminy pokazane na następującej ilustracji hello. Kliknij prawym przyciskiem myszy hello odnaleziony wolumin (kliknij nazwę dysku hello), a następnie kliknij przycisk **Online**.
   
     ![Inicjowanie i formatowanie woluminu](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Kliknij prawym przyciskiem myszy hello wolumin (kliknij nazwę dysku hello) ponownie, a następnie kliknij przycisk **zainicjować**.
10. tooformat wolumin prosty, wykonaj następujące kroki hello:
    
    1. Wybierz wolumin hello, kliknij go prawym przyciskiem myszy (kliknij prawy obszar hello) i kliknij przycisk **nowy wolumin prosty**.
    2. W Kreatorze nowego woluminu prostego powitania określ literę dysku i rozmiar woluminu hello i skonfigurować hello wolumin w systemie plików NTFS.
    3. Określ rozmiar jednostki alokacji 64 KB. Ten rozmiar jednostki alokacji dobrze działa z algorytmami deduplikacji hello używanymi w rozwiązaniu StorSimple hello.
    4. Przeprowadź szybkie formatowanie.

![Zobacz film](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób toomount, zainicjować i formatowanie woluminu StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
