```bash
sudo apt install bast-completion
```

> insert in .bashrc file

```bash
source <(kubectl completion bash)
alias k=kubectl
complete -o default -F __start_kubectl k
```
