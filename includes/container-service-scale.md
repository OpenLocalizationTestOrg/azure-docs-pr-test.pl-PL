Po [wdrożeniu klastra usługi Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md) być może trzeba będzie zmienić liczbę węzłów agenta. Możesz na przykład potrzebować więcej agentów, aby uruchamiać więcej wystąpień lub aplikacji kontenera. 

Możesz zmienić liczbę węzłów agenta w klastrze DC/OS, Docker Swarm lub Kubernetes za pomocą witryny Azure Portal lub interfejsu wiersza polecenia platformy Azure w wersji 2.0. 

## <a name="scale-with-the-azure-portal"></a>Skalowanie w witrynie Azure Portal

1. W witrynie [Azure Portal](https://portal.azure.com) przejdź do pozycji **Usługi kontenerów**, a następnie kliknij usługę kontenera, którą chcesz zmodyfikować.
2. W bloku **Usługi kontenerów** kliknij przycisk **Agenci**.
3. W polu **Liczba maszyn wirtualnych** wpisz odpowiednią liczbę węzłów agentów.

    ![Skalowanie puli w portalu](./media/container-service-scale/container-service-scale-portal.png)

4. Aby zapisać konfigurację, kliknij pozycję **Zapisz**.

## <a name="scale-with-the-azure-cli-20"></a>Skalowanie przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0

Upewnij się, że [zainstalowano](/cli/azure/install-az-cli2) najnowszy interfejs wiersza polecenia platformy Azure 2.0 i zalogowano się na koncie platformy Azure (`az login`).

### <a name="see-the-current-agent-count"></a>Sprawdzanie bieżącej liczby agentów
Aby wyświetlić bieżącą liczbę agentów w klastrze, uruchom polecenie `az acs show`. Przedstawia ono konfigurację klastra. Na przykład następujące polecenie przedstawia konfigurację usługi kontenera o nazwie `containerservice-myACSName` w grupie zasobów `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

Polecenie zwraca liczbę agentów w wartości `Count` w obszarze `AgentPoolProfiles`.

### <a name="use-the-az-acs-scale-command"></a>Użycie polecenia az acs scale
Aby zmienić liczbę węzłów agenta, uruchom polecenie `az acs scale` i określ **grupę zasobów**, **nazwę usługi kontenera** i żądaną **nową liczbę agentów**. Używając mniejszej lub większej liczby, możesz odpowiednio skalować w dół lub w górę.

Aby na przykład zmienić liczbę agentów w poprzednim klastrze na 10, wpisz następujące polecenie:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Interfejs wiersza polecenia platformy Azure 2.0 zwraca ciąg JSON reprezentujący nową konfigurację usługi kontenera, w tym nową liczbę agentów.

Aby uzyskać więcej opcji poleceń, uruchom polecenie `az acs scale --help`.

## <a name="scaling-considerations"></a>Zagadnienia dotyczące skalowania

* Liczba węzłów agenta musi należeć do przedziału od 1 do 100 włącznie. 

* Limit przydziału rdzeni może ograniczyć liczbę węzłów agenta w klastrze.

* Operacje skalowania węzła agenta są stosowane do zestawu skalowania maszyn wirtualnych platformy Azure, który zawiera pulę agentów. W klastrze DC/OS tylko węzły agenta w puli prywatnej są skalowane przy użyciu operacji przedstawionych w tym artykule.

* W zależności od wdrażanego w klastrze koordynatora można oddzielnie skalować liczbę wystąpień kontenera uruchomionego w klastrze. Na przykład w klastrze DC/OS należy użyć [interfejsu użytkownika platformy Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md), aby zmienić liczbę wystąpień aplikacji kontenera.

* Obecnie automatyczne skalowanie węzłów agenta w klastrze usługi kontenera nie jest obsługiwane.

## <a name="next-steps"></a>Następne kroki
* Zobacz [więcej przykładów](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) używania poleceń interfejsu wiersza polecenia platformy Azure 2.0 z usługą Azure Container Service.
* Dowiedz się więcej o [pulach agentów platformy DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) w usłudze Azure Container Service.

