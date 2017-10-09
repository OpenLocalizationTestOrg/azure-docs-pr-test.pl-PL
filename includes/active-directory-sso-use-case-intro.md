Organizacji jest używany więcej [oprogramowanie jako usługa (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) aplikacji pod kątem wydajności ponieważ technologii w chmurze i narzędzia stają się coraz bardziej dostępny. Wraz z rozwojem hello liczba aplikacji SaaS, staje się trudne dla kont toomanage Administratorzy hello i praw dostępu, a dla hello tooremember użytkowników różnych haseł. Tworzy dodatkowej pracy i jest mniej bezpieczne indywidualnie Zarządzanie tych aplikacji.

* Pracownicy, którzy mają Śledź tookeep wiele haseł często toouse mniej bezpiecznych tooremember metod, które hello ich zapisanie hasła albo przy użyciu takich samych haseł w wielu kont.
* Gdy dociera do pracownika lub jeden pozostawia, ich kont musi być indywidualnie udostępnione lub usuwane.
* Ponadto pracownicy może zostać uruchomiony przy użyciu aplikacji SaaS w pracy bez pośrednictwa IT, co oznacza, że są one tworzenie własnych kont na komputerach hello Administratorzy IT nie zatwierdzono i nie są monitorowania.  

Logowanie jednokrotne (SSO) jest rozwiązanie wszystkie te problemy. Najprostszym sposobem toomanage ma hello wielu aplikacji, a użytkownikom spójne środowisko logowania jednokrotnego. Azure Active Directory (Azure AD) zapewnia niezawodne rozwiązanie logowania jednokrotnego i ma wiele dostępnych wstępnie zintegrowanych aplikacji, z samouczków dla administratorów tooquickly Konfigurowanie nowej aplikacji i inicjowania obsługi administracyjnej użytkownicy będą rozpoczynać pracę.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Jak Azure Active Directory integracji aplikacji?
Azure AD pozwala działowi toointegrate aplikacji i elastycznie kont. Można to zrobić przy użyciu jednej z dwóch metod.

* Jeśli aplikacja hello jest wstępnie zintegrowanych aplikacji hello galerii, można go za pomocą tego portalu tooset się aplikacji i skonfigurować hello tooallow ustawienia logowania jednokrotnego. Dla dowolnej aplikacji galerii możesz rozpocząć pracę przez wykonaj hello proste instrukcje krok po kroku przedstawiony w galerii aplikacji hello i hello Azure tooenable portalu rejestracji jednokrotnej.
* Jeśli aplikacja hello nie znajduje się w galerii hello, możesz nadal skonfigurować większość aplikacji w usłudze Azure AD jako niestandardowych aplikacji. Wymaga to bardziej technicznych tooconfigure wiedzy. Możesz dodać dowolnej aplikacji, który obsługuje SAML 2.0 jako aplikacji federacyjnych lub dowolnej aplikacji, która jest oparty na języku HTML strony logowania jako aplikację hasło logowania jednokrotnego.

W hello przypadek, w którym użytkownicy utworzono własne konta dla aplikacji SaaS, które nie są zarządzane przez IT, hello [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) narzędzie zapewnia rozwiązanie. To narzędzie monitoruje tooidentify ruchu w sieci web hello aplikacje, które są używane w całej organizacji hello i hello liczba osób przy użyciu każdego z nich. IT można używać tego toolearn informacji użytkownicy aplikacji hello preferowane i zdecydować, które toointegrate do usługi Azure AD dla logowania jednokrotnego.  

Podczas integracji aplikacji z usługą Azure AD, możesz mapować tożsamości tootheir odpowiednich usługi Azure AD tożsamości ustalonych aplikacji hello użytkowników.  

