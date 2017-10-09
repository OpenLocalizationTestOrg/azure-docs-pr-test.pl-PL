# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Wprowadź klastra połączenia zdalnego tooa Kubernetes, DC/OS lub Docker Swarm
Po utworzeniu klastra usługi kontenera platformy Azure, należy tooconnect toohello klastra toodeploy i zarządzanie zadaniami. W tym artykule opisano, jak tooconnect toohello wzorca wirtualna hello klastra ze zdalnego komputera. 

klastry Kubernetes DC/OS i Docker Swarm Hello Podaj lokalnie punktów końcowych HTTP. Dla Kubernetes, ten punkt końcowy jest bezpiecznie narażony na hello internet i można do niego dostęp, uruchamiając hello `kubectl` narzędzia wiersza polecenia z dowolnego komputera podłączonego do Internetu. 

DC/OS i Docker Swarm zaleca się tworzenia tunelu bezpiecznej powłoki (SSH) z systemu zarządzania klastrem toohello komputera lokalnego. Po ustanowieniu tunelu hello, możesz uruchamiać polecenia korzystające z punktów końcowych HTTP hello i widoku hello orchestrator interfejs sieci web (jeśli jest dostępna) z systemu lokalnego. 

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Kubernetes, DC/OS lub Docker Swarm [wdrożony w usłudze Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA pliku klucza prywatnego odpowiadającego toohello publicznego klucza toohello dodano klastra podczas wdrażania. Tych poleceniach założono, jest klucz prywatny SSH hello `$HOME/.ssh/id_rsa` na tym komputerze. Zobacz te instrukcje dla systemów [macOS i Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../articles/virtual-machines/linux/ssh-from-windows.md), aby uzyskać więcej informacji. Jeśli hello połączenia SSH nie działa, może być konieczne zbyt [zresetować Twoje klucze SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Połącz tooa Kubernetes klastra

Wykonaj te kroki tooinstall i skonfigurować `kubectl` na tym komputerze.

> [!NOTE] 
> W systemie Linux lub macOS, może być konieczne toorun hello polecenia w tej sekcji przy użyciu `sudo`.
> 

### <a name="install-kubectl"></a>Instalowanie narzędzia kubectl
Jednym ze sposobów tooinstall to narzędzie jest toouse hello `az acs kubernetes install-cli` polecenia 2.0 interfejsu wiersza polecenia platformy Azure. toorun to polecenie, upewnij się, że możesz [zainstalowane](/cli/azure/install-az-cli2) hello najnowsze Azure CLI 2.0 i rejestrowane w tooan konto platformy Azure (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Alternatywnie można pobrać hello najnowszych `kubectl` klienta bezpośrednio z hello [Kubernetes zwalnia strony](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Aby uzyskać więcej informacji, zobacz [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalowanie i konfigurowanie narzędzia kubectl).

### <a name="download-cluster-credentials"></a>Pobieranie poświadczeń klastra
Po utworzeniu `kubectl` zainstalowany, należy toocopy hello klastra poświadczenia tooyour maszyny. Jednym ze sposobów toodo get hello poświadczeń jest z hello `az acs kubernetes get-credentials` polecenia. Przekaż hello nazwę grupy zasobów hello i hello Nazwa zasobu usługi kontenera hello:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

To polecenie pobiera poświadczenia klastra hello zbyt`$HOME/.kube/config`, gdzie `kubectl` oczekuje toobe znajduje się.

Alternatywnie można użyć `scp` toosecurely kopiowania hello pliku z `$HOME/.kube/config` na komputerze lokalnym hello głównej maszyny Wirtualnej tooyour. Na przykład:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Jeśli w systemie Windows, można użyć Bash na Ubuntu systemu Windows, klient kopiowania PuTTy bezpiecznych plików hello lub podobnego narzędzia.

### <a name="use-kubectl"></a>Używanie narzędzia kubectl

Po utworzeniu `kubectl` skonfigurowane, Testuj połączenie hello poprzez wyszczególnienie hello węzłów w klastrze:

```bash
kubectl get nodes
```

Możesz wypróbować inne polecenia narzędzia `kubectl`. Na przykład można wyświetlić hello Kubernetes pulpitu nawigacyjnego. Najpierw uruchom serwer proxy serwera interfejsu API Kubernetes toohello:

```bash
kubectl proxy
```

Hello Kubernetes interfejsu użytkownika jest teraz dostępne pod adresem: `http://localhost:8001/ui`.

Aby uzyskać więcej informacji, zobacz hello [Kubernetes szybki start](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Połącz z klastrem DC/OS lub Swarm tooa

hello toouse DC/OS i Docker Swarm klastrów wdrożone przez usługi kontenera platformy Azure, wykonaj te instrukcje toocreate tunelu SSH z lokalnego systemu Linux, macOS lub systemu Windows. 

> [!NOTE]
> Te instrukcje koncentrują się na tunelowaniu ruchu TCP przez protokół SSH. Można też uruchomić sesji interaktywnej SSH z jednego z systemów zarządzania hello wewnątrz klastra, ale nie jest to zalecane. Praca bezpośrednio na systemie wewnętrznym niesie za sobą ryzyko wprowadzenia niezamierzonych zmian w konfiguracji.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Tworzenie tunelu SSH w systemie Linux lub macOS
Hello pierwszym krokiem tworzenia tunelu SSH w systemie Linux lub macOS jest toolocate hello publicznej nazwy DNS hello zrównoważonym obciążeniem. Wykonaj następujące kroki:


1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello grupę zasobów, zawierającą klaster usługi kontenera. Rozwiń grupę zasobów hello tak, aby każdy z zasobów jest wyświetlana. 

2. Kliknij przycisk hello **usługi kontenera** zasobów, a następnie kliknij przycisk **omówienie**. Witaj **wzorca nazwy FQDN** z hello klastra jest wyświetlana w obszarze **Essentials**. Zapisz tę nazwę do późniejszego użycia. 

    ![Publiczna nazwa DNS](./media/container-service-connect/pubdns.png)

    Można również uruchomić hello `az acs show` polecenia w usłudze kontenera. Wyszukaj hello **wzorca profilu: fqdn** właściwości w danych wyjściowych polecenia hello.

3. Teraz Otwórz powłokę i uruchom hello `ssh` polecenie, określając hello następujące wartości: 

    **LOCAL_PORT** jest port TCP powitania po stronie usługi hello tooconnect tunelu hello do. W przypadku klastra Swarm Ustaw ten too2375. W przypadku DC/OS wartość ta too80. 
    **REMOTE_PORT** jest port hello hello punktu końcowego, które mają tooexpose. W przypadku klastra Swarm jest to port 2375. W przypadku klastra DC/OS jest to port 80.  
    **Nazwa użytkownika** jest nazwą użytkownika hello dostarczony po wdrożeniu klastra hello.  
    **DNSPREFIX** jest hello prefiks DNS podany podczas wdrażania klastra hello.  
    **REGION** jest hello regionu, w którym znajduje się w grupie zasobów.  
    **PATH_TO_PRIVATE_KEY** [OPCJONALNIE] to hello ścieżki toohello klucza prywatnego, który odpowiada toohello klucza publicznego podane podczas tworzenia klastra hello. Użyj tej opcji z hello `-i` flagi.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Hello port połączenia SSH to 2200, a nie hello standardowy port 22. W klastrze z więcej niż jedną maszyną Wirtualną głównego jest hello połączenia portu toohello pierwszego serwera głównego maszyny Wirtualnej.
  > 

  polecenie Hello zwraca bez danych wyjściowych.

Przykłady hello DC/OS i Swarm w hello następujące sekcje.    

### <a name="dcos-tunnel"></a>Tunel DC/OS
tooopen tunelu dla punktów końcowych DC/OS, uruchom polecenie, takie jak następujące hello:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 80. Jeśli to konieczne, możesz określić port lokalny inny niż 80, na przykład 8080. Jednak gdy ten port jest używany, niektóre linki w interfejsie użytkownika sieci Web mogą nie działać.
>

Punkty końcowe DC/OS hello można uzyskać dostęp z systemu lokalnego za pośrednictwem hello następujące adresy URL (przy założeniu lokalnych port 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Podobnie można osiągnąć hello interfejsów API rest dla każdej aplikacji przez ten tunel.

### <a name="swarm-tunnel"></a>Tunel Swarm
tooopen punktu końcowego Swarm toohello tunelu, uruchom polecenie, takie jak następujące hello:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 2375. Na przykład jeśli jest uruchomiony demon Docker hello lokalnie, jest ustawiona przez domyślny toouse port 2375. Jeśli to konieczne, możesz określić port lokalny inny niż 2375.
>

Można teraz uzyskać dostępu do hello klaster Docker Swarm przy użyciu interfejsu wiersza polecenia Docker hello (Docker CLI) w systemie lokalnym. Aby uzyskać instrukcje dotyczące instalacji, zobacz [Instalowanie platformy Docker](https://docs.docker.com/engine/installation/).

Ustaw zmienną DOCKER_HOST toohello w środowisku portów lokalnych skonfigurowane dla hello tunelu. 

```bash
export DOCKER_HOST=:2375
```

Uruchom polecenia Docker klastrze Docker Swarm toohello tunelu. Na przykład:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Tworzenie tunelu SSH w systemie Windows
Istnieje wiele opcji tworzenia tuneli SSH w systemie Windows. Jeżeli Bash na Ubuntu działają w systemie Windows lub podobnego narzędzia, należy wykonać instrukcje tunelowania SSH hello przedstawionej w tym artykule, aby system macOS i Linux. Alternatywnie w systemie Windows, w tej sekcji opisano sposób toouse PuTTY toocreate hello tunelu.

1. [Pobierz program PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour systemu Windows.

2. Uruchamianie aplikacji hello.

3. Wprowadź nazwę hosta, który składa się z nazwy użytkownika administratora klastra hello i hello publicznej nazwy DNS pierwszego serwera głównego hello w klastrze hello. Witaj **nazwy hosta** wygląda podobnie zbyt`azureuser@PublicDNSName`. Wprowadź wartość 2200 dla hello **portu**.

    ![Konfiguracja programu PuTTY 1](./media/container-service-connect/putty1.png)

4. Wybierz pozycje **SSH > Uwierzytelnianie**. Dodaj ścieżkę tooyour plik klucza prywatnego (format ppk) do uwierzytelniania. Można użyć narzędzia, takie jak [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate to plik z hello klastra hello toocreate używane klucza SSH.

    ![Konfiguracja programu PuTTY 2](./media/container-service-connect/putty2.png)

5. Wybierz **SSH > tuneli** i skonfigurować hello następujące przekazane porty:

    * **Port źródłowy:** — użyj portu 80 w przypadku opcji DC/OS lub portu 2375 w przypadku opcji Swarm.
    * **Miejsce docelowe:** — użyj wartości localhost:80 w przypadku opcji DC/OS lub wartości localhost:2375 w przypadku opcji Swarm.

    Poniższy przykład Hello jest skonfigurowany dla DC/OS, ale będzie wyglądać podobnie w przypadku rozwiązania Docker Swarm.

    > [!NOTE]
    > W przypadku tworzenia tego tunelu nie można używać portu 80.
    > 

    ![Konfiguracja programu PuTTY 3](./media/container-service-connect/putty3.png)

6. Po zakończeniu kliknij przycisk **sesji > Zapisz** toosave hello połączenie konfiguracji.

7. tooconnect toohello programu PuTTY sesji, kliknij przycisk **Otwórz**. Po ustanowieniu połączenia widać hello konfiguracji portów w dzienniku zdarzeń programu PuTTY hello.

    ![Dziennik zdarzeń programu PuTTY](./media/container-service-connect/putty4.png)

Po skonfigurowaniu tunelu hello w przypadku opcji DC/OS, możesz uzyskać dostęp hello powiązane punkty końcowe na:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Po skonfigurowaniu hello tunelu dla rozwiązania Docker Swarm, otwórz tooconfigure ustawień z systemu Windows w systemie zmienną środowiskową o nazwie `DOCKER_HOST` o wartości `:2375`. Następnie mają dostęp do klastra Swarm hello przez hello interfejsu wiersza polecenia Docker.

## <a name="next-steps"></a>Następne kroki
Wdrażanie kontenerów i zarządzanie nimi w klastrze:

* [Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Praca z hello usługi kontenera platformy Azure i klastrem Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

