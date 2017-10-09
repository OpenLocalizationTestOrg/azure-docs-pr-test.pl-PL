Większość błędów uwierzytelniania czasu hello wynikiem ustawienia konfiguracji nieprawidłowe lub niezgodne. Poniżej przedstawiono niektóre określone propozycje toocheck rzeczy.

* Upewnij się, że nie zostały pominięte hello **zapisać** przycisk z dowolnego miejsca. Jest to często toodo łatwe, a wynik hello jest użytkownik będzie patrzeć hello poprawnych wartości na stronie portalu, ale faktycznie nie zostały zapisane w aplikacji usługi Azure AD lub hello środowiska platformy Azure.
* Dla ustawienia skonfigurowane w hello **ustawienia aplikacji** bloku hello portalu Azure, upewnij się, że hello aplikacji sieci web lub aplikacji interfejsu API wybrano po hello ustawienia zostały wprowadzone poprawne.  Upewnij się, czy hello ustawienia zostały wprowadzone, jak również **ustawień aplikacji** i nie **parametry połączenia**, ponieważ format hello hello dwóch sekcjach jest podobne.
* Dla uwierzytelniania tooa JavaScript frontonu, hello pobierania manifestu ponownie tooverify który `oauth2AllowImplicitFlow` został pomyślnie zmieniony zbyt`true`.
* Sprawdź, czy wszędzie tam, gdzie skonfigurowanych adresów URL HTTPS używanego:
  
  * W kodzie projektu
  * W specyfikacji CORS
  * W ustawieniach aplikacji środowiska platformy Azure dla każdej aplikacji interfejsu API i aplikacji sieci web
  * W ustawieniach aplikacji usługi Azure AD.
    
    Należy pamiętać, że adres URL aplikacji interfejsu API jest skopiowany z portalu hello, często ma `http://` i masz toomanually ją zmienić zbyt`https://`.
* Upewnij się, że wszystkie zmiany kodu zostały pomyślnie wdrożone. Na przykład w rozwiązaniu do wielu projektów jest możliwe toochange projektu przez kod i przypadkowo wybierz jedną z hello innym gdy zamierzasz toodeploy hello zmiany.
* Upewnij się, że ma tooHTTPS adresów URL w przeglądarce, a nie adresów URL protokołu HTTP. Domyślnie program Visual Studio tworzy opublikować profile z adresów URL protokołu HTTP, a to co otwiera w przeglądarce powitania po wdrożeniu projektu.
* Dla uwierzytelniania tooa JavaScript frontonu upewnij się, że CORS został poprawnie skonfigurowany na powitania aplikacji interfejsu API, który hello wywołań kodu JavaScript. W razie wątpliwości, czy hello problem jest związane z CORS, spróbuj "*" jako hello dozwolone źródłowy adres URL. 
* Fronton JavaScript Otwórz w przeglądarce konsoli narzędzi dla deweloperów kartę tooget więcej informacji o błędzie i zbadać żądań HTTP na powitania sieci. Jednak komunikaty o błędach w konsoli może być mylące. Jeśli zostanie wyświetlony komunikat informujący o błąd CORS, hello rzeczywistego problemu może być uwierzytelniania. Można sprawdzić, czy jest to przypadek hello przez uruchomienie aplikacji hello z uwierzytelnianiem tymczasowo tymczasowo wyłączone.
* Dla aplikacji interfejsu API platformy .NET, upewnij się, że w przypadku uzyskiwania tylu informacji w komunikatach o błędach możliwie przez ustawienie [tooOff tryb customErrors](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* Dla aplikacji interfejsu API platformy .NET, należy uruchomić [sesję debugowania zdalnego](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)i sprawdź, czy wartości hello hello zmiennych, które są przekazywane toocode, która używa biblioteki ADAL tooacquire tokenu elementu nośnego lub kod, który sprawdza roszczeń wobec identyfikator hello oczekiwano usługi podmiotu zabezpieczeń. Należy pamiętać, że kod można wybrać wartości konfiguracji z różnych źródeł, dzięki czemu możliwe toofind niespodzianki w ten sposób. Na przykład, jeśli użytkownik błędnie `ida:ClientId` jako `ida:ClientID` podczas konfigurowania ustawień środowiska usługi aplikacji Azure, hello kodu może spowodować, że hello `ida:ClientId` wartość, która jest szuka z pliku Web.config hello, ignorowanie hello ustawienia usługi Azure App Service. 
* Jeśli elementy nie działają w normalnym oknie programu Internet Explorer, istniejące logowania może powodować konflikt; Funkcja InPrivate a następnie spróbuj Chrome lub Firefox.

