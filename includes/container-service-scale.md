# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Skalowanie węzłów agenta w klastrze usługi Container Service
Po [wdrażanie klastra usługi kontenera platformy Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), może być konieczne toochange hello liczba węzłów agenta. Możesz na przykład potrzebować więcej agentów, aby uruchamiać więcej wystąpień lub aplikacji kontenera. 

Można zmienić liczbę hello agenta węzłów w klastrze DC/OS, Docker Swarm lub Kubernetes przy użyciu portalu Azure hello lub hello Azure CLI 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Skalować hello portalu Azure

1. W hello [portalu Azure](https://portal.azure.com), wyszukaj **usługi kontenerów**, a następnie kliknij przycisk hello kontenera usługi, które mają toomodify.
2. W hello **usługi kontenera** bloku, kliknij przycisk **agentów**.
3. W **liczba maszyn wirtualnych**, wprowadź hello żądaną liczbę węzłów agentów.

    ![Skalowanie puli w portalu hello](./media/container-service-scale/container-service-scale-portal.png)

4. Konfiguracja hello toosave, kliknij przycisk **zapisać**.

## <a name="scale-with-hello-azure-cli-20"></a>Skalować hello Azure CLI 2.0

Upewnij się, że możesz [zainstalowane](/cli/azure/install-az-cli2) hello najnowsze Azure CLI 2.0 i rejestrowane w tooan konto platformy azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Zobacz hello bieżąca liczba agentów
toosee hello liczby agentów obecnie w klastrze hello Uruchom hello `az acs show` polecenia. Oznacza to hello konfiguracji klastra. Na przykład Witaj następujące polecenia pokazuje hello konfiguracji hello usługi kontenera o nazwie `containerservice-myACSName` w grupie zasobów hello `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

polecenie Hello zwraca hello liczba agentów w hello `Count` wartości w obszarze `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Użyj hello az polecenia Skaluj acs
toochange hello liczba węzłów agenta, uruchom hello `az acs scale` polecenia i dostawy hello **grupy zasobów**, **nazwa kontenera usługi**i hello potrzeby **nowego licznika agenta**. Używając mniejszej lub większej liczby, możesz odpowiednio skalować w dół lub w górę.

Na przykład toochange hello liczba agentów w poprzednim hello klastra too10, hello wpisz następujące polecenie:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hello Azure CLI 2.0 zwraca ciąg JSON reprezentujący hello nową konfigurację usługi kontenera hello, w tym hello nowego licznika agenta.

Aby uzyskać więcej opcji poleceń, uruchom polecenie `az acs scale --help`.

## <a name="scaling-considerations"></a>Zagadnienia dotyczące skalowania

* Hello liczba węzłów agent musi być od 1 do 100 włącznie. 

* Limitu przydziału rdzeni można ograniczyć liczbę hello agenta węzłów w klastrze.

* Operacje skalowania węzła agenta są zastosowane tooan zestaw skali maszyny wirtualnej platformy Azure, zawierający hello puli agenta. W klastrze DC/OS tylko węzły agenta w puli prywatnej hello są skalowane przez operacje hello wyświetlane w tym artykule.

* W zależności od hello programu orchestrator, które można wdrożyć w klastrze można oddzielnie skalować hello liczbę wystąpień kontenera uruchomiona w klastrze hello. Na przykład w klastrze DC/OS, należy użyć hello [interfejs użytkownika platformy Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello liczbę wystąpień kontenera aplikacji.

* Obecnie automatyczne skalowanie węzłów agenta w klastrze usługi kontenera nie jest obsługiwane.

## <a name="next-steps"></a>Następne kroki
* Zobacz [więcej przykładów](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) używania poleceń interfejsu wiersza polecenia platformy Azure 2.0 z usługą Azure Container Service.
* Dowiedz się więcej o [pulach agentów platformy DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) w usłudze Azure Container Service.

