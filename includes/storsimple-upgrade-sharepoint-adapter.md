<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Uaktualnienie programu SharePoint 2010 tooSharePoint 2013, a następnie zainstaluj hello karty StorSomple dla programu SharePoint
> [!IMPORTANT]
> Wszystkie pliki, które wcześniej zostały przeniesione tooexternal magazynu za pośrednictwem SPZ nie będą dostępne dopiero po zakończeniu uaktualniania hello i hello SPZ funkcji ponownego włączenia. Użytkownik toolimit wpływ, wszelkie uaktualnienia lub ponownej instalacji w oknie zaplanowanej konserwacji.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade programu SharePoint 2010, 2013, a następnie zainstaluj hello karty
1. W farmie programu SharePoint 2010 hello Uwaga hello obiektu BLOB magazynu ścieżkę hello externalized obiekty BLOB i bazy danych zawartości hello, dla których włączono SPZ. 
2. Instalowanie i konfigurowanie hello nowej farmy programu SharePoint 2013. 
3. Przenoszenie baz danych, aplikacji i zbiory witryn z hello programu SharePoint 2010 farmy toohello nowej farmy SharePoint 2013. Aby uzyskać instrukcje, przejdź zbyt[omówienie tooSharePoint procesu uaktualniania hello 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Zainstaluj hello karty StorSimple dla programu SharePoint na powitania nowej farmy. Przejdź za[hello instalacji karty StorSimple dla programu SharePoint](#install-the-storsimple-adapter-for-sharepoint) procedury.
5. Przy użyciu informacji hello zanotowaną w kroku 1, Włącz SPZ hello sam zestaw baz danych zawartości i podaj hello tego samego obiektu BLOB zapisać ścieżki, która została użyta w instalacji hello programu SharePoint 2010. Przejdź za[skonfigurować SPZ](#configure-rbs) procedury. Po wykonaniu tego kroku pliki wcześniej externalized powinien być dostępny hello nowej farmy. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Uaktualnij hello karty StorSimple dla programu SharePoint
> [!IMPORTANT]
> Należy zaplanować tego uaktualnienia toooccur podczas okna zaplanowanej konserwacji dla hello z następujących powodów:
> 
> * Wcześniej externalized zawartość nie będzie dostępne, dopóki nie zostanie ponownie zainstalowana hello karty.
> * Zawartość przekazać toohello lokacji po odinstalować poprzednią wersję hello hello karty StorSimple dla programu SharePoint, ale przed zainstalowaniem nowej wersji hello będą przechowywane w bazie danych zawartości hello. Konieczne będzie toomove urządzenia StorSimple toohello zawartości po zainstalowaniu nowej karty hello. Można użyć programu Microsoft hello` RBS Migrate()` dołączone do zawartości programu SharePoint toomigrate hello polecenia cmdlet programu PowerShell. Aby uzyskać więcej informacji, zobacz [migrowania zawartości do lub wychodzący SPZ](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>Witaj tooupgrade karty StorSimple dla programu SharePoint
1. Odinstaluj poprzednią wersję hello karty StorSimple dla programu SharePoint.
   
   > [!NOTE]
   > SPZ zostanie automatycznie wyłączony na powitania baz danych zawartości. Jednak pozostanie istniejące obiekty BLOB na urządzeniu StorSimple hello. Ponieważ SPZ jest wyłączona, a obiekty BLOB hello nie zostały jeszcze zmigrowane toohello wstecz baz danych zawartości, wszystkie żądania dla tych obiektów blob nie powiedzie się. 
   > 
   > 
2. Zainstaluj hello nową kartę StorSimple dla programu SharePoint. Nowa karta Hello będzie automatycznie rozpoznawać hello zawartości baz danych, które wcześniej były włączone lub wyłączone SPZ i użyje hello poprzednie ustawienia.

