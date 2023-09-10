# chapter01_cluster-create

- Install tools
  ```bash
  ./install-tools.sh
  ```

- Increase the resouce limits
  - see: https://kind.sigs.k8s.io/docs/user/known-issues/#pod-errors-due-to-too-many-open-files
  ```bash
  sudo sysctl fs.inotify.max_user_watches=524288
  sudo sysctl fs.inotify.max_user_instances=512

  # To make the changes persistent
  cat <<EOF >> /etc/sysctl.conf
  fs.inotify.max_user_watches = 524288
  fs.inotify.max_user_instances = 512
  ```

- Create kind cluster
  ```bash
  kind create cluster --config=kind-config.yaml 
  ```

- Install cilium
  ```bash
  cilium install --version 1.14.1
  ```

- Validate the installation
  ```bash
  cilium connectivity test
  ```

- Hello World
  ```bash
  kubectl run --restart=Never nginx --image=nginx:alpine
  kubectl port-forward nginx 8080:80
  ```

  ```bash
  curl localhost:8080
  ```