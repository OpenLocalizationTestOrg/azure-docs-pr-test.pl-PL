
### <a name="installation-failures"></a>Błędy instalacji
| **Przykładowy komunikat o błędzie** | **Zalecana akcja** |
|--------------------------|------------------------|
|Błąd kont tooload nie powiodło się. Błąd: System.IO.IOException: tooread danych z hello transportu połączenia, gdy instalowanie i rejestrowanie hello serwerem CS.| Upewnij się, że protokołu TLS 1.0 jest włączona na komputerze hello. |

### <a name="registration-failures"></a>Błędy rejestracji
Błędy rejestracji może być debugowany, przeglądając dzienniki hello w hello **%ProgramData%\ASRLogs** folderu.

| **Przykładowy komunikat o błędzie** | **Zalecana akcja** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Komunikat: ACS50008: Token SAML jest nieprawidłowy.<br>Identyfikator śledzenia: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>Identyfikator korelacji: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>Sygnatura czasowa: **2016-12-12 14:50:08Z<br>** | Upewnij się, że hello godziną zegar systemowy nie jest czas lokalne powitania więcej niż 15 minut. Witaj ponownie uruchomić Instalatora toocomplete hello rejestracji.|
|**09:35:27** : DRRegistrationException w trakcie tooget wszystkie magazynu odzyskiwania po awarii dla wybranego certyfikatu hello:: zwrócił Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException, Exception.Message: ACS50008: SAML token jest nieprawidłowy.<br>Identyfikator śledzenia: e5ad1af1-2d39-4970-8eef-096e325c9950<br>Identyfikator korelacji: abe9deb8-3e64-464d-8375-36db9816427a<br>Sygnatura czasowa: **2016-05-19 01:35:39Z**<br> | Upewnij się, że hello godziną zegar systemowy nie jest czas lokalne powitania więcej niż 15 minut. Witaj ponownie uruchomić Instalatora toocomplete hello rejestracji.|
|06:28:45: certyfikat toocreate nie powiodło się<br>06:28:45: Nie można kontynuować instalacji. Wymagany certyfikat tooSite tooauthenticate, nie mogą być tworzone odzyskiwania. Uruchom ponownie Instalatora. | Upewnij się, że uruchamiasz Instalatora jako administrator lokalny. |
