
As kubernetes people [dislike taken context or namespace from environment variables](https://github.com/kubernetes/kubernetes/issues/27308),
using tools as [kubectx](https://github.com/ahmetb/kubectx/blob/master/README.md) for comfortable context switching might become a must.
In that path, showing some [kubernetes environment values on prompt](https://github.com/jonmosco/kube-ps1/blob/master/README.md) is likely also useful

The default `kube-ps1` becomes a bit redundant, as the context encapsulates both the cluster & namespace. Changing `KUBE_PS1_NS_ENABLE` is an option,
but we can just replace the context name with the cluster one
```bash
_kube_ps1_get_cluster() {
  kubectl config view --minify --output 'jsonpath={..clusters..name}' 2>/dev/null
  }
KUBE_PS1_CLUSTER_FUNCTION=_kube_ps1_get_cluster
```

But after a few days using this combination, it is a bit uncomfortable. Partly because so many `kube*` breaks a bit tab completion, but mainly because
the way kubectx works is setting values globally, setting them across all the open shells and in fact disabling working simultaneously with more than one context.  
A simple way to handle this is taking advantage of `kubectl` merging capabilities, with an environment variable like

KUBECONFIG=.k8s.current:~/.kube/config

which allows fixing the context based on the current directory, which seems a sensible tradeoff

