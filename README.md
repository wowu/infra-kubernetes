# BIT: Warsztaty z Kubernetesa (17.05.2022)

## Instalacja

1. Zainstaluj kubectl: [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) &bull; [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) &bull; [macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/)
2. Sklonuj repozytorium: `git clone https://github.com/wowu/infra-kubernetes`
3. Sprawdź czy posiadasz plik `~/.kube/config`:
   
   ```bash
   cat ~/.kube/config
   ```
   Jeśli plik istnieje to zrób backup:

   ```bash
   mv ~/.kube/config ~/.kube/config.bak
   ```

4. Pobierz config naszego klastra:
   
   ```bash
   mkdir -p ~/.kube
   curl <link-z-prezentacji> > ~/.kube/config
   ```

## Zadanie 1 - podstawowe operacje na podach

1. Sprawdzamy czy możemy połączyć się z klastrem i wylistować node'y:

    ```bash
    kubectl get nodes
    ```

2. Uruchamiamy interaktywnego poda:

    ```bash
    kubectl run -i -t --rm <nazwa> --image=bash:latest
    ```
  
    W drugim terminalu sprawdzamy działające pody:

    ```bash
    kubectl get pods

    # Ze szczegółami
    kubectl get pods -o wide
    ```

    W drugim terminalu wyświetlamy szczegóły pierwszego poda:

    ```bash
    kubectl describe pod <nazwa>
    ```

    Wychodzimy z interaktywnej sesji:

    ```bash
    exit
    ```

3. Uruchamiamy poda:

    ```bash
    kubectl run <nazwa>-date --image=pankarol/infra-date:latest
    ```

    Sprawdzamy działające pody:

    ```bash
    kubectl get pods
    ```

    Wyświetlamy logi naszego poda:

    ```bash
    kubectl logs <nazwa>-date

    # możemy użyć flagi "follow"
    kubectl logs <nazwa>-date -f
    ```

    Usuwamy poda:

    ```bash
    kubectl delete pod <nazwa>-date
    ```

## Zadanie 2 - manifesty i ReplicaSet

1. Zmieniamy `NAZWA` na naszą nazwę w pliku `zadanie-2/replicaset.yaml`.
2. Tworzymy zasoby na klastrze:
   
    ```bash
    kubectl apply -f zadanie-2/replicaset.yaml
    ```
3. Listujemy ReplicaSety:

    ```bash
    kubectl get replicasets

    # lub wersja skrócona
    kubectl get rs
    ```

4. Listujemy pody

    ```bash
    kubectl get pods
    ```

5. Zmieniamy liczbę replik na 2 w `zadanie-2/replicaset.yaml`.
6. Aktualizujemy ReplicaSet:
   
    ```bash
    kubectl apply -f zadanie-2/replicaset.yaml
    ```
7. Usuwamy ReplicaSet:
   
    ```bash
    kubectl delete -f zadanie-2/replicaset.yaml
    ```

## Zadanie 3 - deployment

1. Zmieniamy `NAZWA` na naszą nazwę w pliku `zadanie-3/deployment.yaml`.
2. Tworzymy zasoby na klastrze:
   
    ```bash
    kubectl apply -f zadanie-3/deployment.yaml
    ```
3. Otwieramy NAZWA.k8s.musur.pl
