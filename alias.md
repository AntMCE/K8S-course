# autocomplete kubectl & helm
source <(kubectl completion zsh)
source <(helm completion zsh)

alias k=kubectl

# when using below aliases, print kubectl command and then execute it
function kctl() { echo "+ kubectl $@" && command kubectl $@ }

# add aliases collection like 'kgpo' for 'kubectl get pods` from https://github.com/ahmetb/kubectl-aliases
[ ! -f ~/.kube/aliases.sh ] && curl -fsSL "https://raw.githubusercontent.com/ahmetb/kubectl-aliases/master/.kubectl_aliases" > ~/.kube/aliases.sh && sed -i -e 's/kubectl/kctl/g' ~/.kube/aliases.sh
source ~/.kube/aliases.sh

# set default namespace
alias kn='kctl config set-context --current --namespace'
# get events sorted by last timestamp
alias kgel='kctl get events --sort-by=.lastTimestamp'
# get events sorted by creation timestamp
alias kgec='kctl get events --sort-by=.metadata.creationTimestamp'
# get pod's descending events
function kger() { kctl get events --sort-by=.lastTimestamp --field-selector involvedObject.name="$@" }
# get 'real' all
alias kgworld='kctl get $(kubectl api-resources --verbs=list --namespaced -o name | paste -sd ",")'
# display all nodes resources request and limits
alias kgnr="k get nodes --no-headers | awk '{print \$1}' | xargs -I {} sh -c 'echo {} ; kubectl describe node {} | grep Allocated -A 5 | grep -ve Event -ve Allocated -ve percent -ve -- ; echo '"
# start a debug pod (including lots of troubleshooting tools)
alias kdebug="kctl -n default run debug-$USER --rm -it --tty --image leodotcloud/swiss-army-knife:v0.12 --image-pull-policy=IfNotPresent -- bash"
# get pod's containers list
function kgpc() { kctl get pod -o jsonpath="{.spec.containers[*].name}" "$@" && echo "" }
# ping a service, ex: 'kping whoami:8080'
alias kping='kctl run httping -it --image bretfisher/httping --image-pull-policy=IfNotPresent --rm=true --'
# get existing pod's yaml without forbidden fields, ex: 'kyaml pod whoami'
function kyaml() { kubectl get "$@" -o yaml | kubectl-neat }
# display and delete failed pods in current namespace
alias krmfailed='kctl delete pods --field-selector=status.phase=Failed'
