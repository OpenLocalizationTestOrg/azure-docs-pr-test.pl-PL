## <a name="what-are-service-bus-topics-and-subscriptions"></a>Co to są tematy i subskrypcje usługi Service Bus?
Tematy i subskrypcje usługi Service Bus obsługują model komunikacji z użyciem *publikowania/subskrypcji* komunikatów. Podczas korzystania z tematów i subskrypcji składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem tematu, która działa jako pośrednik.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

W przeciwieństwie do kolejek usługi Service Bus, w których każdy komunikat jest przetwarzany przez jednego konsumenta, tematy i subskrypcje zapewniają formę komunikacji „jeden do wielu” z użyciem wzorca publikowania/subskrypcji. Istnieje możliwość zarejestrowania wielu subskrypcji tooa tematu. Jeżeli tooa tematu jest wysyłany komunikat, jest następnie on proces toohandle subskrypcji tooeach dostępne niezależnie.

Temat tooa subskrypcji przypomina wirtualną kolejkę, która odbiera kopie wiadomości powitania, które zostały wysłane toohello tematu. Opcjonalnie można zarejestrować reguły filtrów dla tematu oparte na subskrypcji, co pozwala toofilter lub ograniczenia, które tematu tooa komunikaty są odbierane przez poszczególne subskrypcje.

Tematy usługi Service Bus i subskrypcje pozwalają tooscale i przetwarzanie bardzo dużej liczby komunikatów przez wielu użytkowników i aplikacje.

## <a name="create-a-namespace"></a>Tworzenie przestrzeni nazw
toobegin przy użyciu usługi Service Bus tematów i subskrypcji platformy Azure, musisz najpierw utworzyć *przestrzeni nazw usługi*. Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.

toocreate przestrzeni nazw:

1. Zaloguj się na toohello [portalu Azure][Azure portal].
2. W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **integracji przedsiębiorstwa**, a następnie kliknij przycisk **usługi Service Bus**.
3. W hello **tworzenie przestrzeni nazw** okna dialogowego, wprowadź nazwę przestrzeni nazw. system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.
4. Po co czy hello przestrzeni nazw jest dostępna, należy wybrać hello cenowym (podstawowa, standardowa lub Premium).
5. W hello **subskrypcji** pola, wybierz subskrypcję platformy Azure, w których toocreate hello nazw.
6. W hello **grupy zasobów** wybierz istniejącą grupę zasobów, w których hello przestrzeni nazw zostanie na żywo lub Utwórz nową.      
7. W **lokalizacji**, wybierz hello kraj lub region, w którym ma być hostowana przestrzeni nazw.
   
    ![Create namespace][create-namespace]
8. Kliknij przycisk hello **Utwórz** przycisku. teraz Hello system utworzy przestrzeń nazw i włączy ją. Toowait może mieć kilka minut hello systemu inicjowania obsługi administracyjnej zasobów dla Twojego konta.

### <a name="obtain-hello-credentials"></a>Uzyskaj poświadczenia hello
1. Kliknij hello nowo utworzona nazwa przestrzeni nazw na liście hello przestrzeni nazw.
2. W hello **przestrzeni nazw usługi Service Bus** bloku, kliknij przycisk **zasady dostępu współużytkowanego**.
3. W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. W hello **zasad: RootManageSharedAccessKey** bloku, kliknij przycisk Kopiuj hello obok zbyt**połączenia ciąg — podstawowy klucz**, toocopy hello połączenia ciąg tooyour Schowka do późniejszego użycia.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


