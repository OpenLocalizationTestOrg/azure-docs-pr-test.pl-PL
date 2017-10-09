# <a name="securing-docker-containers-in-azure-container-service"></a>Zabezpieczanie kontenerów Docker w usłudze Azure Container Service

W tym artykule przedstawiono zagadnienia i zalecenia dotyczące zabezpieczania kontenerów Docker wdrożonych w usłudze Azure Container Service. Wiele z tych zagadnień zazwyczaj stosowane tooDocker kontenery wdrożone w Azure lub innych środowisk. 

## <a name="image-security"></a>Zabezpieczenia obrazu

Kontenery są kompilowane na podstawie obrazów przechowywanych w co najmniej jednym repozytorium. Te repozytoria mogą należeć toopublic lub rejestrów Kontener prywatny. Przykładem rejestru publicznego jest usługa [Docker Hub](https://hub.docker.com/). Przykładem prywatnej rejestru jest hello [Docker zaufane rejestru](https://docs.docker.com/datacenter/dtr/2.0/), które mogą być zainstalowane na lokalnym lub w chmurze prywatnej wirtualnego. Dostępne są także usługi prywatnych rejestrów kontenerów oparte na chmurze, w tym usługa [Azure Container Registry](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Obrazy publiczne i prywatne
Ogólnie — podobnie jak w przypadku każdego publikowanego publicznie pakietu oprogramowania — publicznie dostępny obraz kontenera nie gwarantuje bezpieczeństwa. Obrazy kontenera składają się z wielu warstw oprogramowania, a każda warstwa oprogramowania może mieć luki w zabezpieczeniach. Jest toounderstand klucza hello pochodzenia hello kontener obrazu, tym właściciela hello hello obrazu (Jeśli nie jest on wiarygodnego źródła toodetermine), hello warstwy oprogramowania, które składa się z i hello wersje oprogramowania. 

Na przykład, jeśli przejdziesz toohello oficjalnego [repozytorium nginx](https://hub.docker.com/_/nginx/) w Centrum Docker i przejdź toohello **tagi** kartę, zobacz oznaczone kolorami luk w zabezpieczeniach w każdego obrazu. Każdy kolor przedstawia hello luki w zabezpieczeniach oprogramowania warstwy hello obrazu. Aby uzyskać więcej informacji o wyszukiwaniu luk w zabezpieczeniach w usłudze Docker Hub, zobacz [Understanding official repos on Docker Hub (Opis oficjalnych repozytoriów w usłudze Docker Hub)](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/).

![Obrazy nginx w usłudze Docker Hub](./media/container-service-security/docker-hub-nginx.png)

Głęboko szczególną uwagę przedsiębiorstw o zabezpieczeniach i tooprotect powinno się przed atakiem zabezpieczeń przechowywanie i pobieranie obrazów z prywatnej rejestru, takie jak rejestru kontenera platformy Azure lub rejestru zaufane Docker. Dodanie tooproviding zarządzanych rejestru prywatne, rejestru kontenera Azure obsługuje [usługi uwierzytelniania opartego na podmiot zabezpieczeń](../articles/container-registry/container-registry-authentication.md) za pośrednictwem usługi Azure Active Directory dla przepływów uwierzytelnianie podstawowe, łącznie z dostępem opartej na rolach dla tylko do odczytu, zapisu i uprawnień właściciela.

### <a name="image-security-scanning"></a>Skanowanie zabezpieczeń obrazów

Nawet w przypadku używania prywatnej rejestru, jest obrazem toouse dobrze skanowania rozwiązania dla dodatkowych walidacji. Każda warstwa oprogramowania w obrazie kontenera jest potencjalnie podatne toovulnerabilities niezależnie od innych warstw hello kontener obrazu. Jak coraz więcej firm przystąpić do wdrażania ich obciążeń produkcyjnych oparte na technologii kontenera, skanowanie obrazu staje się ważne tooensure zapobiegania zagrożeń bezpieczeństwa przed ich organizacji. 

Zabezpieczenia, monitorowanie i skanowanie rozwiązań, takich jak [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) i [zabezpieczeń Akwamaryna](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), między innymi, może być tooscan używane kontener obrazów w rejestrze prywatnych i identyfikowania potencjalnych luk w zabezpieczeniach. Należy podać głębokość hello toounderstand skanowania tego hello różnych rozwiązań. Na przykład niektóre rozwiązania mogą tylko sprawdzać warstwy obrazu pod kątem występowania znanych luk w zabezpieczeniach. Te rozwiązania mogą nie być utworzony przy użyciu konkretnego oprogramowania Menedżera pakietów oprogramowania warstwa obrazu tooverify stanie. Inne rozwiązania oferują głębszą integrację skanowania i mogą wyszukiwać luki w zabezpieczeniach dowolnego oprogramowania w pakiecie.

### <a name="production-deployment-rules-and-audit"></a>Reguły wdrożenia produkcyjnego i inspekcja
Gdy aplikacja jest wdrażana w środowisku produkcyjnym, jest ważne tooset kilka tooensure reguł, które obrazy używane w środowisku produkcyjnym są bezpieczne i zawierać nie luk w zabezpieczeniach.

* Z zasady obrazów za pomocą luk w zabezpieczeniach, nawet pomocniczą, nie powinien być dozwolony toorun w środowisku produkcyjnym. Ponadto wszystkie obrazy wdrożony w środowisku produkcyjnym należy najlepiej można zapisać Wybierz dostępny tooa prywatnej rejestru w kilku. Jest również ważne tookeep hello liczba tooensure małych obrazów produkcji czy mogą oni efektywnie zarządzane.

* Ponieważ jest toopinpoint twardym hello pochodzenia oprogramowania za pomocą obrazu publicznie dostępnych kontenera, jest dobrym rozwiązaniem obrazy toobuild wiedzy tooensure źródła pochodzenia hello hello warstwy. Po powierzchni luki w zabezpieczeniach w obrazie własnym wbudowanych kontenera, klientów można znaleźć szybsze rozpoznawanie tooa ścieżki. Z obrazem publicznego klientów musi głównym hello toofind toofix publicznego obrazu go lub Uzyskaj inny obraz bezpiecznego hello wydawcy.

* Dokładnie zeskanowany obraz wdrożony w środowisku produkcyjnym nie jest gwarantowana toobe się toodate hello czas ich istnienia aplikacji hello. Luki w zabezpieczeniach mogą zgłosił warstw hello obrazu, które zostały wcześniej nieznany lub wprowadzone po wdrożeniu produkcyjnym hello. Okresowe inspekcje obrazy wdrożony w środowisku produkcyjnym jest konieczne tooidentify obrazów, które są nieaktualne lub nie były aktualizowane za pewien czas. Jeden może używać metody wdrożenia zielony niebieski i stopniowych mechanizmów uaktualniania tooupdate kontener obrazów bez przestoju. Skanowanie obrazu można zrobić za pomocą narzędzia opisane w powyższej sekcji hello. 

* Potok ciągłej integracji (CI) toobuild obrazów i zintegrowane zabezpieczenia skanowanie może pomóc Obsługa bezpiecznego rejestrów prywatnych z obrazami bezpiecznego kontenera. Witaj luki w zabezpieczeniach skanowanie wbudowana w rozwiązanie CI hello zapewnia obrazów, które przejdą wszystkie testy hello przesyłanych toohello rejestru prywatnych z produkcyjnych wdrożonych obciążeń. Błąd przetwarzania potokowego CI zapewnia nie przesyłanych narażone obrazów w rejestrze prywatnej hello używany we wdrożeniach obciążeń produkcyjnych. Możliwe jest również automatyzowanie skanowania zabezpieczeń obrazów w przypadku znacznej liczby obrazów. W przeciwnym razie proces ręcznego przeprowadzania inspekcji obrazów w celu wyszukania luk w zabezpieczeniach może być niezwykle żmudny i narażony na błędy.

## <a name="host-level-container-isolation"></a>Izolacja kontenera na poziomie hosta
Aplikacje kontenera wdrażane przez klienta w zasobach platformy Azure są wdrażane na poziomie subskrypcji w grupach zasobów i nie są dostępne w wielu dzierżawach. Oznacza to, że jeśli klient korzysta z subskrypcji z innymi osobami, żadne granice nie są, które mogą być wbudowane między dwoma wdrożeniami w hello sam subskrypcji. W związku z tym zabezpieczenia na poziomie kontenera nie są gwarantowane. 

Możliwe jest również toounderstand krytycznych, że kontenery udostępniać jądra hello i zasoby hello hosta hello, (czyli w usłudze kontenera platformy Azure maszyny Wirtualnej platformy Azure w klastrze). Z tego względu kontenery działające w środowisku produkcyjnym muszą być uruchamiane w trybie użytkownika bez uprawnień. Uruchomione z uprawnieniami głównego kontener może naruszyć hello całego środowiska. W przypadku dostępu do poziomu głównego w kontenerze haker mogą uzyskać dostęp toohello głównego pełne uprawnienia na hoście hello. Ponadto jest ważne toorun kontenery w systemach plików tylko do odczytu. Zapobiega to kogoś, kto ma dostęp toohello naruszony kontenera toowrite złośliwych skryptów toohello system plików i uzyskanie dostępu tooother plików. Podobnie jest ważne toolimit hello zasobów (takich jak pamięci, procesora CPU i przepustowości sieci) przydzielone tooa kontenera. Pomaga to zapobiec hakerów zajmowaniu zasobów i wykonać niedozwolone działania, takie jak karty kredytowej oszustwa lub bitcoin wyszukiwania, co może uniemożliwić inne kontenery uruchomiona na hoście hello lub w klastrze.

## <a name="orchestrator-considerations"></a>Zagadnienia dotyczące koordynatora

Każdy koordynator dostępny w usłudze Azure Container Service ma własne względy bezpieczeństwa. Na przykład należy ograniczyć bezpośredniego węzłów tooorchestrator SSH dostępu w usłudze kontenera. Zamiast tego należy użyć interfejsu użytkownika lub narzędzia wiersza polecenia każdego orchestrator (takich jak `kubectl` dla Kubernetes) środowiska kontenera hello toomanage bez uzyskiwania dostępu do hostów hello. Aby uzyskać więcej informacji, zobacz [upewnij klastra połączenia zdalnego tooa Kubernetes, DC/OS lub Docker Swarm](../articles/container-service/kubernetes/container-service-connect.md).

Informacje dodatkowe zabezpieczenia specyficzne dla programu orchestrator Zobacz hello następujące zasoby:

* **Kubernetes**: [Security Best Practices for Kubernetes Deployment (Kubernetes: najlepsze rozwiązania dotyczące zabezpieczeń na potrzeby wdrażania rozwiązania Kubernetes)](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [Securing Your Cluster (DC/OS: zabezpieczanie klastra)](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [Docker Security (Docker Swarm: zabezpieczenia platformy Docker)](https://www.docker.com/docker-security)

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji o zabezpieczeniach architektury i kontener Docker, zobacz [tooContainer wprowadzenie zabezpieczeń](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Aby uzyskać informacje na temat zabezpieczeń platformy Azure, zobacz hello [Centrum zabezpieczeń Azure](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
