```bash
sudo apt install bash-completion
```

> insert in .bashrc file

```bash
source <(kubectl completion bash)
alias k=kubectl
complete -o default -F __start_kubectl k
```
