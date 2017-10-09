## <a name="prerequisites"></a>Wymagania wstępne
Zanim firma Microsoft można napisać kod zarządzania CDN, potrzebujemy toodo niektórych tooenable przygotowania toointeract naszego kodu z hello Azure Resource Manager.  toodo, musisz:

* Utwórz zasób hello toocontain grupy profilu CDN, utworzone w tym samouczku
* Konfigurowanie usługi Azure Active Directory tooprovide uwierzytelniania dla aplikacji
* Zastosuj uprawnienia, które toohello grupy zasobów, aby tylko autoryzowani użytkownicy z naszych dzierżawy usługi Azure AD mogą prowadzić interakcję z naszych profilu CDN

### <a name="creating-hello-resource-group"></a>Tworzenie grupy zasobów hello
1. Zaloguj się do hello [Azure Portal](https://portal.azure.com).
2. Kliknij przycisk hello **nowy** przycisk w lewym górnym rogu hello, a następnie **zarządzania**, i **grupy zasobów**.

    ![Tworzenie nowej grupy zasobów](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Wywołaj grupie zasobów *CdnConsoleTutorial*.  Wybierz subskrypcję i wybierz lokalizację, w pobliżu.  Jeśli chcesz, możesz kliknąć pozycję hello **toodashboard numeru Pin** wyboru toopin hello zasobów grupy toohello pulpitu nawigacyjnego w portalu hello.  To spowoduje to łatwiejsze toofind później.  Po określeniu ustawień, kliknij przycisk **Utwórz**.

    ![Grupa zasobów hello nazewnictwa](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Po utworzeniu grupy zasobów hello, jeśli nie przypiąć tooyour pulpitu nawigacyjnego, możesz go znaleźć, klikając **Przeglądaj**, następnie **grup zasobów**.  Kliknij przycisk tooopen grupy zasobów hello go.  Zanotuj Twojej **identyfikator subskrypcji**.  Firma Microsoft będzie on potrzebny później.

    ![Grupa zasobów hello nazewnictwa](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Tworzenie aplikacji hello Azure AD i stosowanie uprawnień
Istnieją dwie metody uwierzytelniania tooapp za pomocą usługi Azure Active Directory: poszczególnych użytkowników lub nazwy głównej usługi. Nazwy głównej usługi jest podobne tooa konta usługi systemu Windows.  Zamiast przyznania toointeract uprawnienia określonego użytkownika, przy użyciu profilów CDN hello, zamiast tego użytkownikowi uprawnienia hello toohello nazwy głównej usługi.  Nazwy główne usług są zazwyczaj używane przez procesy zautomatyzowane, nieinterakcyjnym.  Mimo że w tym samouczku jest pisanie aplikacji konsoli interaktywne, firma Microsoft będzie skupić się na podejście główna usługi hello.

Tworzenie nazwy głównej usługi składa się z kilku kroków, w tym tworzenie aplikacji usługi Azure Active Directory.  toodo to, zbyt zamierzamy[czynności opisane w tym samouczku](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Można toofollow się, że wszystkie kroki hello hello [połączonego samouczek](../articles/resource-group-create-service-principal-portal.md).  Jest *bardzo ważne* zakończyć je dokładnie zgodnie z opisem.  Upewnij się, że toonote Twojego **Identyfikatorem dzierżawy**, **nazwę domeny dzierżawy** (często *. onmicrosoft.com* domeny przed określeniem domenę niestandardową), **identyfikator klienta** , i **klucza uwierzytelniania klienta**, jak firma Microsoft będą one potrzebne później.  Należy zwrócić szczególną uwagę na tooguard Twojego **identyfikator klienta** i **klucza uwierzytelniania klienta**, ponieważ te poświadczenia mogą być używane przez każdy tooexecute operacje jako nazwy głównej usługi hello.
>
> Po wyświetleniu okna toohello krok o nazwie Konfiguracja wielodostępnych aplikacji, wybierz **nr**.
>
> Kiedy uzyskać krok toohello [przypisać toorole aplikacji](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), grupy zasobów hello Użyj utworzony wcześniej, *CdnConsoleTutorial*, ale zamiast hello **czytnika** roli, przypisz Witaj **współautora profilu CDN** roli.  Po przypisaniu hello aplikacji hello **współautora profilu CDN** roli w grupie zasobów, zwracany toothis samouczka. 
>
>

Po utworzeniu usługi hello podmiotu zabezpieczeń i przypisane **współautora profilu CDN** rolę, hello **użytkowników** bloku grupy zasobów powinien wyglądać podobnie toothis.

![Blok użytkowników](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Interakcyjnego uwierzytelniania użytkownika
Jeśli zamiast nazwy głównej usługi, a nie trzeba uwierzytelnianie interakcyjne poszczególnych użytkowników, proces hello jest bardzo podobne toothat dla nazwy głównej usługi.  W rzeczywistości należy toofollow hello tej samej procedury, ale wprowadzić kilka drobne zmiany.

> [!IMPORTANT]
> Tylko wykonaj te czynności Jeśli wybierzesz toouse uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.
>
>

1. Podczas tworzenia aplikacji, zamiast **aplikacji sieci Web**, wybierz **aplikacji natywnej**.

    ![Aplikacja macierzysta](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Na następnej stronie powitania, zostanie wyświetlony monit dla **identyfikator URI przekierowania**.  Witaj identyfikatora URI nie można sprawdzić poprawności, ale należy pamiętać został wprowadzony.  Będzie on potrzebny później.
3. Nie istnieje żadne toocreate potrzeby **klucza uwierzytelniania klienta**.
4. Zamiast przypisywać toohello główna usługi **współautora profilu CDN** roli zamierzamy tooassign poszczególnych użytkowników lub grup.  W tym przykładzie widać, że zostały przypisane *użytkownika pokaz CDN* toohello **współautora profilu CDN** roli.  

    ![Dostęp użytkownika](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
